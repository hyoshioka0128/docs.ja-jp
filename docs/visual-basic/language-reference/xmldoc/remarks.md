---
title: <remarks>
ms.date: 07/20/2015
helpviewer_keywords:
- <remarks> XML tag
- remarks XML tag
ms.assetid: c6241773-a7ed-41c9-9a8b-9722a0c606a9
ms.openlocfilehash: c57ddb870192bd94301f99eb71ad29526e8efc28
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84400022"
---
# <a name="remarks-visual-basic"></a>\<remarks> (Visual Basic)
メンバーの解説セクションを指定します。  
  
## <a name="syntax"></a>構文  
  
```xml  
<remarks>description</remarks>  
```  
  
## <a name="parameters"></a>パラメーター  
 `description`  
 メンバーの説明。  
  
## <a name="remarks"></a>Remarks  
 `<remarks>` タグを使用して、型の情報を追加し、[\<summary>](summary.md) で指定された情報を補足します。  
  
 この情報はオブジェクト ブラウザーに表示されます。 オブジェクト ブラウザーについては、「[コードの構造の表示](/visualstudio/ide/viewing-the-structure-of-code)」を参照してください。  
  
 コンパイル時に [-doc](../../reference/command-line-compiler/doc.md) を指定して、ドキュメント コメントをファイルに出力します。  
  
## <a name="example"></a>例  
 この例では、`<remarks>` タグを使用して `UpdateRecord` メソッドの動作を説明します。  
  
 [!code-vb[VbVbcnXmlDocComments#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnXmlDocComments/VB/Class1.vb#6)]  
  
## <a name="see-also"></a>関連項目

- [XML のコメント用タグ](index.md)
