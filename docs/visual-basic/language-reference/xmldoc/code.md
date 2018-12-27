---
title: '&lt;コード&gt;(Visual Basic)'
ms.date: 07/20/2015
helpviewer_keywords:
- code XML tag
- <code> XML tag
ms.assetid: 925e5342-be05-45f2-bf66-7398bbd6710e
ms.openlocfilehash: e66aebe35dd8f6443fefe3b07842b37270159e6e
ms.sourcegitcommit: 3c1c3ba79895335ff3737934e39372555ca7d6d0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/06/2018
ms.locfileid: "43858640"
---
# <a name="ltcodegt-visual-basic"></a>&lt;コード&gt;(Visual Basic)
テキストが複数行のコードであることを示します。  
  
## <a name="syntax"></a>構文  
  
```xml  
<code>content</code>  
```  
  
#### <a name="parameters"></a>パラメーター  
 `content`  
 コードとしてマークするテキスト。  
  
## <a name="remarks"></a>Remarks  
 使用して、`<code>`をコードとして複数の行を示すタグ。 説明内のテキストをコードとしてマークする場合は、[\<c>](../../../visual-basic/language-reference/xmldoc/c.md) タグを使用します。  
  
 コンパイル時に [/doc](../../../visual-basic/reference/command-line-compiler/doc.md) を指定して、ドキュメント コメントをファイルに出力します。  
  
## <a name="example"></a>例  
 この例では、\<code> タグを使用するためのサンプル コードを`ID`フィールド。  
  
 [!code-vb[VbVbcnXmlDocComments#2](../../../visual-basic/language-reference/xmldoc/codesnippet/VisualBasic/code_1.vb)]  
  
## <a name="see-also"></a>関連項目  
 [XML のコメント用タグ](../../../visual-basic/language-reference/xmldoc/index.md)
