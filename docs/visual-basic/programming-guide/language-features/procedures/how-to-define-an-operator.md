---
title: '方法: 演算子を定義する'
ms.date: 07/20/2015
helpviewer_keywords:
- procedures [Visual Basic], defining
- Visual Basic code, procedures
- operators [Visual Basic], defining
- procedures [Visual Basic], operator
- Visual Basic code, operators
- syntax [Visual Basic], Operator procedures
- operators [Visual Basic], overloading
- operator procedures [Visual Basic], about operator procedures
- return values [Visual Basic], Operator procedures
- operator overloading
ms.assetid: d4b0e253-092a-4e6e-9fe2-01f562140a29
ms.openlocfilehash: 49b9c8d1a6db56a56b50c16b4a6bb5b928df6c7d
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84388038"
---
# <a name="how-to-define-an-operator-visual-basic"></a>方法: 演算子を定義する (Visual Basic)
クラスまたは構造体を定義している場合、一方または両方のオペランドがクラスまたは構造体の型である場合の標準演算子 (`*`、`<>`、または `And` など) の動作を定義できます。  
  
 標準演算子をクラスまたは構造体内の演算子プロシージャとして定義します。 すべての演算子プロシージャは、`Public` `Shared` にする必要があります。  
  
 クラスまたは構造体での演算子の定義は、演算子の "*オーバーロード*" とも呼ばれます。  
  
## <a name="example"></a>例  
 次の例では、`height` という構造体の `+` 演算子を定義しています。 この構造体では、フィートとインチで計測された高さを使用します。 1 "*インチ*" は 2.54 センチメートルであり、1 "*フィート*" は 12 インチです。 正規化された値 (インチ < 12.0) を確保するために、コンストラクターでは "*剰余*" 12 演算が実行されます。 `+` 演算子では、コンストラクターを使用して正規化された値が生成されます。  
  
 [!code-vb[VbVbcnProcedures#25](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#25)]  
  
 次のコードで構造体 `height` をテストできます。  
  
 [!code-vb[VbVbcnProcedures#26](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#26)]  

## <a name="see-also"></a>関連項目

- [演算子プロシージャ](./operator-procedures.md)
- [方法: 変換演算子を定義する](./how-to-define-a-conversion-operator.md)
- [方法: 演算子プロシージャを呼び出す](./how-to-call-an-operator-procedure.md)
- [方法: 演算子を定義するクラスを使用する](./how-to-use-a-class-that-defines-operators.md)
- [Operator ステートメント](../../../language-reference/statements/operator-statement.md)
- [Structure ステートメント](../../../language-reference/statements/structure-statement.md)
- [方法: 構造体を宣言する](../data-types/how-to-declare-a-structure.md)
- [Mod 演算子](../../../language-reference/operators/mod-operator.md)
