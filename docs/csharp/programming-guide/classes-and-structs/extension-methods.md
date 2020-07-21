---
title: 拡張メソッド - C# プログラミング ガイド
ms.date: 03/19/2020
helpviewer_keywords:
- methods [C#], adding to existing types
- extension methods [C#]
- methods [C#], extension
ms.assetid: 175ce3ff-9bbf-4e64-8421-faeb81a0bb51
ms.openlocfilehash: 0f9c0f053e531a44640084a35dc5d8e844ee0b46
ms.sourcegitcommit: 1eae045421d9ea2bfc82aaccfa5b1ff1b8c9e0e4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/16/2020
ms.locfileid: "84803182"
---
# <a name="extension-methods-c-programming-guide"></a>拡張メソッド (C# プログラミング ガイド)

拡張メソッドを使用すると、新規の派生型の作成、再コンパイル、または元の型の変更を行うことなく既存の型にメソッドを "追加" できます。 拡張メソッドは静的メソッドですが、拡張された型のインスタンス メソッドのように呼び出します。 C#、F#、Visual Basic で作成されたクライアント コードの場合は、拡張メソッドの呼び出しと、型で定義されているメソッドの呼び出しに明確な違いはありません。

最も一般的な拡張メソッドは、既存の <xref:System.Collections.IEnumerable?displayProperty=nameWithType> 型および <xref:System.Collections.Generic.IEnumerable%601?displayProperty=nameWithType> 型にクエリ機能を追加する LINQ 標準クエリ演算子です。 この標準クエリ演算子を使用するには、まず `using System.Linq` ディレクティブを使用して、スコープに含めます。 <xref:System.Collections.Generic.IEnumerable%601> を実装するすべての型は、<xref:System.Linq.Enumerable.GroupBy%2A>、<xref:System.Linq.Enumerable.OrderBy%2A>、<xref:System.Linq.Enumerable.Average%2A> などのインスタンス メソッドを持っていると考えられます。 <xref:System.Collections.Generic.List%601>、<xref:System.Array> などの <xref:System.Collections.Generic.IEnumerable%601> 型のインスタンスの後に "ドット" を入力すると、IntelliSense により、ステートメントの入力候補としてこれらの追加メソッドが表示されます。

### <a name="orderby-example"></a>OrderBy の例

整数の配列において、標準クエリ演算子の `OrderBy` メソッドを呼び出す方法を次の例に示します。 かっこ内の式はラムダ式です。 標準クエリ演算子の多くはパラメーターとしてラムダ式を受け取りますが、拡張メソッドでは、これは必須ではありません。 詳細については、「[ラムダ式](../statements-expressions-operators/lambda-expressions.md)」を参照してください。

[!code-csharp[csProgGuideExtensionMethods#3](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideExtensionMethods/cs/extensionmethods.cs#3)]

拡張メソッドは、静的メソッドとして定義しますが、インスタンス メソッドの構文を使用して呼び出します。 最初のパラメーターでは、メソッドによって操作される型を指定します。 このパラメーターの前には [this](../../language-reference/keywords/this.md) 修飾子を付けます。 `using` ディレクティブを使用して名前空間をソース コードに明示的にインポートした場合、拡張メソッドはそのスコープでのみ有効です。

<xref:System.String?displayProperty=nameWithType> クラスに対して拡張メソッドを定義する例を次に示します。 入れ子になっていない、非ジェネリックの静的クラス内で定義されています。

[!code-csharp[csProgGuideExtensionMethods#4](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideExtensionMethods/cs/extensionmethods.cs#4)]

この `WordCount` ディレクティブを使用することで、`using` 拡張メソッドをスコープに取り込むことができます。

```csharp
using ExtensionMethods;
```

また、この構文を使用することで、アプリケーションから呼び出すことができます。

```csharp
string s = "Hello Extension Methods";
int i = s.WordCount();
```

コードでは、インスタンス メソッドの構文を使用して、拡張メソッドを呼び出します。 コンパイラによって生成される中間言語 (IL) により、コードは静的メソッドの呼び出しに変換されます。 カプセル化の原則には実質的に違反していません。 拡張メソッドでは、それが拡張している型のプライベート変数にはアクセスできません。

詳細については、「[カスタム拡張メソッドを実装して呼び出す方法](./how-to-implement-and-call-a-custom-extension-method.md)」を参照してください。

一般に、独自に実装するより、拡張メソッドを呼び出す方がはるかに多くなると思われます。 拡張メソッドは、インスタンス メソッドの構文を使用して呼び出すので、特別な知識がなくてもクライアント コードからそれらを使用できます。 メソッドが定義されている名前空間に関する `using` ディレクティブを追加するだけで、特定の型の拡張メソッドを使用できるようになります。 たとえば、標準クエリ演算子を使用するには、次の `using` ディレクティブをコードに追加します。

```csharp
using System.Linq;
```

場合によっては、System.Core.dll への参照も追加する必要があります。ほとんどの <xref:System.Collections.Generic.IEnumerable%601> 型で利用できる追加メソッドとして、標準クエリ演算子が IntelliSense に表示されるようになりました。

## <a name="binding-extension-methods-at-compile-time"></a>コンパイル時の拡張メソッドのバインディング

拡張メソッドを使用してクラスまたはインターフェイスを拡張することはできますが、これらをオーバーライドすることはできません。 インターフェイス メソッドまたはクラス メソッドと同じ名前およびシグネチャを持つ拡張メソッドは決して呼び出されません。 コンパイル時に、型自体で定義されているインスタンス メソッドよりも低い優先順位が拡張メソッドには必ず設定されます。 つまり、型に `Process(int i)` という名前のメソッドがあり、これと同じシグネチャの拡張メソッドがある場合、コンパイラは必ずインスタンス メソッドにバインドします。 コンパイラは、メソッド呼び出しを検出すると、最初に型のインスタンス メソッドから一致するものを探します。 一致するものが見つからない場合、型に対して定義されている拡張メソッドを検索し、見つかった最初の拡張メソッドにバインドします。 次の例は、コンパイラが拡張メソッドとインスタンス メソッドのどちらにバインドするかを決定する方法を示しています。

## <a name="example"></a>例

次の例は、C# のコンパイラがメソッド呼び出しを型のインスタンス メソッドにバインドするか、拡張メソッドにバインドするかを決定するときに従う規則を示しています。 `Extensions` 静的クラスには、`IMyInterface` を実装する型に対して定義された拡張メソッドが含まれています。 `A`、`B`、および `C` の各クラスはすべてこのインターフェイスを実装しています。

`MethodB` 拡張メソッドは、その名前とシグネチャがクラスにより既に実装されているメソッドと完全に一致しているため、呼び出されることはありません。

コンパイラは、一致するシグネチャを持つインスタンス メソッドを検出できない場合、一致する拡張メソッドが存在する場合はそれにバインドします。

[!code-csharp[csProgGuideExtensionMethods#5](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideExtensionMethods/cs/extensionmethods.cs#5)]

## <a name="common-usage-patterns"></a>一般的な使用パターン

### <a name="collection-functionality"></a>コレクションの機能

これまでは、特定の型の <xref:System.Collections.Generic.IEnumerable%601?displayProperty=nameWithType> インターフェイスが実装され、その型のコレクションに対して動作する機能が含まれている、"コレクション クラス" を作成するのが一般的でした。 この種類のコレクション オブジェクトを作成しても問題はありませんが、<xref:System.Collections.Generic.IEnumerable%601?displayProperty=nameWithType> の拡張機能を使用して同じ機能を実現できます。 拡張機能には、その型の <xref:System.Collections.Generic.IEnumerable%601?displayProperty=nameWithType> が実装されている <xref:System.Array?displayProperty=nameWithType> や <xref:System.Collections.Generic.List%601?displayProperty=nameWithType> などの任意のコレクションから機能を呼び出すことができるという利点があります。 Int32 の配列のこの使用例については、[この記事で既に](#orderby-example)示されています。

### <a name="layer-specific-functionality"></a>レイヤー固有の機能

オニオン アーキテクチャまたは他のレイヤー化アプリケーション設計を使用する場合は、アプリケーションの境界を越えて通信するために使用できるドメイン エンティティまたはデータ転送オブジェクトのセットを使用するのが一般的です。 これらのオブジェクトには、通常、機能が含まれていないか、またはアプリケーションのすべてのレイヤーに適用される最小限の機能のみが含まれています。 他のレイヤーで必要のないメソッドや望ましくないメソッドを使用してオブジェクトを読み込むことなしに、拡張メソッドを使用して、各アプリケーション レイヤーに固有の機能を追加することができます。

```csharp
public class DomainEntity
{
    public int Id { get; set; }
    public string FirstName { get; set; }
    public string LastName { get; set; }
}

static class DomainEntityExtensions
{
    static string FullName(this DomainEntity value)
        => $"{value.FirstName} {value.LastName}";
}
```

### <a name="extending-predefined-types"></a>定義済みの型の拡張

再利用可能な機能を作成する必要があるときに、新しいオブジェクトを作成するのではなく、多くの場合、.NET や CLR 型などの既存の型を拡張できます。 たとえば、拡張メソッドを使用しない場合は、コード内の複数の場所から呼び出すことができる `Engine` または `Query` クラスを作成して、SQL サーバーに対するクエリの実行を処理することが考えられます。 一方、代わりに拡張メソッドを使用して <xref:System.Data.SqlClient.SqlConnection?displayProperty=nameWithType> クラスを拡張すると、SQL サーバーに接続している任意の場所からそのクエリを実行することができます。 他の例としては、<xref:System.String?displayProperty=nameWithType> クラスへの共通機能の追加、<xref:System.IO.File?displayProperty=nameWithType> および <xref:System.IO.Stream?displayProperty=nameWithType> オブジェクトのデータ処理機能の拡張、特定のエラー処理機能のための <xref:System.Exception?displayProperty=nameWithType> オブジェクトなどがあります。 この種のユース ケースは、開発者の想像力と良識によってのみ制限されます。

`struct` 型は、メソッドに値で渡されるため、定義済みの型を拡張するのが難かしい場合があります。 これは、構造体への変更が構造体のコピーに対して行われることを意味します。 そのような変更は、拡張メソッドが終了した後では認識できません。 C# 7.2 以降では、拡張メソッドの最初の引数に `ref` 修飾子を追加できます。 `ref` 修飾子を追加すると、最初の引数が参照によって渡されます。 これにより、拡張されている構造体の状態を変更する拡張メソッドを記述できます。

## <a name="general-guidelines"></a>一般的なガイドライン

オブジェクトのコードを変更したり新しい型を派生させたりすることによって機能を追加することが妥当かつ可能である場合は、そのようにすることがやはり推奨されますが、.NET エコシステムの全体で、拡張メソッドが再利用可能な機能を作成するための重要なオプションになってきています。 元のソースを制御できない場合、派生オブジェクトが不適切または不可能な場合、または該当するスコープを超えて機能を公開してはならない場合は、拡張メソッドが優れた選択肢になります。

派生型について詳しくは、「[継承](./inheritance.md)」をご覧ください。

ソース コードを制御できない型を、拡張メソッドを使用して拡張すると、型の実装の変更により拡張メソッドが破損するというリスクを負うことになります。

所定の型の拡張メソッドを実装する場合、次の点に注意してください。

- 拡張メソッドが型で定義されているメソッドと同じシグネチャを持つ場合、その拡張メソッドは呼び出されません。
- 拡張メソッドは名前空間レベルでスコープ内に取り込まれます。 たとえば、`Extensions` という名前の単一の名前空間に、拡張メソッドを含む複数の静的クラスがある場合、`using Extensions;` ディレクティブによって、それらのすべての拡張メソッドがスコープ内に取り込まれます。

実装したクラス ライブラリでは、アセンブリのバージョン番号のインクリメントを避けるために、拡張メソッドは使用しないでください。 ソース コードを所有するライブラリに重要な機能を追加する場合は、アセンブリのバージョン管理について、.NET ガイドラインに従う必要があります。 詳細については、「[アセンブリのバージョン管理](../../../standard/assembly/versioning.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [C# プログラミング ガイド](../index.md)
- [並列プログラミングのサンプル (拡張メソッドの例が多数掲載されています)](/samples/browse/?products=dotnet-core%2Cdotnet-standard&term=parallel)
- [ラムダ式](../statements-expressions-operators/lambda-expressions.md)
- [標準クエリ演算子の概要](../concepts/linq/standard-query-operators-overview.md)
- [インスタンス パラメーターの変換規則とその影響](https://docs.microsoft.com/archive/blogs/sreekarc/conversion-rules-for-instance-parameters-and-their-impact)
- [拡張メソッドの言語間での相互運用性](https://docs.microsoft.com/archive/blogs/sreekarc/extension-methods-interoperability-between-languages)
- [拡張メソッドとカリー化デリゲート](https://docs.microsoft.com/archive/blogs/sreekarc/extension-methods-and-curried-delegates)
- [バインディングとエラー報告に関する拡張メソッド](https://docs.microsoft.com/archive/blogs/sreekarc/extension-method-binding-and-error-reporting)
