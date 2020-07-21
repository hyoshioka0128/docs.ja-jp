---
title: <<= 演算子
ms.date: 07/20/2015
f1_keywords:
- vb.<<=
helpviewer_keywords:
- operator <<=
- assignment statements [Visual Basic], compound
- <<= operator [Visual Basic]
- statements [Visual Basic], compound assignment
- operator<<=
- compound assignment statements [Visual Basic]
ms.assetid: 8ad26613-faff-4e2f-89ee-63feee33bfda
ms.openlocfilehash: ff7cbb02a9a10dbe11450491e93fd85fd77b44ba
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84370662"
---
# <a name="-operator-visual-basic"></a>\<\<= 演算子 (Visual Basic)
変数またはプロパティの値に算術左シフトを実行し、結果をその変数またはプロパティに戻して代入します。  
  
## <a name="syntax"></a>構文  
  
```vb  
variableorproperty <<= amount  
```  
  
## <a name="parts"></a>指定項目  
 `variableorproperty`  
 必須です。 整数型の変数またはプロパティ (`SByte`、`Byte`、`Short`、`UShort`、`Integer`、`UInteger`、`Long`、`ULong`)。  
  
 `amount`  
 必須です。 `Integer` に拡大されるデータ型の数値式。  
  
## <a name="remarks"></a>Remarks  
 `<<=` 演算子の左側の要素には、単純なスカラー変数、プロパティ、または配列の要素を指定できます。 変数またはプロパティを [ReadOnly](../modifiers/readonly.md) にすることはできません。  
  
 `<<=` 演算子は、まず変数またはプロパティの値に対して算術左シフトを実行します。 次に、この演算子はその演算の結果をその変数またはプロパティに戻して代入します。  
  
 算術シフトは循環ではありません。つまり、結果の一方の端からシフトされたビットはもう一方の端には再入されません。 算術左シフトでは、結果のデータ型の範囲を超えてシフトされたビットは破棄され、右側に空いたビット位置は 0 に設定されます。  
  
## <a name="overloading"></a>オーバーロード  
 [<< 演算子](left-shift-operator.md)は "*オーバーロード*" できます。つまり、オペランドがあるクラスまたは構造体の型を持っているときに、そのクラスまたは構造体がその動作を再定義できます。 `<<` 演算子をオーバーロードすると、`<<=` 演算子の動作に影響します。 コードで、`<<` をオーバーロードするクラスまたは構造体で `<<=` を使用する場合は、再定義された動作を理解していることを確認してください。 詳細については、「 [Operator Procedures](../../programming-guide/language-features/procedures/operator-procedures.md)」を参照してください。  
  
## <a name="example"></a>例  
 次の例では、`<<=` 演算子を使用して、`Integer` 変数のビット パターンを、指定された桁数だけ左にシフトし、結果をその変数に代入します。  
  
 [!code-vb[VbVbalrOperators#13](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#13)]  
  
## <a name="see-also"></a>関連項目

- [<< 演算子](left-shift-operator.md)
- [代入演算子](assignment-operators.md)
- [ビット シフト演算子](bit-shift-operators.md)
- [Visual Basic における演算子の優先順位](operator-precedence.md)
- [機能別の演算子一覧](operators-listed-by-functionality.md)
- [ステートメント](../../programming-guide/language-features/statements.md)
