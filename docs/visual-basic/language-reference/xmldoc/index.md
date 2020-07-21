---
title: ドキュメント コメントとして推奨される XML タグ
ms.date: 07/20/2015
f1_keywords:
- vb.XmlDocComment
helpviewer_keywords:
- tags, XML
- XML comments, recommended tags [Visual Basic]
- comments, recommended XML tags
ms.assetid: 294e0736-ff1e-498e-af83-6db71ed41a72
ms.openlocfilehash: af57fc7d55c5cfda24a2fd9406b17dedee898760
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "85503787"
---
# <a name="recommended-xml-tags-for-documentation-comments-visual-basic"></a>ドキュメント コメントとして推奨される XML タグ (Visual Basic)
Visual Basic コンパイラでは、コード内のドキュメント コメントを処理し、XML ファイルに変換できます。 追加のツールを利用すれば、XML ファイルを処理してドキュメントに変換できます。  
  
 XML コメントは、型や型メンバーなどのコード コンストラクターで許可されます。 部分型の場合、そのメンバーに対するコメント作成に制限はありませんが、XML コメントを追加できる型の部分は 1 つだけです。  
  
> [!NOTE]
> ドキュメント コメントは、名前空間に適用できません。 その理由は、1 つの名前空間は複数のアセンブリにまたがることができて、かつ、すべてのアセンブリを同時に読み込む必要はないということにあります。  
  
 コンパイラは、有効な XML であるタグをすべて処理します。 次のタグによって、ユーザー ドキュメントで一般的に使用される機能が与えられます。  
  
||||  
|---|---|---|  
|[\<c>](c.md)|[\<code>](code.md)|[\<example>](example.md)|  
|[\<exception>](exception.md) <sup>1</sup>|[\<include>](include.md) <sup>1</sup>|[\<list>](list.md)|  
|[\<para>](para.md)|[\<param>](param.md) <sup>1</sup>|[\<paramref>](paramref.md)|  
|[\<permission>](permission.md) <sup>1</sup>|[\<remarks>](remarks.md)|[\<returns>](returns.md)|  
|[\<see>](see.md) <sup>1</sup>|[\<seealso>](seealso.md) <sup>1</sup>|[\<summary>](summary.md)|  
|[\<typeparam>](typeparam.md) <sup>1</sup>|[\<value>](value.md)||  
  
 (<sup>1</sup> コンパイラによって構文が検証されます。)  
  
> [!NOTE]
> ドキュメント コメントのテキストに山かっこを表示する場合は、`&lt;` と `&gt;` を使用します。 たとえば、文字列 `"&lt;text in angle brackets&gt;"` は `<text in angle brackets>` として表示されます。  
  
## <a name="see-also"></a>関連項目

- [XML の使用によるコードのドキュメントの作成](../../programming-guide/program-structure/documenting-your-code-with-xml.md)
- [-doc](../../reference/command-line-compiler/doc.md)
- [方法: XML ドキュメントを作成する](../../programming-guide/program-structure/how-to-create-xml-documentation.md)
