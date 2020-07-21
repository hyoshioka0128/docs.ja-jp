---
title: 暗黙の型変換と明示的な型変換
ms.date: 07/20/2015
helpviewer_keywords:
- conversions [Visual Basic], type
- variables [Visual Basic], changing data type
- casting
- conversions [Visual Basic], data type
- type conversion [Visual Basic], implicit conversions
- CType function [Visual Basic], conversions
- casting, data types
- data type conversion [Visual Basic], explicit
- type conversion [Visual Basic], explicit conversions
- data types [Visual Basic], casting
- conversions [Visual Basic], implicit
- explicit data type conversions [Visual Basic]
- conversions [Visual Basic]
- changing data types [Visual Basic]
- conversions [Visual Basic], explicit
- data type conversion [Visual Basic], implicit
- implicit data type conversions [Visual Basic]
ms.assetid: 77de1659-af8a-492c-967e-e7ef60ccce66
ms.openlocfilehash: 2858dafd2531bd846ad89672348d103f385c4511
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84393832"
---
# <a name="implicit-and-explicit-conversions-visual-basic"></a>暗黙の型変換と明示的な型変換 (Visual Basic)

"*暗黙の変換*" では、ソース コードに特別な構文は必要ありません。 次の例で、Visual Basic は、`k` の値を単精度浮動小数点値に暗黙的に変換してから、`q` に代入します。

```vb
Dim k As Integer
Dim q As Double
' Integer widens to Double, so you can do this with Option Strict On.
k = 432
q = k
```

"*明示的な変換*" では、型変換キーワードを使用します。 Visual Basic には、このようなキーワードがいくつか用意されており、これらを使用すると、かっこ内の式が目的のデータ型に強制的に変換されます。 これらのキーワードは関数と同様に機能しますが、コンパイラによってインラインでコードが生成されるため、関数呼び出しに比べて実行速度が若干速くなります。

次に示すのは前の例を拡張したものですが、`CInt` キーワードによって `q` の値が整数に変換された後で `k` に代入されます。

```vb
' q had been assigned the value 432 from k.
q = Math.Sqrt(q)
k = CInt(q)
' k now has the value 21 (rounded square root of 432).
```

## <a name="conversion-keywords"></a>変換キーワード

次の表に、使用可能な変換キーワードを示します。

|型変換キーワード|式の変換先のデータ型|変換可能な式のデータ型|
|---|---|---|
|`CBool`|[Boolean データ型](../../../language-reference/data-types/boolean-data-type.md)|任意の数値型 (`Byte`、`SByte`、列挙型など)、`String`、`Object`|
|`CByte`|[Byte データ型](../../../language-reference/data-types/byte-data-type.md)|任意の数値型 (`SByte` や列挙型など)、`Boolean`、`String`、`Object`|
|`CChar`|[Char データ型](../../../language-reference/data-types/char-data-type.md)|`String`、`Object`|
|`CDate`|[Date データ型](../../../language-reference/data-types/date-data-type.md)|`String`、`Object`|
|`CDbl`|[Double 型](../../../language-reference/data-types/double-data-type.md)|任意の数値型 (`Byte`、`SByte`、列挙型など)、`Boolean`、`String`、`Object`|
|`CDec`|[Decimal データ型](../../../language-reference/data-types/decimal-data-type.md)|任意の数値型 (`Byte`、`SByte`、列挙型など)、`Boolean`、`String`、`Object`|
|`CInt`|[Integer データ型](../../../language-reference/data-types/integer-data-type.md)|任意の数値型 (`Byte`、`SByte`、列挙型など)、`Boolean`、`String`、`Object`|
|`CLng`|[Long データ型](../../../language-reference/data-types/long-data-type.md)|任意の数値型 (`Byte`、`SByte`、列挙型など)、`Boolean`、`String`、`Object`|
|`CObj`|[Object 型](../../../language-reference/data-types/object-data-type.md)|任意の型|
|`CSByte`|[SByte データ型](../../../language-reference/data-types/sbyte-data-type.md)|任意の数値型 (`Byte` や列挙型など)、`Boolean`、`String`、`Object`|
|`CShort`|[Short データ型](../../../language-reference/data-types/short-data-type.md)|任意の数値型 (`Byte`、`SByte`、列挙型など)、`Boolean`、`String`、`Object`|
|`CSng`|[Single データ型](../../../language-reference/data-types/single-data-type.md)|任意の数値型 (`Byte`、`SByte`、列挙型など)、`Boolean`、`String`、`Object`|
|`CStr`|[String データ型](../../../language-reference/data-types/string-data-type.md)|任意の数値型 (`Byte`、`SByte`、列挙型など)、`Boolean`、`Char`、`Char` 配列、`Date`、`Object`|
|`CType`|コンマ (`,`) の後に指定される型|"*基本データ型*" (基本型の配列を含む) に変換するときは、対応する変換キーワードと同じ型が許可されます。<br /><br /> "*複合データ型*" に変換するときは、実装するインターフェイスと継承するクラス<br /><br /> `CType` をオーバーロードしたクラスまたは構造体に変換するときは、そのクラスまたは構造体|
|`CUInt`|[UInteger データ型](../../../language-reference/data-types/uinteger-data-type.md)|任意の数値型 (`Byte`、`SByte`、列挙型など)、`Boolean`、`String`、`Object`|
|`CULng`|[ULong データ型](../../../language-reference/data-types/ulong-data-type.md)|任意の数値型 (`Byte`、`SByte`、列挙型など)、`Boolean`、`String`、`Object`|
|`CUShort`|[UShort データ型](../../../language-reference/data-types/ushort-data-type.md)|任意の数値型 (`Byte`、`SByte`、列挙型など)、`Boolean`、`String`、`Object`|

## <a name="the-ctype-function"></a>CType 関数

[CType 関数](../../../language-reference/functions/ctype-function.md)は、2 つの引数に対して動作します。 1 つ目は変換される式、2 つ目は変換先のデータ型またはオブジェクト クラスです。 1 つ目の引数は型ではなく式である必要があることに注意してください。

`CType` は "*インライン関数*" です。つまり、多くの場合、関数呼び出しを生成せず、コンパイルされたコードが変換を行います。 これによってパフォーマンスも向上します。

`CType` と他の型変換キーワードとの比較については、「[DirectCast 演算子](../../../language-reference/operators/directcast-operator.md)」と「[TryCast 演算子](../../../language-reference/operators/trycast-operator.md)」を参照してください。

### <a name="elementary-types"></a>基本型

次の例は、`CType` の使い方を示しています。

```vb
k = CType(q, Integer)
' The following statement coerces w to the specific object class Label.
f = CType(w, Label)
```

### <a name="composite-types"></a>複合型

`CType` を使用すると、値を基本型だけでなく複合データ型にも変換できます。 また、これを使用して、次の例のように、オブジェクト クラスをそのインターフェイスの型の 1 つに強制的に変換することもできます。

```vb
' Assume class cZone implements interface iZone.
Dim h As Object
' The first argument to CType must be an expression, not a type.
Dim cZ As cZone
' The following statement coerces a cZone object to its interface iZone.
h = CType(cZ, iZone)
```

### <a name="array-types"></a>配列型

`CType` では、次の例のように配列データ型を変換することもできます。

```vb
Dim v() As classV
Dim obArray() As Object
' Assume some object array has been assigned to obArray.
' Check for run-time type compatibility.
If TypeOf obArray Is classV()
    ' obArray can be converted to classV.
    v = CType(obArray, classV())
End If
```

詳細および例については、「[配列の変換](array-conversions.md)」を参照してください。

### <a name="types-defining-ctype"></a>CType を定義する型

定義したクラスまたは構造体で `CType` を定義できます。 これにより、クラスまたは構造体の型との間で値を変換できるようになります。 詳細および使用例については、「[方法:変換演算子を定義する](../procedures/how-to-define-a-conversion-operator.md)」を参照してください。

> [!NOTE]
> 変換キーワードと共に使用する値は、変換先のデータ型で有効でなければなりません。そうでない場合、エラーが発生します。 たとえば、`Long` を `Integer` に変換しようとする場合、`Long` の値は `Integer` データ型の有効範囲内である必要があります。

> [!CAUTION]
> `CType` を指定した、あるクラス型から別のクラス型への変換が実行時に失敗するのは、変換元の型が変換先の型から派生されない場合です。 このような失敗では、<xref:System.InvalidCastException> 例外がスローされます。

ただし、型のいずれかが定義した構造体またはクラスであり、その構造体またはクラスに `CType` を定義している場合、それが `CType` の要件を満たすと変換が成功する可能性があります。 「[方法:変換演算子を定義する](../procedures/how-to-define-a-conversion-operator.md)」を参照してください。

明示的な変換の実行は、指定のデータ型またはオブジェクト クラスへの式の "*キャスト*" とも呼ばれます。

## <a name="see-also"></a>関連項目

- [Visual Basic における型変換](type-conversions.md)
- [文字列とその他の型との変換](conversions-between-strings-and-other-types.md)
- [方法: Visual Basic でオブジェクトを別の型に変換する](how-to-convert-an-object-to-another-type.md)
- [構造体](structures.md)
- [データの種類](../../../language-reference/data-types/index.md)
- [データ型変換関数](../../../language-reference/functions/type-conversion-functions.md)
- [トラブルシューティング (データ型)](troubleshooting-data-types.md)
