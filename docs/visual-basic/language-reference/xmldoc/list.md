---
title: <list>
ms.date: 07/20/2015
helpviewer_keywords:
- listheader XML tag
- <item> XML tag
- <list> XML tag
- <listheader> XML tag
- term XML tag
- list XML tag
- <description> XML tag
- description XML tag
- item XML tag
- <term> XML tag
ms.assetid: ec35fced-d58e-4520-a764-0691256e014b
ms.openlocfilehash: 955c1a4c5c5619f908b8d03dbf12360c23574478
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84400087"
---
# <a name="list-visual-basic"></a>\<list> (Visual Basic)
リストまたはテーブルを定義します。  
  
## <a name="syntax"></a>構文  
  
```xml  
<list type="type">  
   <listheader>  
      <term>term</term>  
      <description>description</description>  
   </listheader>  
   <item>  
      <term>term</term>  
      <description>description</description>  
   </item>  
</list>  
```  
  
## <a name="parameters"></a>パラメーター  
 `type`  
 リストの種類。 箇条書きの場合は "bullet"、番号付きリストの場合は "number"、2 列のテーブルの場合は "table" にする必要があります。  
  
 `term`  
 `type` が "table" の場合にのみ使用されます。 定義対象の用語。description タグで定義されています。  
  
 `description`  
 `type` が "bullet" または "number" の場合、`description` は リストの項目です。`type` が "table" の場合、`description` は `term` の定義です。  
  
## <a name="remarks"></a>Remarks  
 `<listheader>` ブロックでは、テーブルまたは定義リストの見出しが定義されます。 テーブルを定義するときは、見出しの `term` のエントリを指定することだけが必要です。  
  
 リストの各項目は、`<item>` ブロックで指定されます。 定義リストを作成する場合は、`term` と `description` の両方を指定する必要があります。 ただし、テーブル、箇条書き、または番号付きリストの場合は、`description` のエントリを指定するだけです。  
  
 リストまたはテーブルでは、必要な数の `<item>` ブロックを使用できます。  
  
 コンパイル時に [-doc](../../reference/command-line-compiler/doc.md) を指定して、ドキュメント コメントをファイルに出力します。  
  
## <a name="example"></a>例  
 この例では、`<list>` タグを使用して、解説セクションの箇条書きを定義します。  
  
 [!code-vb[VbVbcnXmlDocComments#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnXmlDocComments/VB/Class1.vb#5)]  
  
## <a name="see-also"></a>関連項目

- [XML のコメント用タグ](index.md)
