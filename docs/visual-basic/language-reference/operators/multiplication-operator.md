---
title: '* 演算子'
ms.date: 07/20/2015
f1_keywords:
- vb.*
helpviewer_keywords:
- arithmetic operators [Visual Basic], multiplication
- operators [Visual Basic], multiplication
- '* operator [Visual Basic]'
- multiplication operator [Visual Basic], syntax
- math operators [Visual Basic]
ms.assetid: 2b210382-99da-4195-89ba-b1d06f5e89ad
ms.openlocfilehash: f1a7653fb3006ab3c9736ec168a8c5ea028f4763
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84409321"
---
# <a name="-operator-visual-basic"></a>* 演算子 (Visual Basic)
2 つの数値を乗算します。  
  
## <a name="syntax"></a>構文  
  
```vb  
number1 * number2  
```  
  
## <a name="parts"></a>指定項目  
  
|用語|定義|  
|---|---|  
|`number1`|必須です。 任意の数式。|  
|`number2`|必須です。 任意の数式。|  
  
## <a name="result"></a>結果  
 結果は `number1` と `number2` の積になります。  
  
## <a name="supported-types"></a>サポートされている型  
 すべての数値型。これには、符号なしおよび浮動小数点型と `Decimal` が含まれます。  
  
## <a name="remarks"></a>Remarks  
 結果のデータ型は、オペランドの型によって異なります。 次の表は、結果のデータ型がどのように決定されるかを示しています。  
  
|オペランドのデータ型|結果のデータ型|  
|---|---|  
|両方の式が整数データ型 ([SByte](../data-types/sbyte-data-type.md)、[Byte](../data-types/byte-data-type.md)、[Short](../data-types/short-data-type.md)、[UShort](../data-types/ushort-data-type.md)、[Integer](../data-types/integer-data-type.md)、[UInteger](../data-types/uinteger-data-type.md)、[Long](../data-types/long-data-type.md)、[ULong](../data-types/ulong-data-type.md))|`number1` と `number2` のデータ型に適した数値データ型。 「[演算子の結果のデータ型](data-types-of-operator-results.md)」の「整数演算」の表を参照してください。|  
|両方の式が [decimal](../data-types/decimal-data-type.md)|`Decimal`|  
|両方の式が [Single](../data-types/single-data-type.md)|`Single`|  
|一方の式が浮動小数点データ型 (`Single` または [Double](../data-types/double-data-type.md)) で、両方が `Single` ではない (`Decimal` は浮動小数点データ型ではないので注意してください)|`Double`|  
  
 式が [Nothing](../nothing.md) に評価される場合、0 として扱われます。  
  
## <a name="overloading"></a>オーバーロード  
 `*` 演算子は "*オーバーロード*" できます。つまり、オペランドがクラスまたは構造体の型を持っているときに、クラスまたは構造体はその動作を再定義できます。 コードで、そのようなクラスまたは構造体に対してこの演算子が使用される場合は、再定義された動作を理解していることを確認してください。 詳細については、「 [Operator Procedures](../../programming-guide/language-features/procedures/operator-procedures.md)」を参照してください。  
  
## <a name="example"></a>例  
 この例では、`*` 演算子を使用して 2 つの数値を乗算しています。 結果は 2 つのオペランドの積になります。  
  
 [!code-vb[VbVbalrOperators#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#4)]  
  
## <a name="see-also"></a>関連項目

- [*= 演算子](multiplication-assignment-operator.md)
- [算術演算子](arithmetic-operators.md)
- [Visual Basic における演算子の優先順位](operator-precedence.md)
- [機能別の演算子一覧](operators-listed-by-functionality.md)
- [Visual Basic における算術演算子](../../programming-guide/language-features/operators-and-expressions/arithmetic-operators.md)
