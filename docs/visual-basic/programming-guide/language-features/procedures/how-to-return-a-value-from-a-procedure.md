---
title: '方法: プロシージャから値を返す'
ms.date: 07/20/2015
helpviewer_keywords:
- Visual Basic code, procedures
- procedures [Visual Basic], returning from
- procedures [Visual Basic], returning a value
ms.assetid: 4bcc4724-2b4e-4df8-9b4b-16054607f87d
ms.openlocfilehash: 917e52b711645fbf94a132216a3fa90b0dfc15b3
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84414325"
---
# <a name="how-to-return-a-value-from-a-procedure-visual-basic"></a>方法: プロシージャから値を返す (Visual Basic)
`Function` プロシージャは、`Return` ステートメントを実行するか、`Exit Function` または `End Function` ステートメントを検出すると、呼び出し元のコードに値を返します。  
  
### <a name="to-return-a-value-using-the-return-statement"></a>Return ステートメントを使用して値を返すには  
  
1. プロシージャのタスクが完了した位置に、`Return` ステートメントを配置します。  
  
2. `Return` キーワードの後に、呼び出し元のコードに返す値を生成する式を入力します。  
  
3. 同じプロシージャ内に複数の `Return` ステートメントを含めることができます。  
  
     次の `Function` プロシージャは、直角三角形の最も長い辺 (斜辺) を計算して呼び出し元のコードに返します。  
  
     [!code-vb[VbVbcnProcedures#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#1)]  
  
     次の例は、戻り値を格納する `hypotenuse` の一般的な呼び出しを示しています。  
  
     [!code-vb[VbVbcnProcedures#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#6)]  
  
### <a name="to-return-a-value-using-exit-function-or-end-function"></a>Exit Function または End Function を使用して値を返すには  
  
1. `Function` プロシージャ内の少なくとも 1 か所で、プロシージャの名前に値を割り当てます。  
  
2. `Exit Function` または `End Function` ステートメントを実行すると、Visual Basic はプロシージャの名前に最後に割り当てられた値を返します。  
  
3. 同じプロシージャ内に複数の `Exit Function` ステートメントを含めることができ、さらに同じプロシージャ内に `Return` ステートメントと `Exit Function` ステートメントを混在させることができます。  
  
4. `End Function` ステートメントは、`Function` プロシージャに 1 つだけ含めることができます。  
  
     詳細と例については、「[Function Statement (Function ステートメント)](../../../language-reference/statements/function-statement.md)」の戻り値に関するセクションをご覧ください。  
  
## <a name="see-also"></a>関連項目

- [手順](./index.md)
- [Sub プロシージャ](./sub-procedures.md)
- [Property プロシージャ](./property-procedures.md)
- [演算子プロシージャ](./operator-procedures.md)
- [プロシージャのパラメーターと引数](./procedure-parameters-and-arguments.md)
- [Function ステートメント](../../../language-reference/statements/function-statement.md)
- [Return ステートメント](../../../language-reference/statements/return-statement.md)
- [方法: 値を返すプロシージャを作成する](./how-to-create-a-procedure-that-returns-a-value.md)
- [方法: 値を返すプロシージャを呼び出す](./how-to-call-a-procedure-that-returns-a-value.md)
