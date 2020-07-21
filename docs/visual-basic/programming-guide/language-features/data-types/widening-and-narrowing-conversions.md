---
title: Widening and Narrowing Conversions
ms.date: 07/20/2015
helpviewer_keywords:
- widening conversions [Visual Basic]
- narrowing conversions [Visual Basic]
- conversions [Visual Basic], type
- data types [Visual Basic], changing
- variables [Visual Basic], changing data type
- conversions [Visual Basic], exceptions during conversion
- type conversion [Visual Basic], exceptions during conversion
- conversions [Visual Basic], data type
- conversions [Visual Basic], narrowing
- type conversion [Visual Basic], narrowing
- data type conversion [Visual Basic], widening
- data type conversion [Visual Basic], narrowing
- changing data types [Visual Basic]
- type conversion [Visual Basic], widening
- data type conversion [Visual Basic], exceptions during conversion
- conversions [Visual Basic], widening
ms.assetid: 058c3152-6c28-4268-af44-2209e774f0bd
ms.openlocfilehash: 177ff6c6fe15c57563d2f62ed8927f9ee975be48
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84393001"
---
# <a name="widening-and-narrowing-conversions-visual-basic"></a>拡大変換と縮小変換 (Visual Basic)
型変換に関する重要な考慮事項は、変換結果が変換先のデータ型の範囲内に収まるかどうかです。  
  
 "*拡大変換*" では、値が元のデータのあらゆる値を収容できるデータ型に変更されます。  拡大変換では変換元の値が保持されますが、その表現が変化する可能性があります。 そのようになるのは、整数型から `Decimal`、または `Char` から `String` に変換した場合です。  
  
 *縮小変換* により、有効値の一部を保持できない可能性のあるデータ型に値が変更されます。 たとえば、小数値を整数型に変換すると丸められます。また、`Boolean` に変換される数値型は `True` または `False` に縮小されます。  
  
## <a name="widening-conversions"></a>拡大変換  
 次の表は、標準の拡大変換を示しています。  
  
|データの種類|拡大変換先のデータ型<sup>1</sup>|  
|---|---|  
|[SByte](../../../language-reference/data-types/sbyte-data-type.md)|`SByte`, `Short`, `Integer`, `Long`, `Decimal`, `Single`, `Double`|  
|[Byte](../../../language-reference/data-types/byte-data-type.md)|`Byte`、`Short`、`UShort`、`Integer`、`UInteger`、`Long`、`ULong`、`Decimal`、`Single`、`Double`|  
|[Short](../../../language-reference/data-types/short-data-type.md)|`Short`, `Integer`, `Long`, `Decimal`, `Single`, `Double`|  
|[UShort](../../../language-reference/data-types/ushort-data-type.md)|`UShort`, `Integer`, `UInteger`, `Long`, `ULong`, `Decimal`, `Single`, `Double`|  
|[Integer](../../../language-reference/data-types/integer-data-type.md)|`Integer`、`Long`、`Decimal`、`Single`、`Double`<sup>2</sup>|  
|[UInteger](../../../language-reference/data-types/uinteger-data-type.md)|`UInteger`、`Long`、`ULong`、`Decimal`、`Single`、`Double`<sup>2</sup>|  
|[Long](../../../language-reference/data-types/long-data-type.md)|`Long`、`Decimal`、`Single`、`Double`<sup>2</sup>|  
|[ULong](../../../language-reference/data-types/ulong-data-type.md)|`ULong`、`Decimal`、`Single`、`Double`<sup>2</sup>|  
|[Decimal](../../../language-reference/data-types/decimal-data-type.md)|`Decimal`、`Single`、`Double`<sup>2</sup>|  
|[Single](../../../language-reference/data-types/single-data-type.md)|`Single`、`Double`|  
|[Double](../../../language-reference/data-types/double-data-type.md)|`Double`|  
|任意の列挙型 ([Enum](../../../language-reference/statements/enum-statement.md))|基になる整数型、および基になる型が拡大変換される任意の型。|  
|[Char](../../../language-reference/data-types/char-data-type.md)|`Char`、`String`|  
|`Char` 配列|`Char` 配列、`String`|  
|任意の型|[オブジェクト](../../../language-reference/data-types/object-data-type.md)|  
|任意の派生型|派生元の任意の基本型<sup>3</sup>|  
|任意の型|実装する任意のインターフェイス|  
|[Nothing](../../../language-reference/nothing.md)|任意のデータ型またはオブジェクト型|  
  
 <sup>1</sup> 定義により、すべてのデータ型がそれ自体に拡大変換されます。  
  
 <sup>2</sup> `Integer`、`UInteger`、`Long`、`ULong`、または `Decimal` から `Single` または `Double` への変換では、精度が失われることがありますが、大きさは失われません。 この意味で、情報の損失は発生しません。  
  
 <sup>3</sup> 派生型からその基本型の 1 つに変換することが拡大と見なされるのは意外かもしれません。 理由は、派生型には基本型のすべてのメンバーが含まれており、基本型のインスタンスとしての資格を満たすためです。 逆方向の場合、基本型には、派生型によって定義される新しいメンバーは含まれません。  
  
 拡大変換は実行時に必ず成功し、データの損失が発生することはありません。 [Option Strict ステートメント](../../../language-reference/statements/option-strict-statement.md)で、型チェック スイッチが `On` と `Off` のどちらに設定されていても、これらは常に暗黙で実行できます。  
  
## <a name="narrowing-conversions"></a>縮小変換  
 標準的な縮小変換には、次のようなものがあります。  
  
- 前の表に示した拡大変換の逆方向 (すべての型のそれ自体への拡大変換を除く)  
  
- [Boolean](../../../language-reference/data-types/boolean-data-type.md) と任意の数値型の間での双方向の変換  
  
- 任意の数値型から任意の列挙型 (`Enum`) への変換  
  
- [String](../../../language-reference/data-types/string-data-type.md) と、任意の数値型、`Boolean`、または [Date](../../../language-reference/data-types/date-data-type.md) の間での双方向の変換  
  
- データ型またはオブジェクト型から、派生元の型への変換  
  
 縮小変換は実行時に必ず成功するとは限らず、失敗したり、データの損失が発生したりする可能性があります。 エラーが発生するのは、変換先のデータ型が、変換された値を受け取ることができない場合です。 たとえば、数値変換でオーバーフローが発生する場合があります。 [Option Strict ステートメント](../../../language-reference/statements/option-strict-statement.md)で型チェック スイッチを `Off` に設定しない限り、縮小変換を暗黙に実行することはコンパイラによって許可されません。  
  
> [!NOTE]
> `For Each…Next` コレクション内の要素からループ制御変数への変換では、縮小変換エラーが抑制されます。 詳細と例については、「[For Each...Next ステートメント](../../../language-reference/statements/for-each-next-statement.md)」の縮小変換に関するセクションを参照してください。  
  
### <a name="when-to-use-narrowing-conversions"></a>縮小変換を使用する場合  
 縮小変換を使用するのは、変換元の値を変換先データ型に変換することができ、エラーやデータの損失が発生しないとわかっている場合です。 たとえば、"True" または "False" のいずれかが含まれていることがわかっている `String` がある場合、`CBool` キーワードを使用して `Boolean` に変換できます。  
  
## <a name="exceptions-during-conversion"></a>変換時の例外  
 拡大変換は常に成功するため、例外はスローされません。 縮小変換では、エラーが発生した場合によくスローされるのは次の例外です。  
  
- <xref:System.InvalidCastException> — 2 つの型の間に変換が定義されていない場合  
  
- <xref:System.OverflowException> — (整数型のみ) 変換後の値が、変換先の型に対して大きすぎる場合  
  
 クラスまたは構造体によって、そのクラスまたは構造体との間の変換演算子として使用される [CType 関数](../../../language-reference/functions/ctype-function.md)が定義されている場合、その `CType` によって該当する例外がスローされます。 また、この `CType` が Visual Basic 関数または .NET Framework メソッドを呼び出して、さらにさまざまな例外がスローされる可能性があります。  
  
## <a name="changes-during-reference-type-conversions"></a>参照型変換時の変更  
 "*参照型*" からの変換では、ポインターが値にコピーされるだけです。 値そのものがコピーされたり変更されたりすることはありません。 変更できるのは、ポインターを保持している変数のデータ型だけです。 次の例では、データ型は派生クラスから基本クラスに変換されますが、両方の変数が参照するオブジェクトは変更されません。  
  
```vb  
' Assume class cSquare inherits from class cShape.  
Dim shape As cShape  
Dim square As cSquare = New cSquare  
' The following statement performs a widening  
' conversion from a derived class to its base class.  
shape = square  
```  
  
## <a name="see-also"></a>関連項目

- [データの種類](index.md)
- [Visual Basic における型変換](type-conversions.md)
- [暗黙の型変換と明示的な型変換](implicit-and-explicit-conversions.md)
- [文字列とその他の型との変換](conversions-between-strings-and-other-types.md)
- [方法: Visual Basic でオブジェクトを別の型に変換する](how-to-convert-an-object-to-another-type.md)
- [配列変換](array-conversions.md)
- [データの種類](../../../language-reference/data-types/index.md)
- [データ型変換関数](../../../language-reference/functions/type-conversion-functions.md)
