---
title: データの種類
ms.date: 07/20/2015
helpviewer_keywords:
- data types [Visual Basic], declaring
- typing
- data types [Visual Basic]
- Visual Basic code, data types
- data types [Visual Basic], improving speed with
ms.assetid: 5e1b9aaf-c7ca-4b29-9b22-0e82ed8e85e2
ms.openlocfilehash: 928d7fb6a40873641ae3e91e057c272b946a0091
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "85503781"
---
# <a name="data-types-in-visual-basic"></a>Visual Basic におけるデータ型
プログラミング要素の*データ型*は、保持できるデータの種類やデータの格納方法を示します。 データ型は、コンピューターのメモリに格納できるすべての値に適用され、式の評価にも関与します。 変数、リテラル、定数、列挙値、プロパティ、プロシージャのパラメーター、プロシージャの引数、およびプロシージャの戻り値にはすべてデータ型があります。  
  
## <a name="declared-data-types"></a>宣言済みデータ型  
 プログラミング要素は、宣言ステートメントで定義し、`As` 句を使用してデータ型を指定します。 次の表は、さまざまな要素の宣言に使用するステートメントを示しています。  
  
|プログラミング要素|データ型の宣言|  
|-------------------------|---------------------------|  
|変数|[Dim ステートメント](../../../language-reference/statements/dim-statement.md)<br /><br /> `Dim`   `amount As Double`<br /><br /> `Static`   `yourName As String`<br /><br /> `Public`   `billsPaid As Decimal = 0`|  
|Literal|リテラルの型文字で指定する場合は、「[Type Characters (型文字)](type-characters.md)」の「Literal Type Characters (リテラルの型文字)」を参照してください<br /><br /> `Dim searchChar As Char = "."`  `C`|  
|定数|[Const ステートメント](../../../language-reference/statements/const-statement.md)<br /><br /> `Const`   `modulus As Single = 4.17825F`|  
|列挙|[Enum ステートメント](../../../language-reference/statements/enum-statement.md)<br /><br /> `Public`   `Enum`   `colors`|  
|プロパティ|[Property ステートメント](../../../language-reference/statements/property-statement.md)<br /><br /> `Property`   `region() As String`|  
|プロシージャ パラメーター|[Sub ステートメント](../../../language-reference/statements/sub-statement.md)、[Function ステートメント](../../../language-reference/statements/function-statement.md)、または[Operator ステートメント](../../../language-reference/statements/operator-statement.md)<br /><br /> `Sub addSale(ByVal`   `amount`   `As Double)`|  
|プロシージャ引数|呼び出しコードの各引数は、すでに宣言されているプログラミング要素、または宣言されている要素を含む式です<br /><br /> `subString = Left(`  `inputString`  `,`   `5`  `)`|  
|プロシージャの戻り値|[Function ステートメント](../../../language-reference/statements/function-statement.md)、または[Operator ステートメント](../../../language-reference/statements/operator-statement.md)<br /><br /> `Function convert(ByVal b As Byte)`   `As String`|  
  
 Visual Basic のデータ型の一覧については、[データ型](../../../language-reference/data-types/index.md)に関するページをご覧ください。  
  
## <a name="see-also"></a>関連項目

- [型文字](type-characters.md)
- [基本データ型](elementary-data-types.md)
- [複合データ型](composite-data-types.md)
- [Generic Types in Visual Basic](generic-types.md)
- [Value Types and Reference Types](value-types-and-reference-types.md)
- [Visual Basic における型変換](type-conversions.md)
- [構造体](structures.md)
- [タプル](tuples.md)
- [トラブルシューティング (データ型)](troubleshooting-data-types.md)
- [データの種類](../../../language-reference/data-types/index.md)
- [データ型の有効な使用方法](efficient-use-of-data-types.md)
