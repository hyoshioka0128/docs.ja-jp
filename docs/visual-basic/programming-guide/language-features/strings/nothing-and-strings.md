---
title: テキストと文字列
ms.date: 07/20/2015
helpviewer_keywords:
- strings [Visual Basic], Nothing
ms.assetid: 261380af-2024-4ecf-823b-43b1034d92cd
ms.openlocfilehash: 392de45b0ee1688224f3e8170b0144f1acdb0912
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84360567"
---
# <a name="nothing-and-strings-in-visual-basic"></a>Visual Basic の Nothing と文字列
Visual Basic ランタイムと .NET Framework では、文字列に関する `Nothing` の評価が異なります。  
  
## <a name="visual-basic-runtime-and-the-net-framework"></a>Visual Basic ランタイムと .NET Framework  
 次に例を示します。  
  
 [!code-vb[VbVbalrStrings#47](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStrings/VB/Class2.vb#47)]  
  
 通常、Visual Basic ランタイムでは、`Nothing` が空の文字列 ("") として評価されます。 ただし、.NET Framework では実行されず、`Nothing` に対して文字列操作を実行しようとするたびに例外がスローされます。  
  
## <a name="see-also"></a>関連項目

- [Visual Basic の文字列の概要](introduction-to-strings.md)
