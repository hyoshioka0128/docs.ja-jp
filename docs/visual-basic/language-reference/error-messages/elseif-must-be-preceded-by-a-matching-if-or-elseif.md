---
title: ''#ElseIf' の前には、対応する '#If' または '#ElseIf' が必要です'
ms.date: 07/20/2015
f1_keywords:
- vbc30014
- bc30014
helpviewer_keywords:
- BC30014
ms.assetid: 5215585e-2efa-485a-9efe-9833a1cc83a0
ms.openlocfilehash: ef904173b1791309f6c2722bd959cabdad1d71da
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/04/2018
ms.locfileid: "33588149"
---
# <a name="39elseif39-must-be-preceded-by-a-matching-39if39-or-39elseif39"></a>'#ElseIf' の前には、対応する '#If' または '#ElseIf' が必要です
`#ElseIf` 条件付きコンパイル ディレクティブです。 `#ElseIf`句の前に、対応する必要があります`#If`または`#ElseIf`句。  
  
 **エラー ID:** BC30014  
  
## <a name="to-correct-this-error"></a>このエラーを解決するには  
  
1.  確認先行`#If`または`#ElseIf`これから分割されたいない`#ElseIf`によって、中間の条件付きコンパイル ブロックや、間違って配置された`#End If`です。  
  
2.  場合、`#ElseIf`は後に、`#Else`ディレクティブを削除するか、`#Else`に変更して、または、`#ElseIf`です。  
  
3.  他のすべての順序が正しい場合、 `#If` ディレクティブを条件付きコンパイル ブロックの先頭に追加します。  
  
## <a name="see-also"></a>関連項目  
 [#If...Then...#Else ディレクティブ](../../../visual-basic/language-reference/directives/if-then-else-directives.md)
