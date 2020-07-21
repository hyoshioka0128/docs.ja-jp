---
title: C# の予約済み属性:Null 許容のスタティック分析
ms.date: 04/14/2020
description: これらの属性は、null 許容および null 非許容参照型に対するより適切な静的分析を提供するために、コンパイラによって解釈されます。
ms.openlocfilehash: 33521133a6a01196e6e1ab9c3cdc191a24f1ecf3
ms.sourcegitcommit: 73aa9653547a1cd70ee6586221f79cc29b588ebd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "82102711"
---
# <a name="reserved-attributes-contribute-to-the-compilers-null-state-static-analysis"></a>予約済み属性はコンパイラの null 状態の静的分析に寄与する

null 許容コンテキストの場合、コンパイラではコードの静的分析を実行して、すべての参照型変数の null 状態を判断します。

- *null 以外*:静的分析では、変数が null 以外の値に割り当てられていると判断されました。
- *null の可能性あり*:静的分析では、変数に null 以外の値が割り当てられていることを判断できません。

API のセマンティクスについての情報をコンパイラに提供する、いくつかの属性を適用できます。 この情報は、コンパイラで静的分析を実行し、変数が null でないかどうかを判断するのに役立ちます。 この記事では、これらの各属性とその使用方法について簡単に説明します。 すべての例では C# 8.0 以降を想定しており、コードは null 許容コンテキストに含まれています。

よくある例から始めましょう。 ライブラリに、リソース文字列を取得するための次の API があるとします。

```csharp
bool TryGetMessage(string key, out string message)
```

前述の例では、.NET のよくある `Try*` パターンに従っています。 この API には、2 つの参照引数 (`key` および `message` パラメーター) があります。 この API には、これらの引数の null 性に関連する次の規則があります。

- 呼び出し元では、`key` の引数として `null` を渡すことはできません。
- 呼び出し元では、`message` の引数として、値が `null` の変数を渡すことができます。
- `TryGetMessage` メソッドから `true` が返された場合、`message` の値は null ではありません。 戻り値が `false,` である場合、`message` (およびその null 状態) の値は null です。

`key` の規則は、変数型で表すことができます。`key` は null 非許容参照型である必要があります。 `message` パラメーターはより複雑です。 引数として `null` が許可されますが、成功した場合、`out` 引数が null でないことが保証されます。 これらのシナリオでは、予測を記述するために、より豊富なボキャブラリが必要です。

変数の null 状態に関する追加情報を表すために、いくつかの属性が追加されました。 C# 8 で null 許容参照型型が導入される前に記述したすべてのコードでは、"*null が認識されません*" でした。 つまり、参照型変数は null である可能性がありますが、null チェックは必須ではありません。 コードが "*null 許容認識*" になると、それらの規則は変わります。 参照型を `null` 値にすることはできません。また、null 許容参照型は、逆参照される前に `null` に対してチェックする必要があります。

API の規則は、`TryGetValue` API シナリオで見たとおり、より複雑になる可能性があります。 多くの API には、変数を `null` にできる場合やできない場合のより複雑な規則があります。 このような場合は、次の属性のいずれかを使用して、これらの規則を表します。

- [AllowNull](xref:System.Diagnostics.CodeAnalysis.AllowNullAttribute):null 非許容の入力引数は null にすることができます。
- [DisallowNull](xref:System.Diagnostics.CodeAnalysis.DisallowNullAttribute):null 許容の入力引数を null にすることはできません。
- [MaybeNull](xref:System.Diagnostics.CodeAnalysis.MaybeNullAttribute):null 非許容の戻り値は null である可能性があります。
- [NotNull](xref:System.Diagnostics.CodeAnalysis.NotNullAttribute):null 許容の戻り値が null になることはありません。
- [MaybeNullWhen](xref:System.Diagnostics.CodeAnalysis.MaybeNullWhenAttribute):メソッドから指定された `bool` 値が返された場合、null 非許容の入力引数は null である可能性があります。
- [NotNullWhen](xref:System.Diagnostics.CodeAnalysis.NotNullWhenAttribute):メソッドから指定された `bool` 値が返された場合、null 許容の入力引数は null にはなりません。
- [NotNullIfNotNull](xref:System.Diagnostics.CodeAnalysis.NotNullIfNotNullAttribute):指定されたパラメーターの引数が null でない場合、戻り値は null ではありません。
- [DoesNotReturn](xref:System.Diagnostics.CodeAnalysis.DoesNotReturnAttribute):メソッドから制御が返されることはありません。 つまり、常に例外がスローされます。
- [DoesNotReturnIf](xref:System.Diagnostics.CodeAnalysis.DoesNotReturnIfAttribute):関連付けられた `bool` パラメーターに指定された値がある場合、このメソッドから制御が返されることはありません。

前述の説明は、各属性動作に関するクイック リファレンスです。 次の各セクションでは、動作と意味について、より詳しく説明します。

これらの属性を追加すると、API の規則に関する詳細情報がコンパイラに与えられます。 呼び出し元のコードが、null 許容が有効なコンテキストでコンパイルされると、呼び出し元がこれらの規則に違反したときに、コンパイラによって警告されます。 これらの属性では、実装に対する追加のチェックが有効になりません。

## <a name="specify-preconditions-allownull-and-disallownull"></a>事前条件を指定する: `AllowNull` と `DisallowNull`

適切な既定値が設定されているため、`null` を返すことのない読み取りおよび書き込みプロパティについて考えてみます。 呼び出し元では、その既定値に設定するときに、set アクセサーに `null` を渡します。 たとえば、チャット ルームで画面名を要求するメッセージング システムがあるとします。 何も指定されていない場合、システムによってランダムな名前が生成されます。

```csharp
public string ScreenName
{
   get => screenName;
   set => screenName = value ?? GenerateRandomScreenName();
}
private string screenName;
```

null 許容の認識されないコンテキストで上記のコードをコンパイルする場合、何も問題はありません。 null 許容参照型を有効にすると、`ScreenName` プロパティが null 非許容参照になります。 これは `get` アクセサーでは正しい動作です。`null` が返されることはありません。 呼び出し元では、返されたプロパティで `null` をチェックする必要はありません。 しかし、ここでプロパティを `null` に設定すると、警告が生成されます。 この種類のコードを引き続きサポートするには、次のコードに示すように、<xref:System.Diagnostics.CodeAnalysis.AllowNullAttribute?displayProperty=nameWithType> 属性をプロパティに追加します。

```csharp
[AllowNull]
public string ScreenName
{
   get => screenName;
   set => screenName = value ?? GenerateRandomScreenName();
}
private string screenName = GenerateRandomScreenName();
```

これと、この記事で説明されている他の属性を使用するには、<xref:System.Diagnostics.CodeAnalysis> の `using` ディレクティブを追加する必要がある場合があります。 属性は、`set` アクセサーではなく、プロパティに適用されます。 `AllowNull` 属性では "*事前条件*" を指定し、入力にのみ適用されます。 `get` アクセサーには戻り値がありますが、入力引数はありません。 したがって、`AllowNull` 属性は `set` アクセサーにのみ適用されます。

前の例では、引数に `AllowNull` 属性を追加する場合の検索方法が示されています。

1. その変数の一般的なコントラクトは、`null` にできないため、null 非許容参照型が必要であるというものです。
1. 入力変数を `null` にするシナリオはありますが、それらは最も一般的な使用方法ではありません。

ほとんどの場合、プロパティ、または `in`、`out`、および `ref` 引数にこの属性が必要になります。 `AllowNull` 属性は、通常は変数が null 以外だが、`null` を事前条件として許可する必要がある場合に最適です。

`DisallowNull` を使用するシナリオと比較してください。この属性を使用して、null 許容参照型の入力変数を `null` にできないことを指定します。 `null` は既定値であるが、クライアントでは null 以外の値にしか設定できないというプロパティについて考えてみます。 次のコードがあるとします。

```csharp
public string ReviewComment
{
    get => _comment;
    set => _comment = value ?? throw new ArgumentNullException(nameof(value), "Cannot set to null");
}
string _comment;
```

上記のコードは、`ReviewComment` が `null` である可能性はあるが、`null` に設定できないという設計を表すのに最適な方法です。 このコードが null 許容認識になると、<xref:System.Diagnostics.CodeAnalysis.DisallowNullAttribute?displayProperty=nameWithType> を使用して、呼び出し元に対して、この概念をより明確に表すことができます。

```csharp
[DisallowNull]
public string? ReviewComment
{
    get => _comment;
    set => _comment = value ?? throw new ArgumentNullException(nameof(value), "Cannot set to null");
}
string? _comment;
```

null 許容コンテキストでは、`ReviewComment` `get` アクセサーから `null` の既定値が返される可能性があります。 コンパイラからは、アクセスの前にチェックする必要があることが警告されます。 さらに、`null` である可能性があっても、呼び出し元で明示的に `null` に設定できないことが、呼び出し元に警告されます。 `DisallowNull` 属性では、"*事前条件*" も指定され、これは `get` アクセサーには影響しません。 以下について、これらの特性を監視する場合は、`DisallowNull` 属性を使用します。

1. 主なシナリオでは (多くの場合、最初にインスタンス化されるときに)、変数が `null` である可能性があります。
1. 変数は、明示的に `null` に設定することはできません。

このような状況は、もともと "*null として認識されていなかった*" コードでよく見られます。 オブジェクト プロパティが、2 つの異なる初期化操作で設定されている可能性があります。 一部のプロパティは、一部の非同期処理が完了した後にのみ設定される可能性があります。

`AllowNull` および `DisallowNull` 属性を使用すると、変数の事前条件が、これらの変数の null 許容注釈と一致しない可能性があることを指定できます。 これにより、API の特性の詳細が提供されます。 この追加情報は、呼び出し元で API を正しく使用するのに役立ちます。 次の属性を使用して、事前条件を指定することを忘れないでください。

- [AllowNull](xref:System.Diagnostics.CodeAnalysis.AllowNullAttribute):null 非許容の入力引数を null にすることができます。
- [DisallowNull](xref:System.Diagnostics.CodeAnalysis.DisallowNullAttribute):null 許容の入力引数を null にすることはできません。

## <a name="specify-post-conditions-maybenull-and-notnull"></a>事後条件を指定する: `MaybeNull` と `NotNull`

次のシグネチャを持つメソッドがあるとします。

```csharp
public Customer FindCustomer(string lastName, string firstName)
```

検索された名前が見つからなかったときに `null` を返す、このようなメソッドを記述した可能性があります。 `null` は、レコードが見つからなかったことを明確に示しています。 この例では、戻り値の型を `Customer` から `Customer?` に変更する可能性があります。 戻り値を null 許容参照型として宣言すると、この API の意図が明確になります。

「[ジェネリック定義と NULL 値の許容](../../nullable-migration-strategies.md#generic-definitions-and-nullability)」に記載されている理由により、その手法はジェネリック メソッドでは機能しません。 同様のパターンに従うジェネリック メソッドがある場合があります。

```csharp
public T Find<T>(IEnumerable<T> sequence, Func<T, bool> match)
```

戻り値が `T?` であることを指定することはできません。 検索された項目が見つからない場合、このメソッドからは `null` が返されます。 戻り値の型として `T?` を宣言することはできないため、メソッドの戻り値に `MaybeNull` 注釈を追加します。

```csharp
[return: MaybeNull]
public T Find<T>(IEnumerable<T> sequence, Func<T, bool> match)
```

前のコードでは、コントラクトは null 非許容型を意味するが、戻り値は実際には null である "*可能性がある*" ことを呼び出し元に通知します。  API は null 非許容型で、通常はジェネリック型パラメーターである必要はあるが、`null` が返されるインスタンスが存在する可能性がある場合は、`MaybeNull` 属性を使用します。

型が null 許容参照型である場合でも、戻り値あるいは `out` または `ref` 引数が null でないことを指定することもできます。 配列が、多数の要素を保持するのに十分な大きさであることを保証するメソッドについて考えてみます。 入力引数に容量がない場合、ルーチンで新しい配列を割り当てて、そこに既存のすべての要素をコピーします。 入力引数が `null` である場合は、ルーチンで新しいストレージを割り当てます。 十分な容量がある場合、ルーチンでは何も行いません。

```csharp
public void EnsureCapacity<T>(ref T[] storage, int size)
```

次のように、このルーチンを呼び出すことができます。

```csharp
// messages has the default value (null) when EnsureCapacity is called:
EnsureCapacity<string>(ref messages, 10);
// messages is not null.
EnsureCapacity<string>(messages, 50);
```

null 参照型を有効にした後、確実に前のコードが警告なしでコンパイルされるようにする必要があります。 メソッドから制御が戻ったときに、`storage` 引数が null でないことが保証されます。 しかし、null 参照で `EnsureCapacity` を呼び出すことはできます。 `storage` を null 許容参照型にして、`NotNull` 事後条件をパラメーター宣言に追加することができます。

```csharp
public void EnsureCapacity<T>([NotNull]ref T[]? storage, int size)
```

上記のコードは、既存のコントラクトを明確に表しています。呼び出し元では `null` 値を持つ変数を渡すことはできますが、戻り値は null になることはないことが保証されます。 `NotNull` 属性は、`null` が引数として渡される可能性があるが、メソッドから制御が戻ったときにその引数が null でないことが保証される、`ref` および `out` 引数に最も役立ちます。

無条件の事後条件は、次の属性を使用して指定します。

- [MaybeNull](xref:System.Diagnostics.CodeAnalysis.MaybeNullAttribute):null 非許容の戻り値は null である可能性があります。
- [NotNull](xref:System.Diagnostics.CodeAnalysis.NotNullAttribute):null 許容の戻り値が null になることはありません。

## <a name="specify-conditional-post-conditions-notnullwhen-maybenullwhen-and-notnullifnotnull"></a>条件付きの事後条件を指定する: `NotNullWhen`、`MaybeNullWhen`、および `NotNullIfNotNull`

`string` メソッド <xref:System.String.IsNullOrEmpty(System.String)?DisplayProperty=nameWithType> は見慣れたものかもしれません。 引数が null または空の文字列の場合、このメソッドから `true` が返されます。 これは、null チェックの形式です。メソッドから `false` が返された場合、呼び出し元で引数の null チェックを行う必要はありません。 この null 許容認識のようなメソッドを作成するには、引数を null 許容参照型に設定し、`NotNullWhen` 属性を追加します。

```csharp
bool IsNullOrEmpty([NotNullWhen(false)]string? value);
```

これにより、戻り値が `false` であるコードでは、null チェックを行う必要がないことがコンパイラに通知されます。 属性を追加すると、`IsNullOrEmpty` で必要な null チェックが実行されることがコンパイラの静的分析に通知されます。`false` が返された場合、入力引数は `null` ではありません。

```csharp
string? userInput = GetUserInput();
if (!string.IsNullOrEmpty(userInput))
{
   int messageLength = userInput.Length; // no null check needed.
}
// null check needed on userInput here.
```

.NET Core 3.0 の場合、上記のように <xref:System.String.IsNullOrEmpty(System.String)?DisplayProperty=nameWithType> メソッドに注釈が付けられます。 コードベースには、オブジェクトの状態で null 値をチェックする、同様のメソッドが存在する場合があります。 コンパイラではカスタムの null チェック メソッドが認識されないため、注釈を自分で追加する必要があります。 属性を追加すると、コンパイラの静的分析で、テストされた変数が null チェックされたかどうが認識されます。

これらの属性のもう 1 つの用途は、`Try*` パターンです。 `ref` および `out` 変数の事後条件は、戻り値を通じて伝達されます。 前述のこのメソッドについて考えてみます。

```csharp
bool TryGetMessage(string key, out string message)
```

上記のメソッドは、一般的な .NET 表現形式に従います。戻り値は、`message` が見つかった値に設定されているかどうか、またはメッセージが見つからない場合は、既定値に設定されているかどうかを示します。 メソッドから `true` が返された場合、`message` の値は null ではありません。それ以外の場合、メソッドでは `message` が null に設定されます。

`NotNullWhen` 属性を使用して、その表現方法を伝達することができます。 null 許容参照型のシグネチャを更新する場合は、`message` を `string?` にして、属性を追加します。

```csharp
bool TryGetMessage(string key, [NotNullWhen(true)] out string? message)
```

前述の例では、`TryGetMessage` から `true` が返された場合、`message` の値は null ではないと認識されます。 同じように、コードベースで同様のメソッドに注釈を付ける必要があります。引数は `null` である可能性があり、メソッドから `true` が返された場合は null ではないと認識されます。

最後にもう 1 つ属性があります。これも必要になる可能性があります。 戻り値の null 状態は、1 つまたは複数の入力引数の null 状態に依存する場合があります。 特定の入力引数が `null` でない場合は常に、これらのメソッドから null 以外の値が返されます。 これらのメソッドに正しく注釈を付けるには、`NotNullIfNotNull` 属性を使用します。 次のメソッドがあるとします。

```csharp
string GetTopLevelDomainFromFullUrl(string url);
```

`url` 引数が null でない場合、出力は `null` ではありません。 null 許容参照を有効にすると、API で null 入力が受け入れられることがない場合、そのシグネチャは正常に機能します。 しかし、入力が null である可能性がある場合は、戻り値も null である可能性があります。 したがって、シグネチャを次のコードに変更できます。

```csharp
string? GetTopLevelDomainFromFullUrl(string? url);
```

これも機能しますが、多くの場合、呼び出し元での追加の `null` チェックの実装が強制されます。 コントラクトは、入力引数 `url` が `null` である場合にのみ、戻り値が `null` になるというものです。 このコントラクトを表すには、次のコードに示すように、このメソッドに注釈を付けます。

```csharp
[return: NotNullIfNotNull("url")]
string? GetTopLevelDomainFromFullUrl(string? url);
```

戻り値と引数の両方に、`?` で注釈が付けられています。これは、どちらも `null` である可能性があることを示しています。 `url` 引数が `null` でない場合、属性によって、戻り値が null にならないことがさらに明確になります。

条件付きの事後条件は、これらの属性を使用して指定します。

- [MaybeNullWhen](xref:System.Diagnostics.CodeAnalysis.MaybeNullWhenAttribute):メソッドから指定された `bool` 値が返された場合、null 非許容の入力引数は null である可能性があります。
- [NotNullWhen](xref:System.Diagnostics.CodeAnalysis.NotNullWhenAttribute):メソッドから指定された `bool` 値が返された場合、null 許容の入力引数は null にはなりません。
- [NotNullIfNotNull](xref:System.Diagnostics.CodeAnalysis.NotNullIfNotNullAttribute):指定されたパラメーターの入力引数が null でない場合、戻り値は null ではありません。

## <a name="verify-unreachable-code"></a>到達できないコードを検証する

一部のメソッド (通常は例外ヘルパーまたはその他のユーティリティ メソッド) は、常に例外をスローすることによって終了します。 あるいは、ヘルパーでは、ブール型引数の値に基づいて、例外がスローされる場合があります。

最初のケースでは、メソッド宣言に `DoesNotReturn` 属性を追加できます。 コンパイラは、3 つの方法で役立ちます。 1 つ目では、例外をスローせずにメソッドを終了できるパスがある場合、コンパイラから警告が出されます。 2 つ目では、コンパイラによって、適切な `catch` 句が検出されるまで、そのメソッドの呼び出しの後にコードが "*到達できない*" ものとしてマークされます。 3 つ目では、到達できないコードが null 状態に影響することはありません。 たとえば、次のメソッドがあったとします。

```csharp
[DoesNotReturn]
private void FailFast()
{
   throw new InvalidOperationException();
}

public void SetState(object containedField)
{
   if (!isInitialized)
      FailFast();

   // unreachable code:
   this.field = containedField;
}
```

2 つ目のケースでは、メソッドのブール型パラメーターに `DoesNotReturnIf` 属性を追加します。 前の例は次のように変更できます。

```csharp
private void FailFast([DoesNotReturnIf(false)]bool isValid)
{
   if (!isValid)
       throw new InvalidOperationException();
}

public void SetState(object containedField)
{
   FailFast(isInitialized);

   // unreachable code when "isInitialized" is false:
   this.field = containedField;
}
```

## <a name="summary"></a>まとめ

null 許容参照型を追加すると、`null` である可能性のある変数に関する API の予測を記述するための、最初のボキャブラリが提供されます。 追加の属性では、変数の null 状態を事前条件および事後条件として記述するために、より豊富なボキャブラリが提供されます。 これらの属性では、予測をより明確に記述し、API を使用して開発者により優れたエクスペリエンスを提供します。

null 許容コンテキストのライブラリを更新する際には、API のユーザーに正しい使用方法を示すために、これらの属性を追加します。 これらの属性は、入力引数と戻り値の null 状態を完全に記述するのに役立ちます。

- [AllowNull](xref:System.Diagnostics.CodeAnalysis.AllowNullAttribute):null 非許容の入力引数を null にすることができます。
- [DisallowNull](xref:System.Diagnostics.CodeAnalysis.DisallowNullAttribute):null 許容の入力引数を null にすることはできません。
- [MaybeNull](xref:System.Diagnostics.CodeAnalysis.MaybeNullAttribute):null 非許容の戻り値は null である可能性があります。
- [NotNull](xref:System.Diagnostics.CodeAnalysis.NotNullAttribute):null 許容の戻り値が null になることはありません。
- [MaybeNullWhen](xref:System.Diagnostics.CodeAnalysis.MaybeNullWhenAttribute):メソッドから指定された `bool` 値が返された場合、null 非許容の入力引数は null である可能性があります。
- [NotNullWhen](xref:System.Diagnostics.CodeAnalysis.NotNullWhenAttribute):メソッドから指定された `bool` 値が返された場合、null 許容の入力引数は null にはなりません。
- [NotNullIfNotNull](xref:System.Diagnostics.CodeAnalysis.NotNullIfNotNullAttribute):指定されたパラメーターの入力引数が null でない場合、戻り値は null ではありません。
- [DoesNotReturn](xref:System.Diagnostics.CodeAnalysis.DoesNotReturnAttribute):メソッドから制御が返されることはありません。 つまり、常に例外がスローされます。
- [DoesNotReturnIf](xref:System.Diagnostics.CodeAnalysis.DoesNotReturnIfAttribute):関連付けられた `bool` パラメーターに指定された値がある場合、このメソッドから制御が返されることはありません。
