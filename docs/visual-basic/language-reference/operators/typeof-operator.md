---
title: TypeOf 演算子
ms.date: 07/20/2015
f1_keywords:
- TypeOf
- vb.TypeOf
helpviewer_keywords:
- types [Visual Basic], compatible
- comparison operators [Visual Basic]
- TypeOf...Is expression
- data types [Visual Basic], compatible
- TypeOf operator [Visual Basic]
- compatible data types [Visual Basic]
ms.assetid: 33f65296-659a-4b9a-9a29-c2a91cff68b2
ms.openlocfilehash: 0cce36073b53442bce63f966f3bd94bd5d70d2a8
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84406328"
---
# <a name="typeof-operator-visual-basic"></a>TypeOf 演算子 (Visual Basic)
式の結果の実行時の型に、指定された型との型互換性があるかどうかを確認します。
  
## <a name="syntax"></a>構文  
  
```vb  
result = TypeOf objectexpression Is typename  
```  
  
```vb  
result = TypeOf objectexpression IsNot typename  
```  
  
## <a name="parts"></a>指定項目  
 `result`  
 必須。 `Boolean` 値。  
  
 `objectexpression`  
 必須です。 参照型に評価される任意の式。  
  
 `typename`  
 必須です。 任意のデータ型名。  
  
## <a name="remarks"></a>Remarks  
 `TypeOf` 演算子は、`objectexpression` の実行時の型が `typename` と互換性があるかどうかを調べます。 互換性は、`typename` の型のカテゴリに依存します。 互換性を決定する方法を次の表に示します。  
  
|`typename` の型のカテゴリ|互換性の条件|  
|---------------------------------|-----------------------------|  
|クラス|`objectexpression` が `typename` 型である、または `typename` を継承する|  
|構造体|`objectexpression` が `typename` 型である|  
|Interface|`objectexpression` が `typename` を実装する、または `typename` を実装するクラスを継承する|  
  
 `objectexpression` の実行時の型が互換性の条件を満たす場合、`result` は `True` です。 それ以外の場合、`result` は `False` です。  `objectexpression` が null の場合、`TypeOf`...`Is` は `False` を返し、...`IsNot` は `True` を返します。  
  
 `TypeOf` は、常に `Is` キーワードと共に `TypeOf`...`Is` 式を構築するか、または `IsNot` キーワードと共に `TypeOf`...`IsNot` 式を構築します。  
  
## <a name="example"></a>例  
 次の例では、`TypeOf`...`Is` 式でさまざまなデータ型を使用して、2 つのオブジェクト参照変数の型の互換性をテストしています。  
  
 [!code-vb[VbVbalrOperators#39](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#39)]  
  
 変数 `refInteger` は、実行時の型 `Integer` を持ちます。 `Integer` と互換性がありますが、`Double` との互換性はありません。 変数 `refForm` は、実行時の型 <xref:System.Windows.Forms.Form> を持ちます。 この変数は、<xref:System.Windows.Forms.Form> (同じ型)、<xref:System.Windows.Forms.Control> (<xref:System.Windows.Forms.Form> は <xref:System.Windows.Forms.Control> を継承する)、および <xref:System.ComponentModel.IComponent> (<xref:System.Windows.Forms.Form> は <xref:System.ComponentModel.IComponent> を実装する <xref:System.ComponentModel.Component> を継承する) と互換性があります。 ただし、`refForm` には <xref:System.Windows.Forms.Label> との互換性はありません。  
  
## <a name="see-also"></a>関連項目

- [Is 演算子](is-operator.md)
- [IsNot 演算子](isnot-operator.md)
- [Visual Basic における比較演算子](../../programming-guide/language-features/operators-and-expressions/comparison-operators.md)
- [Visual Basic における演算子の優先順位](operator-precedence.md)
- [機能別の演算子一覧](operators-listed-by-functionality.md)
- [演算子および式](../../programming-guide/language-features/operators-and-expressions/index.md)
