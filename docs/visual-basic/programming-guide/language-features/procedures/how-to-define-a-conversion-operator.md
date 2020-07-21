---
title: '方法: 変換演算子を定義する'
ms.date: 07/20/2015
helpviewer_keywords:
- procedures [Visual Basic], defining
- operators [Visual Basic], defining
- procedures [Visual Basic], operator
- operators [Visual Basic], overloading
- return values [Visual Basic], Operator procedures
- operator overloading
ms.assetid: 54203dfa-c24b-463f-9942-d5153e89e762
ms.openlocfilehash: 53b0211c6304625edd7ac24fa52ff0c051d8f0a0
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84388090"
---
# <a name="how-to-define-a-conversion-operator-visual-basic"></a>方法: 変換演算子を定義する (Visual Basic)
クラスまたは構造体を定義している場合は、クラスまたは構造体の型と別のデータ型 (`Integer`、`Double`、`String` など) の間の型変換演算子を定義できます。  
  
 型変換をクラスまたは構造体内の [CType 関数](../../../language-reference/functions/ctype-function.md)プロシージャとして定義します。 すべての変換プロシージャは `Public Shared` である必要があります。また、それぞれ [Widening](../../../language-reference/modifiers/widening.md) または [Narrowing](../../../language-reference/modifiers/narrowing.md) を指定する必要があります。  
  
 クラスまたは構造体での演算子の定義は、演算子の "*オーバーロード*" とも呼ばれます。  
  
## <a name="example"></a>例  
 次の例では、`digit` という構造体と `Byte` の間の変換演算子を定義しています。  
  
 [!code-vb[VbVbcnProcedures#27](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#27)]  
  
 次のコードで構造体 `digit` をテストできます。  
  
 [!code-vb[VbVbcnProcedures#28](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#28)]  
  
## <a name="see-also"></a>関連項目

- [演算子プロシージャ](./operator-procedures.md)
- [方法: 演算子を定義する](./how-to-define-an-operator.md)
- [方法: 演算子プロシージャを呼び出す](./how-to-call-an-operator-procedure.md)
- [方法: 演算子を定義するクラスを使用する](./how-to-use-a-class-that-defines-operators.md)
- [Operator ステートメント](../../../language-reference/statements/operator-statement.md)
- [Structure ステートメント](../../../language-reference/statements/structure-statement.md)
- [方法: 構造体を宣言する](../data-types/how-to-declare-a-structure.md)
- [暗黙の型変換と明示的な型変換](../data-types/implicit-and-explicit-conversions.md)
- [拡大変換と縮小変換](../data-types/widening-and-narrowing-conversions.md)
