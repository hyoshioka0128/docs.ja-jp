---
title: '方法: ノード フラグメントを変換する'
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
ms.assetid: 73a6c582-b9d7-4fa7-9a05-6d931e1f3de8
ms.openlocfilehash: e44f44db3e12c5e297f137fa247ecfc2d809dd4d
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84287715"
---
# <a name="how-to-transform-a-node-fragment"></a>方法: ノード フラグメントを変換する
<xref:System.Xml.XmlDocument> オブジェクトまたは <xref:System.Xml.XPath.XPathDocument> オブジェクトに含まれるデータを変換すると、XSLT 変換はドキュメント全体に適用されます。 つまり、ドキュメント ルート ノード以外のノードを指定しても、変換処理では、読み込んだドキュメントのすべてのノードがアクセスされます。 1 つのノード フラグメントを変換するには、ノード フラグメントだけを含むオブジェクトを別に作成し、そのオブジェクトを <xref:System.Xml.Xsl.XslCompiledTransform.Transform%2A> メソッドに渡します。  
  
## <a name="procedures"></a>プロシージャ  
  
#### <a name="to-transform-a-node-fragment"></a>1 つのノード フラグメントを変換するには  
  
1. ソース ドキュメントを含むオブジェクトを作成します。  
  
2. 変換するノード フラグメントを見つけます。  
  
3. そのノード フラグメントだけの別のオブジェクトを作成します。  
  
4. ノード フラグメントを <xref:System.Xml.Xsl.XslCompiledTransform.Transform%2A> メソッドに渡します。  
  
## <a name="example"></a>例  
 次の例は、1 つのノード フラグメントを変換して、結果をコンソールに出力します。  
  
 [!code-csharp[XSLT_NodeFrag#1](../../../../samples/snippets/csharp/VS_Snippets_Data/XSLT_NodeFrag/CS/xslt_frag.cs#1)]
 [!code-vb[XSLT_NodeFrag#1](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XSLT_NodeFrag/VB/xslt_frag.vb#1)]  
  
### <a name="input"></a>入力  
  
##### <a name="booksxml"></a>books.xml  
 [!code-xml[XML_Core_Files#1](../../../../samples/snippets/xml/VS_Snippets_Data/XML_Core_Files/XML/books.xml#1)]  
  
##### <a name="singlexsl"></a>single.xsl  
 [!code-xml[XSLT_NodeFrag#2](../../../../samples/snippets/xml/VS_Snippets_Data/XSLT_NodeFrag/XML/single.xsl#2)]  
  
### <a name="output"></a>Output  
 Book title is The Confidence Man.  
  
## <a name="see-also"></a>関連項目

- [XslCompiledTransform クラスの使用](using-the-xslcompiledtransform-class.md)
