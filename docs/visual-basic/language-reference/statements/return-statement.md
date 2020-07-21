---
title: Return ステートメント
ms.date: 07/20/2015
f1_keywords:
- vb.Return
helpviewer_keywords:
- Return statement [Visual Basic], syntax
- control flow [Visual Basic], returning control to expressions
- Return statement [Visual Basic]
- expressions [Visual Basic], returning control to
ms.assetid: ac86e7f0-5a67-42c3-9834-0e0381efa3ec
ms.openlocfilehash: cdb58e32c30c8e6c1662fb698ac5576c3f71258c
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84404201"
---
# <a name="return-statement-visual-basic"></a>Return ステートメント (Visual Basic)
`Function`、`Sub`、`Get`、`Set`、または `Operator` プロシージャを呼び出したコードに制御を戻します。  
  
## <a name="syntax"></a>構文  
  
```vb  
Return  
' -or-  
Return expression  
```  
  
## <a name="part"></a>パーツ  
 `expression`  
 `Function`、`Get`、または `Operator` プロシージャで必要です。 呼び出し元のコードに返される値を表す式。  
  
## <a name="remarks"></a>Remarks  
 `Sub` または `Set` プロシージャでは、`Return` ステートメントは `Exit Sub` または `Exit Property` ステートメントと同じです。`expression` は指定しないでください。  
  
 `Function`、`Get`、または `Operator` プロシージャでは、`Return` ステートメントに `expression` を含める必要があります。また、`expression` は、プロシージャの戻り値の型に変換可能なデータ型に評価される必要があります。 `Function` または `Get` プロシージャでは、プロシージャ名に式を代入して戻り値として使用し、`Exit Function` または `Exit Property` ステートメントを実行する方法もあります。 `Operator` プロシージャでは、`Return expression` を使用する必要があります。  
  
 `Return` ステートメントは、必要に応じて同じプロシージャにいくつでも含めることができます。  
  
> [!NOTE]
> `Finally` ブロック内のコードは、`Try` または `Catch` ブロック内で `Return` ステートメントが検出された後、その `Return` ステートメントが実行される前に実行されます。 `Return` ステートメントを `Finally` ブロックに含めることはできません。  
  
## <a name="example"></a>例  
 次の例では、`Return` ステートメントを複数回使用して、プロシージャが他の操作を行う必要がない場合に、呼び出し元のコードに戻ります。  
  
 [!code-vb[VbVbalrStatements#53](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#53)]  
  
## <a name="see-also"></a>関連項目

- [Function ステートメント](function-statement.md)
- [Sub ステートメント](sub-statement.md)
- [Get ステートメント](get-statement.md)
- [Set ステートメント](set-statement.md)
- [Operator ステートメント](operator-statement.md)
- [Property ステートメント](property-statement.md)
- [Exit ステートメント](exit-statement.md)
- [Try...Catch...Finally ステートメント](try-catch-finally-statement.md)
