---
title: '方法: 演算子を定義するクラスを使用する'
ms.date: 07/20/2015
helpviewer_keywords:
- operator procedures [Visual Basic], calling
- procedures [Visual Basic], operator
- procedures [Visual Basic], calling
- examples [Visual Basic], CType
- syntax [Visual Basic], Operator procedures
- operators [Visual Basic], overloading
- return values [Visual Basic], Operator procedures
- operator overloading
ms.assetid: 7ccce94a-6ca0-47d1-9f3f-13385d34f5d5
ms.openlocfilehash: fe15e976e6a5469f2a9d1b3521a70a3e1860fdd3
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84414351"
---
# <a name="how-to-use-a-class-that-defines-operators-visual-basic"></a>方法: 演算子を定義するクラスを使用する (Visual Basic)
独自の演算子が定義されているクラスまたは構造体を使用する場合、Visual Basic からそれらの演算子にアクセスできます。  
  
 クラスまたは構造体での演算子の定義は、演算子の "*オーバーロード*" とも呼ばれます。  
  
## <a name="example"></a>例  
 次の例では、SQL 文字列と Visual Basic 文字列の間の双方向の変換演算子 ([CType 関数](../../../language-reference/functions/ctype-function.md)) が定義されている、SQL 構造体 <xref:System.Data.SqlTypes.SqlString> にアクセスします。 `CType(`*SQL 文字列式*, `String)` を使用して SQL 文字列を Visual Basic 文字列に変換し、`CType(`*Visual Basic 文字列式*, <xref:System.Data.SqlTypes.SqlString>`)` を使用して逆方向に変換します。  
  
 [!code-vb[VbVbcnProcedures#30](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#30)]  
  
 [!code-vb[VbVbcnProcedures#31](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#31)]  
  
 <xref:System.Data.SqlTypes.SqlString> 構造体では、`String` から <xref:System.Data.SqlTypes.SqlString> への変換演算子 ([CType 関数](../../../language-reference/functions/ctype-function.md)) と、<xref:System.Data.SqlTypes.SqlString> から `String` への別の変換演算子が定義されています。 `title` を `jobTitle` に割り当てるステートメントでは最初の演算子を使用し、<xref:Microsoft.VisualBasic.Interaction.MsgBox%2A> 関数呼び出しでは 2 番目の演算子を使用します。  
  
## <a name="compile-the-code"></a>コードのコンパイル  
 使用しているクラスまたは構造体で、使用する演算子が定義されていることを確認します。 クラスまたは構造体で、オーバーロードに使用できるすべての演算子が定義されていると想定しないでください。 使用可能な演算子の一覧については、「[Operator Statement (Operator ステートメント)](../../../language-reference/statements/operator-statement.md)」をご覧ください。  
  
 ソース ファイルの先頭に、SQL 文字列の適切な `Imports` ステートメントを含めます (この例では <xref:System.Data.SqlTypes>)。  
  
 プロジェクトには、System.Data および System.XML への参照が含まれている必要があります。  
  
## <a name="see-also"></a>関連項目

- [演算子プロシージャ](./operator-procedures.md)
- [方法: 演算子を定義する](./how-to-define-an-operator.md)
- [方法: 変換演算子を定義する](./how-to-define-a-conversion-operator.md)
- [方法: 演算子プロシージャを呼び出す](./how-to-call-an-operator-procedure.md)
- [Widening](../../../language-reference/modifiers/widening.md)
- [Narrowing](../../../language-reference/modifiers/narrowing.md)
- [Structure ステートメント](../../../language-reference/statements/structure-statement.md)
- [方法: 構造体を宣言する](../data-types/how-to-declare-a-structure.md)
- [暗黙の型変換と明示的な型変換](../data-types/implicit-and-explicit-conversions.md)
- [拡大変換と縮小変換](../data-types/widening-and-narrowing-conversions.md)
