---
title: CType Function
ms.date: 07/20/2015
f1_keywords:
- vb.CType
helpviewer_keywords:
- expression conversion results
- explicit data type conversions [Visual Basic]
- CType function
- conversions [Visual Basic], expression
ms.assetid: dd4b29e7-6fa1-428c-877e-69955420bb72
ms.openlocfilehash: 88d609146648fe1b0c3124b99a65e85293fc0707
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84406431"
---
# <a name="ctype-function-visual-basic"></a>CType 関数 (Visual Basic)

任意の式を、指定されたデータ型、オブジェクト、構造体、クラス、またはインターフェイスに明示的に変換し、その結果を返します。

## <a name="syntax"></a>構文

```vb
CType(expression, typename)
```

## <a name="parts"></a>指定項目

`expression` 任意の有効な式。 `expression` の値が `typename` で許可されている範囲内でない場合、Visual Basic が例外をスローします。

`typename` `Dim` ステートメントの `As` 句内の有効な任意の式。つまり、任意のデータ型、オブジェクト、構造体、クラス、またはインターフェイスの名前。

## <a name="remarks"></a>Remarks

> [!TIP]
> 次の関数を使用して型変換を実行することもできます。
>
> - 特定のデータ型への変換を実行する、`CByte`、`CDbl`、`CInt` などの型変換関数。 詳細については、「 [データ型変換関数](type-conversion-functions.md)」を参照してください。
> - [DirectCast 演算子](../operators/directcast-operator.md)または [TryCast 演算子](../operators/trycast-operator.md)。 これらの演算子では、一方の型が他方の型を継承または実装している必要があります。 これらの場合は、`CType` データ型との間で変換を行うときに、`Object` よりもいくらかパフォーマンスが向上します。

`CType` は、インラインでコンパイルされます。つまり、変換コードは、式を評価するコードに含まれます。 場合によっては、変換を実行するプロシージャが呼び出されないため、コードの実行速度が速くなります。

`expression` から `typename` など、`Integer` から `Date` への変換が定義されていない場合、Visual Basic はコンパイル時のエラー メッセージを表示します。

実行時に変換が失敗すると、適切な例外がスローされます。 縮小変換が失敗した場合、最もよくスローされるのは <xref:System.OverflowException> です。 変換が定義されていない場合、<xref:System.InvalidCastException> がスローされます。 たとえば、これは、`expression` が `Object` 型で、実行時の型が `typename` への変換を持たない場合に起こります。

`expression` または `typename` のデータ型が、定義したクラスまたは構造体の場合、そのクラスまたは構造体に `CType` を変換演算子として定義できます。 これにより、`CType` は*オーバーロードされた演算子*として機能します。 この方法を利用する場合、定義したクラスまたは構造体からの変換、またはこのクラスまたは構造体への変換の動作 (スローする例外など) を制御できます。

## <a name="overloading"></a>オーバーロード

`CType` 演算子も、コードの外部で定義されたクラスまたは構造体でオーバーロードできます。 このようなクラスまたは構造体からの変換、またはこのクラスまたは構造体への変換を行う場合は、その `CType` 演算子の動作を確認してください。 詳細については、「 [Operator Procedures](../../programming-guide/language-features/procedures/operator-procedures.md)」を参照してください。

## <a name="converting-dynamic-objects"></a>動的オブジェクトの変換

動的オブジェクトの型変換は、<xref:System.Dynamic.DynamicObject.TryConvert%2A> メソッドまたは <xref:System.Dynamic.DynamicMetaObject.BindConvert%2A> メソッドを使用するユーザー定義の動的変換によって実行されます。 動的オブジェクトを使用する場合は、<xref:Microsoft.VisualBasic.Conversion.CTypeDynamic%2A> メソッドを使用して動的オブジェクトを変換します。

## <a name="example"></a>例

`CType` 関数を使用して任意の式を `Single` データ型に変換する例を次に示します。

[!code-vb[VbVbalrFunctions#24](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrFunctions/VB/Class1.vb#24)]

その他の例については、「[暗黙的な変換と明示的な変換](../../programming-guide/language-features/data-types/implicit-and-explicit-conversions.md)」を参照してください。

## <a name="see-also"></a>関連項目

- <xref:System.OverflowException>
- <xref:System.InvalidCastException>
- [データ型変換関数](type-conversion-functions.md)
- [変換関数](conversion-functions.md)
- [Operator ステートメント](../statements/operator-statement.md)
- [方法: 変換演算子を定義する](../../programming-guide/language-features/procedures/how-to-define-a-conversion-operator.md)
- [.NET Framework における型変換](../../../standard/base-types/type-conversion.md)
