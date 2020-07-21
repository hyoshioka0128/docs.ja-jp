---
title: <permission>
ms.date: 07/20/2015
helpviewer_keywords:
- <permission> XML tag
- permission XML tag
ms.assetid: 0edf0500-5cd7-49c0-9255-64c48f972b77
ms.openlocfilehash: b3acec04060367a0b9e54b19c0106644d028357b
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84400035"
---
# <a name="permission-visual-basic"></a>\<permission> (Visual Basic)
メンバーの必要な権限を指定します。  
  
## <a name="syntax"></a>構文  
  
```xml  
<permission cref="member">description</permission>  
```  
  
## <a name="parameters"></a>パラメーター  
 `member`  
 現在のコンパイル環境からの呼び出しに利用できる、メンバーまたはフィールドへの参照。 コンパイラは、指定されたコード要素が存在し、出力の XML で `member` が正規要素名に変換されることを確認します。 `member` を引用符 (" ") で囲みます。  
  
 `description`  
 メンバーへのアクセスの説明です。  
  
## <a name="remarks"></a>Remarks  
 `<permission>` タグを使用して、メンバーのアクセスを文書化します。 <xref:System.Security.PermissionSet> クラスを使用して、メンバーへのアクセスを指定します。  
  
 コンパイル時に [-doc](../../reference/command-line-compiler/doc.md) を指定して、ドキュメント コメントをファイルに出力します。  
  
## <a name="example"></a>例  
 この例では、`<permission>` タグを使用して、<xref:System.Security.Permissions.FileIOPermission> が `ReadFile` メソッドに必要であることを記述します。  
  
 [!code-vb[VbVbcnXmlDocComments#7](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnXmlDocComments/VB/Class1.vb#7)]  
  
## <a name="see-also"></a>関連項目

- [XML のコメント用タグ](index.md)
