---
title: C# の予約済み属性:呼び出し元情報の追跡
ms.date: 04/09/2020
description: これらの属性を使用すると、メンバーを呼び出すコードに関する情報を生成するようにコンパイラに指示できます。 CallerFilePath、CallerLineNumber、および CallerMemberName を使用して、詳細なトレース情報を提供します。
ms.openlocfilehash: ee061d4cae35bdcc0b89007e360e94fee8c5f87c
ms.sourcegitcommit: c91110ef6ee3fedb591f3d628dc17739c4a7071e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/15/2020
ms.locfileid: "81389824"
---
# <a name="reserved-attributes-determine-caller-information"></a>予約済みの属性:呼び出し元情報を判断する

info 属性を使用して、メソッドの呼び出し元に関する情報を取得します。 ソース コードのファイル パス、ソース コードの行番号、呼び出し元のメンバー名を取得します。 メンバー呼び出し元情報を取得するには、省略可能なパラメーターに適用される属性を使用します。 省略可能な各パラメーターでは既定値が指定されます。 次の表は、<xref:System.Runtime.CompilerServices?displayProperty=nameWithType> 名前空間で定義されている呼び出し元情報の属性の一覧です。

|属性|説明|種類|
|---|---|---|
|<xref:System.Runtime.CompilerServices.CallerFilePathAttribute>|呼び出し元を含むソース ファイルのフル パスです。 完全なパスは、コンパイル時のパスです。|`String`|
|<xref:System.Runtime.CompilerServices.CallerLineNumberAttribute>|メソッドの呼び出し元であるソース ファイルの行番号。|`Integer`|
|<xref:System.Runtime.CompilerServices.CallerMemberNameAttribute>|呼び出し元のメソッド名またはプロパティ名。|`String`|

この情報は、トレースの作成、デバッグ、および診断ツールの作成に役立ちます。 呼び出し元情報の属性を使用する方法の例を次に示します。 `TraceMessage` メソッドを呼び出すたびに、呼び出し元情報は、省略可能なパラメーターの引数として設定されます。

```csharp
public void DoProcessing()
{
    TraceMessage("Something happened.");
}

public void TraceMessage(string message,
        [CallerMemberName] string memberName = "",
        [CallerFilePath] string sourceFilePath = "",
        [CallerLineNumber] int sourceLineNumber = 0)
{
    Trace.WriteLine("message: " + message);
    Trace.WriteLine("member name: " + memberName);
    Trace.WriteLine("source file path: " + sourceFilePath);
    Trace.WriteLine("source line number: " + sourceLineNumber);
}

// Sample Output:
//  message: Something happened.
//  member name: DoProcessing
//  source file path: c:\Visual Studio Projects\CallerInfoCS\CallerInfoCS\Form1.cs
//  source line number: 31
```

省略可能な各パラメーターには、明示的な既定値を指定します。 省略可能と指定されていないパラメーターには、呼び出し元情報の属性を適用できません。 呼び出し元情報の属性によってパラメーターが省略可能になるわけではありません。 この属性は、引数を省略したときに渡される既定値に影響します。 呼び出し元情報の値は、コンパイル時に中間言語 (IL) 内にリテラルとして出力されます。 例外の <xref:System.Exception.StackTrace%2A> プロパティの結果とは異なり、難読化による影響は受けません。 省略可能な引数を明示的に指定して、呼び出し元情報を制御したり、非表示にしたりできます。

### <a name="member-names"></a>メンバー名

`CallerMemberName` 属性を使用して、呼び出されたメソッドにメンバー名を `String` 引数として指定することを回避できます。 この方法を使用すると、**リファクタリングの名前の変更**で `String` 値が変更されないという問題が発生しなくなります。 この利点は、次のタスクで役立ちます。

- トレース ルーチンと診断ルーチンの使用。
- データ バインディング時の <xref:System.ComponentModel.INotifyPropertyChanged> インターフェイスの実装。 このインターフェイスを使用すると、オブジェクトのプロパティが、プロパティが変更されたことをデータ バインド コントロールに通知できます。これによって、このコントロールは、更新された情報を表示できます。 `CallerMemberName` 属性がない場合は、リテラルとしてプロパティ名を指定する必要があります。

次のグラフは、`CallerMemberName` 属性の使用時に返されるメンバー名を示します。

|呼び出しの発生元|メンバー名の結果|
|-|-|
|メソッド、プロパティ、またはイベント|呼び出しが発生したメソッド、プロパティ、またはイベントの名前。|
|コンストラクター|文字列「.ctor」|
|静的コンストラクター|文字列「.cctor」|
|デストラクターです。|文字列「Finalize」|
|ユーザー定義の演算子または変換|生成されたメンバー名 (「op_Addition」など)。|
|Attribute コンストラクター|属性が適用されるメソッドまたはプロパティの名前。 属性がメンバー内の要素 (パラメーター、戻り値、ジェネリック型パラメーターなど) である場合、この結果は、その要素に関連付けられているメンバーの名前になります。|
|含んでいないメンバー (型に適用されているアセンブリ レベルや属性など)|省略可能なパラメーターの既定値。|

## <a name="see-also"></a>関連項目

- [名前付き引数と省略可能な引数](../../programming-guide/classes-and-structs/named-and-optional-arguments.md)
- <xref:System.Reflection>
- <xref:System.Attribute>
- [属性](../../../standard/attributes/index.md)
