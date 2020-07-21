---
title: XslTransform への XPathDocument の入力
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
ms.assetid: 7d1bbe8b-ed43-4e62-a5ba-d602d244f4ae
ms.openlocfilehash: 66cdbae8b52ca1b7ed46e8f040fcbf51c969dea2
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84282975"
---
# <a name="xpathdocument-input-to-xsltransform"></a>XslTransform への XPathDocument の入力
<xref:System.Xml.XPath.XPathDocument> は、<xref:System.Xml.Xsl.XslTransform> でドキュメントを処理するための読み取り専用キャッシュです。 <xref:System.Xml.XPath.XPathNavigator> は、構造的には XML ドキュメント オブジェクト モデル (DOM) に似ていますが、 で XPath 最適化関数を使用することで、XSLT (Extensible Stylesheet Language for Transformations) による処理と XPath (XML Path Language) データ モデルに高度に最適化されています。  
  
> [!NOTE]
> .NET Framework 2.0 では <xref:System.Xml.Xsl.XslTransform> クラスが廃止されています。 <xref:System.Xml.Xsl.XslCompiledTransform> クラスを使用して XSLT (Extensible Stylesheet Language for Transformations) 変換を実行できます。 詳しくは、「[XslCompiledTransform クラスの使用](using-the-xslcompiledtransform-class.md)」および「[XslTransform クラスからの移行](migrating-from-the-xsltransform-class.md)」をご覧ください。  
  
 変換への入力として <xref:System.Xml.XPath.XPathDocument> を作成するコード サンプルを次に示します。  
  
```vb  
Dim xslt as XslTransform = new XslTransform()  
Xslt.Load(someStylesheet)  
Dim doc as XPathDocument = New XPathDocument("books.xml")  
Dim fs as StringWriter = new StringWriter()  
Xslt.Transform(doc, Nothing, fs, Nothing);  
```  
  
```csharp  
XslTransform xslt = new XslTransform();  
Xslt.Load(someStylesheet);  
XPathDocument doc = XPathDocument("books.xml");  
StringWriter fs = new StringWriter();  
Xslt.Transform(doc, null, fs, null);  
```  
  
## <a name="see-also"></a>関連項目

- [XslTransform クラスによる XSLT プロセッサの実装](xsltransform-class-implements-the-xslt-processor.md)
