---
title: <param>
ms.date: 07/20/2015
helpviewer_keywords:
- param XML tag
- <param> XML tag
ms.assetid: 4e32e86f-f6f3-4301-b7fc-2f321fb54368
ms.openlocfilehash: d325d5f9fbfd132630cf280653be214a267a7a80
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84400061"
---
# <a name="param-visual-basic"></a>\<param> (Visual Basic)
パラメーターの名前と説明を定義します。  
  
## <a name="syntax"></a>構文  
  
```xml  
<param name="name">description</param>  
```  
  
## <a name="parameters"></a>パラメーター  
 `name`  
 メソッド パラメーターの名前です。 名前は二重引用符 (" ") で囲みます。  
  
 `description`  
 パラメーターの説明です。  
  
## <a name="remarks"></a>Remarks  
 `<param>` タグは、メソッドのいずれかのパラメーターを記述するために、メソッド宣言のコメントで使用する必要があります。  
  
 `<param>` タグのテキストは次の場所に表示されます。  
  
- IntelliSense のパラメーター ヒント。 詳細については、「[IntelliSense の使用](/visualstudio/ide/using-intellisense)」を参照してください。  
  
- オブジェクト ブラウザー。 詳細については、「[コードの構造の表示](/visualstudio/ide/viewing-the-structure-of-code)」を参照してください。  
  
 コンパイル時に [-doc](../../reference/command-line-compiler/doc.md) を指定して、ドキュメント コメントをファイルに出力します。  
  
## <a name="example"></a>例  
 この例では、`<param>` タグを使用して `id` パラメーターを記述します。  
  
 [!code-vb[VbVbcnXmlDocComments#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnXmlDocComments/VB/Class1.vb#6)]  
  
## <a name="see-also"></a>関連項目

- [XML のコメント用タグ](index.md)
