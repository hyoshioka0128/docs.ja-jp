---
title: '方法: 演算子プロシージャを呼び出す'
ms.date: 07/20/2015
helpviewer_keywords:
- operator procedures [Visual Basic], calling
- procedures [Visual Basic], operator
- procedure calls [Visual Basic], operator overloading
- syntax [Visual Basic], Operator procedures
- operators [Visual Basic], overloading
- return values [Visual Basic], Operator procedures
- overloaded operators [Visual Basic], calling
- operator overloading
ms.assetid: 0dce42cc-f0b0-4c14-9f62-018b21f33497
ms.openlocfilehash: fa2bc5417b8b917ff48502a5bd0a4daa21fab67e
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84388570"
---
# <a name="how-to-call-an-operator-procedure-visual-basic"></a>方法: 演算子プロシージャを呼び出す (Visual Basic)
演算子プロシージャは、式で演算子記号を使用して呼び出します。 変換演算子の場合は、[CType 関数](../../../language-reference/functions/ctype-function.md)を呼び出して、あるデータ型から別のデータ型に値を変換します。  
  
 演算子プロシージャを明示的に呼び出すことはありません。 演算子を通常使用する場合と同様に、代入ステートメントまたは式で、演算子または `CType` 関数を使用するだけです。 Visual Basic が演算子プロシージャを呼び出します。  
  
 クラスまたは構造体での演算子の定義は、演算子の "*オーバーロード*" とも呼ばれます。  
  
### <a name="to-call-an-operator-procedure"></a>演算子プロシージャを呼び出すには  
  
1. 通常どおり、式で演算子記号を使用します。  
  
2. オペランドのデータ型がその演算子に適しており、正しい順序であることを確認します。  
  
3. 演算子は想定どおりに式の値を返します。  
  
### <a name="to-call-a-conversion-operator-procedure"></a>変換演算子プロシージャを呼び出すには  
  
1. 式内で `CType` を使用します。  
  
2. オペランドのデータ型が変換に適しており、正しい順序であることを確認します。  
  
3. `CType` は変換演算子プロシージャを呼び出し、変換された値を返します。  
  
## <a name="example"></a>例  
 次の例では、2 つの <xref:System.TimeSpan> 構造体を作成し、それらを合計して、結果を 3 番目の <xref:System.TimeSpan> 構造体に格納します。 <xref:System.TimeSpan> 構造体では、複数の標準演算子をオーバーロードする演算子プロシージャを定義します。  
  
 [!code-vb[VbVbcnProcedures#29](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#29)]  
  
 <xref:System.TimeSpan> は標準の `+` 演算子をオーバーロードするため、前の例では `combinedSpan` の値を計算するときに演算子プロシージャを呼び出します。  
  
 会話演算子プロシージャの呼び出しの例については、「[方法: 演算子を定義するクラスを使用する](./how-to-use-a-class-that-defines-operators.md)」をご覧ください。  
  
## <a name="compile-the-code"></a>コードのコンパイル  
 使用しているクラスまたは構造体で、使用する演算子が定義されていることを確認します。  
  
## <a name="see-also"></a>関連項目

- [演算子プロシージャ](./operator-procedures.md)
- [方法: 演算子を定義する](./how-to-define-an-operator.md)
- [方法: 変換演算子を定義する](./how-to-define-a-conversion-operator.md)
- [Operator ステートメント](../../../language-reference/statements/operator-statement.md)
- [Widening](../../../language-reference/modifiers/widening.md)
- [Narrowing](../../../language-reference/modifiers/narrowing.md)
- [Structure ステートメント](../../../language-reference/statements/structure-statement.md)
- [方法: 構造体を宣言する](../data-types/how-to-declare-a-structure.md)
- [暗黙の型変換と明示的な型変換](../data-types/implicit-and-explicit-conversions.md)
- [拡大変換と縮小変換](../data-types/widening-and-narrowing-conversions.md)
