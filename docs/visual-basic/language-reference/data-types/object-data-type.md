---
title: Object Data Type
ms.date: 07/20/2015
f1_keywords:
- vb.Object
- vb.Variant
helpviewer_keywords:
- object variables [Visual Basic], Object type
- data types [Visual Basic], assigning
- Object data type
- Object data type [Visual Basic], reference
ms.assetid: 61ea4a7c-3b3d-48d4-adc4-eacfa91779b2
ms.openlocfilehash: 14770e74a0169dba3a45a04845dd32323e6201e3
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84415584"
---
# <a name="object-data-type"></a>Object Data Type

オブジェクトを参照するアドレスを保持します。 任意の参照型 (文字列、配列、クラス、またはインターフェイス) を `Object` 変数に割り当てることができます。 `Object` 変数は、任意の値の型 (数値、`Boolean`、`Char`、`Date`、構造体、または列挙型) のデータを参照することもできます。

## <a name="remarks"></a>Remarks

`Object` データ型は、アプリケーションで認識されるオブジェクト インスタンスなどの任意のデータ型のデータを指すことができます。 コンパイル時に変数が指す可能性のあるデータ型がわからない場合は、`Object` を使用します。

`Object` の既定値は `Nothing` (null 参照) です。

## <a name="data-types"></a>データの種類

任意のデータ型の変数、定数、または式を `Object` 変数に割り当てることができます。 `Object` 変数で現在参照されているデータ型を特定するには、<xref:System.Type?displayProperty=nameWithType> クラスの <xref:System.Type.GetTypeCode%2A> メソッドを使用できます。 次に例を示します。

```vb
Dim myObject As Object
' Suppose myObject has now had something assigned to it.
Dim datTyp As Integer
datTyp = Type.GetTypeCode(myObject.GetType())
```

`Object` データ型は参照型です。 ただし、Visual Basic では、値の型のデータを参照するときに、`Object` 変数が値型として扱われます。

## <a name="storage"></a>記憶域

参照先のデータ型にかかわらず、`Object` 変数にはデータ値自体は含まれませんが、値へのポインターが含まれます。 コンピューターのメモリでは常に 4 バイトが使用されますが、変数の値を表すデータの記憶域は含まれません。 コードではポインターを使用してデータが検索されるため、値の型を保持する `Object` 変数は、明示的に型指定された変数よりもアクセスが多少遅くなります。

## <a name="programming-tips"></a>プログラミングのヒント

- **相互運用の考慮事項。** オートメーション オブジェクトや COM オブジェクトのように、.NET Framework 向けに作成されていないコンポーネントとやり取りする場合、他の環境のポインター型は Visual Basic の `Object` 型と互換性がないことに注意してください。

- **パフォーマンス。** `Object` 型で宣言する変数は、任意のオブジェクトへの参照を格納するのに十分な柔軟性があります。 ただし、このような変数に対してメソッドまたはプロパティを呼び出すと、常に*遅延バインディング*が発生します (実行時)。 (コンパイル時の) *事前バインディング*を強制し、パフォーマンスを向上させるには、特定のクラス名を持つ変数を宣言するか、その変数を特定のデータ型にキャストします。

  オブジェクト変数を宣言するときは、一般化された `Object` 型ではなく、<xref:System.OperatingSystem> などの特定のクラス型を使用してみてください。 また、<xref:System.Windows.Forms.Control> ではなく <xref:System.Windows.Forms.TextBox> など、使用可能な最も具体的なクラスを使用して、そのプロパティとメソッドにアクセスできるようにする必要もあります。 通常、使用可能なクラス名を見つけるには、**オブジェクト ブラウザー**の **[クラス]** の一覧を使用できます。

- **拡大変換。** すべてのデータ型とすべての参照型は、`Object` データ型に拡大変換されます。 これは、<xref:System.OverflowException?displayProperty=nameWithType> エラーを発生させることなく、任意の型を `Object` に変換できることを意味します。

  ただし、値の型と `Object` の間で変換を行う場合、Visual Basic では*ボックス化*と*ボックス化解除*という操作が実行され、これにより実行速度が低下します。

- **型文字。** `Object` には、リテラルの型文字も識別子の型文字も含まれません。

- **Framework の型。** .NET Framework において対応する型は、<xref:System.Object?displayProperty=nameWithType> クラスです。

## <a name="example"></a>例

次の例は、オブジェクト インスタンスを指す `Object` 変数を示しています。

```vb
Dim objDb As Object
Dim myCollection As New Collection()
' Suppose myCollection has now been populated.
objDb = myCollection.Item(1)
```

## <a name="see-also"></a>関連項目

- <xref:System.Object>
- [データの種類](index.md)
- [データ型変換関数](../functions/type-conversion-functions.md)
- [変換の概要](../keywords/conversion-summary.md)
- [データ型の有効な使用方法](../../programming-guide/language-features/data-types/efficient-use-of-data-types.md)
- [方法: 2 つのオブジェクトが関連しているかどうかを判別する](../../programming-guide/language-features/variables/how-to-determine-whether-two-objects-are-related.md)
- [方法: 2 つのオブジェクトが同一であるかどうかを判別する](../../programming-guide/language-features/variables/how-to-determine-whether-two-objects-are-identical.md)
