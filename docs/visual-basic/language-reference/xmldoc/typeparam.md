---
title: <typeparam>
ms.date: 07/20/2015
helpviewer_keywords:
- typeparam XML tag
- <typeparam> XML tag
ms.assetid: 1bb5ba78-f060-478c-905c-77a2e43639af
ms.openlocfilehash: 2ad54845645172acb5b91935f5347a828510e3aa
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84411487"
---
# <a name="typeparam-visual-basic"></a>\<typeparam> (Visual Basic)
型パラメーターの名前と説明を定義します。  
  
## <a name="syntax"></a>構文  
  
```xml  
<typeparam name="name">description</typeparam>  
```  
  
## <a name="parameters"></a>パラメーター  
 `name`  
 型パラメーターの名前。 名前は二重引用符 (" ") で囲みます。  
  
 `description`  
 型パラメーターの説明。  
  
## <a name="remarks"></a>Remarks  
 ジェネリック型のコメントまたはジェネリック メンバー宣言で `<typeparam>` タグを使用して、型パラメーターの 1 つについて記述します。  
  
 コンパイル時に [-doc](../../reference/command-line-compiler/doc.md) を指定して、ドキュメント コメントをファイルに出力します。  
  
## <a name="example"></a>例  
 この例では、`<typeparam>` タグを使用して `id` パラメーターを記述します。  
  
 [!code-vb[VbVbcnXmlDocComments#8](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnXmlDocComments/VB/Class1.vb#8)]  
  
## <a name="see-also"></a>関連項目

- [XML のコメント用タグ](index.md)
