---
title: '<remarks> (Visual Basic)'
ms.date: 07/20/2015
helpviewer_keywords:
- <remarks> XML tag
- remarks XML tag
ms.assetid: c6241773-a7ed-41c9-9a8b-9722a0c606a9
ms.openlocfilehash: 97fca8758d9c21ac0b8f15bf9d5831750fbabe77
ms.sourcegitcommit: a885cc8c3e444ca6471348893d5373c6e9e49a47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/06/2018
ms.locfileid: "43863034"
---
# <a name="ltremarksgt-visual-basic"></a><remarks> (Visual Basic)
メンバーの「解説」セクションをを指定します。  
  
## <a name="syntax"></a>構文  
  
```xml  
<remarks>description</remarks>  
```  
  
#### <a name="parameters"></a>パラメーター  
 `description`  
 メンバーの説明。  
  
## <a name="remarks"></a>Remarks  
 使用して、`<remarks>`で指定された情報を補うため、型に関する情報を追加するタグ[\<summary>](../../../visual-basic/language-reference/xmldoc/summary.md)します。  
  
 この情報は、オブジェクト ブラウザーに表示されます。 オブジェクト ブラウザーの詳細については、次を参照してください。[コードの構造を表示する](/visualstudio/ide/viewing-the-structure-of-code)します。  
  
 コンパイル時に [/doc](../../../visual-basic/reference/command-line-compiler/doc.md) を指定して、ドキュメント コメントをファイルに出力します。  
  
## <a name="example"></a>例  
 この例では、`<remarks>`何かを説明するタグ、`UpdateRecord`メソッドします。  
  
 [!code-vb[VbVbcnXmlDocComments#6](../../../visual-basic/language-reference/xmldoc/codesnippet/VisualBasic/remarks_1.vb)]  
  
## <a name="see-also"></a>関連項目  
 [XML のコメント用タグ](../../../visual-basic/language-reference/xmldoc/index.md)
