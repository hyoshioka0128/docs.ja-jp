---
title: 1 次元配列 - C# プログラミング ガイド
ms.date: 06/03/2020
helpviewer_keywords:
- single-dimensional arrays [C#]
- arrays [C#], single-dimensional
ms.assetid: 2cec1196-1de0-49d2-baf2-c607c33310e8
ms.openlocfilehash: e189253eedc21fa2d51e16407f04b034610bb57b
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84410245"
---
# <a name="single-dimensional-arrays-c-programming-guide"></a>1 次元配列 (C# プログラミング ガイド)

配列要素の型と要素の数を指定する [new](../../language-reference/operators/new-operator.md) 演算子を使用して、1 次元配列を作成します。 次の例では、5 つの整数の配列を宣言しています。

:::code language="csharp" source="snippets/SingleDimensionArrays.cs" id="IntDeclaration":::

この配列は、`array[0]` から `array[4]` の要素を含んでいます。 配列の要素は、要素型の既定値である整数 `0` に初期化されます。

配列には、次の例のように、文字列の配列を宣言する、指定した要素型を格納できます。

:::code language="csharp" source="snippets/SingleDimensionArrays.cs" id="StringDeclaration":::

## <a name="array-initialization"></a>配列の初期化

配列を宣言するときに、配列の要素を初期化することができます。 長さ指定子は、初期化リスト内の要素の数から推論されるため、必要ではありません。 次に例を示します。

:::code language="csharp" source="snippets/SingleDimensionArrays.cs" id="IntInitialization":::

次のコードは、配列の各要素が曜日の名前で初期化される文字列配列の宣言を示しています。

:::code language="csharp" source="snippets/SingleDimensionArrays.cs" id="StringInitialization":::
  
次のコードに示すように、宣言時に配列を初期化するときに、`new` 式と配列型を回避することができます。 これは、[暗黙的に型指定される配列](implicitly-typed-arrays.md)と呼ばれます。

:::code language="csharp" source="snippets/SingleDimensionArrays.cs" id="ShorthandInitialization":::

配列変数は作成しなくても宣言できますが、この変数の新しい配列を割り当てるときは `new` 演算子を使用する必要があります。 次に例を示します。

:::code language="csharp" source="snippets/SingleDimensionArrays.cs" id="DeclareAllocate":::

## <a name="value-type-and-reference-type-arrays"></a>値の型と参照型の配列

次の配列の宣言を検討してみます。  

:::code language="csharp" source="snippets/SingleDimensionArrays.cs" id="FinalInstantiation":::

このステートメントの結果は、`SomeType` が値型か参照型かによって決まります。 値型の場合、ステートメントでは、それぞれに `SomeType` 型が含まれる 10 個の要素の配列が作成されます。 `SomeType` が参照型の場合、ステートメントは、それぞれが null 参照に初期化される 10 個の要素の配列を作成します。 両方のインスタンスで、要素は要素型の既定値に初期化されます。 値の型と参照型の詳細については、[値の型](../../language-reference/builtin-types/value-types.md)と[参照型](../../language-reference/keywords/reference-types.md)に関するページをご覧ください。
  
## <a name="see-also"></a>関連項目

- <xref:System.Array>
- [配列](./index.md)
- [多次元配列](./multidimensional-arrays.md)
- [ジャグ配列](./jagged-arrays.md)
