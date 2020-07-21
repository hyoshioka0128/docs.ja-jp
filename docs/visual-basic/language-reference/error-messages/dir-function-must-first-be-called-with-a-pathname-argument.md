---
title: "'Dir' 関数は、'Pathname' 引数で最初に呼び出されなければなりません。"
ms.date: 07/20/2015
f1_keywords:
- vbrDIR_IllegalCall
ms.assetid: 7b5d149f-be91-4ac3-8262-86a360894e7d
ms.openlocfilehash: d255b8dddd098835764f72b8a166eaa08b0353df
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61803455"
---
# <a name="dir-function-must-first-be-called-with-a-pathname-argument"></a>'Dir' 関数は、'Pathname' 引数で最初に呼び出されなければなりません。
`Dir` 関数の最初の呼び出しには、`PathName` 引数は含まれていません。 `Dir` の最初の呼び出しには `PathName` を含める必要がありますが、後続の `Dir` の呼び出しには、次の項目を取得するためのパラメーターを含める必要はありません。  
  
## <a name="to-correct-this-error"></a>このエラーを解決するには  
  
1. 関数呼び出しに `PathName` 引数を指定します。  
  
## <a name="see-also"></a>関連項目

- <xref:Microsoft.VisualBasic.FileSystem.Dir%2A>
