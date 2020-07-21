---
title: <seealso>
ms.date: 07/20/2015
helpviewer_keywords:
- <seealso> XML tag
- seealso XML tag
ms.assetid: 36050c95-1af2-4284-b9b6-1a70691ed978
ms.openlocfilehash: 5999a4ebcc90f21ee8331b96ffb2a50f7905b1b6
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84411513"
---
# <a name="seealso-visual-basic"></a>\<seealso> (Visual Basic)
関連項目セクションに表示されるリンクを指定します。  
  
## <a name="syntax"></a>構文  
  
```xml  
<seealso cref="member"/>  
```  
  
## <a name="parameters"></a>パラメーター  
 `member`  
 現在のコンパイル環境からの呼び出しに利用できる、メンバーまたはフィールドへの参照。 コンパイラは、指定されたコード要素が存在するかどうかを確認し、`member` を出力 XML 内の要素名に渡します。 `member` は、二重引用符 (" ") で囲む必要があります。  
  
## <a name="remarks"></a>Remarks  
 `<seealso>` タグを使用して、関連項目セクションに表示するテキストを指定します。 [\<see>](see.md) を使用すると、テキスト内からリンクを指定できます。  
  
 コンパイル時に [-doc](../../reference/command-line-compiler/doc.md) を指定して、ドキュメント コメントをファイルに出力します。  
  
## <a name="example"></a>例  
 この例では、`DoesRecordExist` 解説セクションの `<seealso>` タグを使用して、`UpdateRecord` メソッドを参照します。  
  
 [!code-vb[VbVbcnXmlDocComments#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnXmlDocComments/VB/Class1.vb#6)]  
  
## <a name="see-also"></a>関連項目

- [XML のコメント用タグ](index.md)
