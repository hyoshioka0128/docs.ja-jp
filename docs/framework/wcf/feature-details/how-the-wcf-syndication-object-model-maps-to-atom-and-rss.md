---
title: WCF 配信オブジェクト モデルを Atom や RSS に割り当てる方法
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 0365eb37-98cc-4b13-80fb-f1e78847a748
ms.openlocfilehash: 67fbbb035a3a6683cefbf24e299f32579b674bbd
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84597255"
---
# <a name="how-the-wcf-syndication-object-model-maps-to-atom-and-rss"></a>WCF 配信オブジェクト モデルを Atom や RSS に割り当てる方法
Windows Communication Foundation (WCF) 配信サービスを開発する場合は、次のクラスを使用してフィードと項目を作成します。  
  
- <xref:System.ServiceModel.Syndication.SyndicationFeed>  
  
- <xref:System.ServiceModel.Syndication.SyndicationItem>  
  
- <xref:System.ServiceModel.Syndication.SyndicationPerson>  
  
- <xref:System.ServiceModel.Syndication.SyndicationLink>  
  
- <xref:System.ServiceModel.Syndication.SyndicationCategory>  
  
- <xref:System.ServiceModel.Syndication.TextSyndicationContent>  
  
- <xref:System.ServiceModel.Syndication.UrlSyndicationContent>  
  
- <xref:System.ServiceModel.Syndication.XmlSyndicationContent>  
  
 <xref:System.ServiceModel.Syndication.SyndicationFeed> はフォーマッタが定義されている任意の配信フォーマットにシリアル化できます。 WCF には、とという2つのフォーマッタが付属 <xref:System.ServiceModel.Syndication.Atom10FeedFormatter> して <xref:System.ServiceModel.Syndication.Rss20FeedFormatter> います。  
  
 RSS 2.0 仕様より Atom 1.0 仕様の方が、<xref:System.ServiceModel.Syndication.SyndicationFeed> および <xref:System.ServiceModel.Syndication.SyndicationItem> 周辺のオブジェクト モデルをより細かく調整しています。 これは、Atom 1.0 が、あいまいな要素または RSS 2.0 仕様から省略された要素を定義する、より基本的な仕様であるためです。 このため、WCF 配信オブジェクトモデルの多くの項目は、RSS 2.0 仕様に直接表現されていません。 <xref:System.ServiceModel.Syndication.SyndicationFeed>とオブジェクトを <xref:System.ServiceModel.Syndication.SyndicationItem> RSS 2.0 にシリアル化する場合、WCF では、atom 仕様に準拠した名前空間で修飾された拡張要素として、atom 固有のデータ要素をシリアル化できます。 これは、<xref:System.ServiceModel.Syndication.Rss20FeedFormatter> コンストラクターに渡すパラメーターで制御できます。  
  
 このトピックのコード例では、ここで定義される 2 つのメソッドのいずれかを使い、実際のシリアル化を行っています。  
  
 `SerializeFeed` は、配信フィードをシリアル化します。  
  
 [!code-csharp[SyndicationMapping#10](../../../../samples/snippets/csharp/VS_Snippets_CFX/syndicationmapping/cs/snippets.cs#10)]
 [!code-vb[SyndicationMapping#10](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/syndicationmapping/vb/snippets.vb#10)]  
  
 `SerializeItem` は、配信項目をシリアル化します。  
  
 [!code-csharp[SyndicationMapping#11](../../../../samples/snippets/csharp/VS_Snippets_CFX/syndicationmapping/cs/snippets.cs#11)]
 [!code-vb[SyndicationMapping#11](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/syndicationmapping/vb/snippets.vb#11)]  
  
## <a name="syndicationfeed"></a>SyndicationFeed  
 <xref:System.ServiceModel.Syndication.SyndicationFeed> クラスを Atom 1.0 および RSS 2.0 にシリアル化するコード例を次に示します。  
  
 [!code-csharp[SyndicationMapping#0](../../../../samples/snippets/csharp/VS_Snippets_CFX/syndicationmapping/cs/snippets.cs#0)]
 [!code-vb[SyndicationMapping#0](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/syndicationmapping/vb/snippets.vb#0)]  
  
 <xref:System.ServiceModel.Syndication.SyndicationFeed> を Atom 1.0 にシリアル化する方法を次の XML に示します。  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<feed xml:lang="EN-US" xmlns="http://www.w3.org/2005/Atom">  
  <title type="text">My Feed Title</title>  
  <subtitle type="text">My Feed Description</subtitle>  
  <id>FeedID</id>  
  <rights type="text">Copyright 2007</rights>  
  <updated>2007-08-29T13:57:17-07:00</updated>  
  <category term="categoryName" label="categoryLabel" scheme="categoryScheme" />  
  <logo>http://server/image.jpg</logo>  
  <generator>Sample Code</generator>  
  <link rel="alternate" href="http://myfeeduri/" />  
  <entry>  
    <id>ItemID</id>  
    <title type="text">Item Title</title>  
    <summary type="text">Item Summary</summary>  
    <published>2007-08-29T00:00:00-07:00</published>  
    <updated>2007-08-29T13:57:17-07:00</updated>  
    <author>  
      <name>Jesper Aaberg</name>  
      <uri>http://Jesper/Aaberg</uri>  
      <email>Jesper@Aaberg.com</email>  
    </author>  
    <contributor>  
      <name>Lene Aaling</name>  
      <uri>http://Lene/Aaling</uri>  
      <email>Lene@Aaling.com</email>  
    </contributor>  
    <link rel="alternate" href="http://myitemuri/" />  
    <category term="categoryName" label="categoryLabel" scheme="categoryScheme" />  
    <content type="text">Item Content</content>  
    <rights type="text">Copyright 2007</rights>  
    <source>  
      <title type="text">My Feed Title</title>  
      <subtitle type="text">My Feed Description</subtitle>  
      <id>FeedID</id>  
      <rights type="text">Copyright 2007</rights>  
      <updated>2007-08-29T13:57:17-07:00</updated>  
      <category term="categoryName" label="categoryLabel" scheme="categoryScheme" />  
      <logo>http://server/image.jpg</logo>  
      <generator>Sample Code</generator>  
      <link rel="alternate" href="http://myfeeduri/" />  
    </source>  
  </entry>  
</feed>  
```  
  
 <xref:System.ServiceModel.Syndication.SyndicationFeed> を RSS 2.0.0 にシリアル化する方法を次の XML に示します。  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<rss xmlns:a10="http://www.w3.org/2005/Atom" version="2.0">  
  <channel>  
    <title>My Feed Title</title>  
    <link>http://myfeeduri/</link>  
    <description>My Feed Description</description>  
    <language>EN-US</language>  
    <copyright>Copyright 2007</copyright>  
    <lastBuildDate>Wed, 29 Aug 2007 13:57:17 -0700</lastBuildDate>  
    <category domain="categoryScheme">categoryName</category>  
    <generator>Sample Code</generator>  
    <image>  
      <url>http://server/image.jpg</url>  
      <title>My Feed Title</title>  
      <link>http://myfeeduri/</link>  
    </image>  
    <a10:id>FeedID</a10:id>  
    <item>  
      <guid isPermaLink="false">ItemID</guid>  
      <link>http://myitemuri/</link>  
      <author>Jesper@Aaberg.com</author>  
      <category domain="categoryScheme">categoryName</category>  
      <title>Item Title</title>  
      <description>Item Summary</description>  
      <source>My Feed Title</source>  
      <pubDate>Wed, 29 Aug 2007 00:00:00 -0700</pubDate>  
      <a10:updated>2007-08-29T13:57:17-07:00</a10:updated>  
      <a10:rights type="text">Copyright 2007</a10:rights>  
      <a10:content type="text">Item Content</a10:content>  
      <a10:contributor>  
        <a10:name>Lene Aaling</a10:name>  
        <a10:uri>http://Lene/Aaling</a10:uri>  
        <a10:email>Lene@Aaling.com</a10:email>  
      </a10:contributor>  
    </item>  
  </channel>  
</rss>  
```  
  
## <a name="syndicationitem"></a>SyndicationItem  
 <xref:System.ServiceModel.Syndication.SyndicationItem> クラスを Atom 1.0 および RSS 2.0 にシリアル化するコード例を次に示します。  
  
 [!code-csharp[SyndicationMapping#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/syndicationmapping/cs/snippets.cs#1)]
 [!code-vb[SyndicationMapping#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/syndicationmapping/vb/snippets.vb#1)]  
  
 <xref:System.ServiceModel.Syndication.SyndicationItem> を Atom 1.0 にシリアル化する方法を次の XML に示します。  
  
```xml  
<entry xmlns="http://www.w3.org/2005/Atom">  
  <id>ItemID</id>  
  <title type="text">Item Title</title>  
  <summary type="text">Item Summary</summary>  
  <published>2007-08-29T00:00:00-07:00</published>  
  <updated>2007-08-29T14:07:09-07:00</updated>  
  <author>  
    <name>Jesper Aaberg</name>  
    <uri>http://Contoso/Aaberg</uri>  
    <email>Jesper.Aaberg@contoso.com</email>  
  </author>  
  <author>  
    <name>Syed Abbas</name>  
    <uri>http://Contoso/Abbas</uri>  
    <email>Syed.Abbas@contoso.com</email>  
  </author>  
  <contributor>  
    <name>Lene Aaling</name>  
    <uri>http://Contoso/Aaling</uri>  
    <email>Lene.Aaling@contoso.com</email>  
  </contributor>  
  <contributor>  
    <name>Kim Abercrombie</name>  
    <uri>http://Contoso/Abercrombie</uri>  
    <email>Kim.Abercrombie@contoso.com</email>  
  </contributor>  
  <link rel="alternate" href="http://myitemuri/" />  
  <category term="categoryName" label="categoryLabel" scheme="categoryScheme" />  
  <category term="categoryName" label="categoryLabel" scheme="categoryScheme" />  
  <content type="text">Item Content</content>  
  <rights type="text">Copyright 2007</rights>  
  <source>  
    <title type="text">My Feed Title</title>  
    <subtitle type="text">My Feed Description</subtitle>  
    <link rel="alternate" href="http://myfeeduri/" />  
  </source>  
</entry>  
```  
  
 <xref:System.ServiceModel.Syndication.SyndicationItem> を RSS 2.0.0 にシリアル化する方法を次の XML に示します。  
  
```xml  
<item>  
  <guid isPermaLink="false">ItemID</guid>  
  <link>http://myitemuri/</link>  
  <author xmlns="http://www.w3.org/2005/Atom">  
    <name>Jesper Aaberg</name>  
    <uri>http://Jesper/Aaberg</uri>  
    <email>Jesper@Aaberg.com</email>  
  </author>  
  <author xmlns="http://www.w3.org/2005/Atom">  
    <name>Syed Abbas</name>  
    <uri>http://Contoso/Abbas</uri>  
    <email>Syed.Abbas@contoso.com</email>  
  </author>  
  <category domain="categoryScheme">categoryName</category>  
  <category domain="categoryScheme">categoryName</category>  
  <title>Item Title</title>  
  <description>Item Summary</description>  
  <source>My Feed Title</source>  
  <pubDate>Wed, 29 Aug 2007 00:00:00 -0700</pubDate>  
  <updated xmlns="http://www.w3.org/2005/Atom">2007-08-29T14:07:09-07:00</updated>  
  <rights type="text" xmlns="http://www.w3.org/2005/Atom">Copyright 2007</rights>  
  <content type="text" xmlns="http://www.w3.org/2005/Atom">Item Content</content>  
  <contributor xmlns="http://www.w3.org/2005/Atom">  
    <name>Lene Aaling</name>  
    <uri>http://Contoso/Aaling</uri>  
    <email>Lene.Aaling@contoso.com</email>  
  </contributor>  
  <contributor xmlns="http://www.w3.org/2005/Atom">  
    <name>Kim Abercrombie</name>  
    <uri>http://Contoso/Abercrombie</uri>  
    <email>Kim.Abercrombie@contoso.com</email>  
  </contributor>  
</item>  
```  
  
## <a name="syndicationperson"></a>SyndicationPerson  
 <xref:System.ServiceModel.Syndication.SyndicationPerson> クラスを Atom 1.0 および RSS 2.0 にシリアル化するコード例を次に示します。  
  
 [!code-csharp[SyndicationMapping#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/syndicationmapping/cs/snippets.cs#2)]
 [!code-vb[SyndicationMapping#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/syndicationmapping/vb/snippets.vb#2)]  
  
 <xref:System.ServiceModel.Syndication.SyndicationPerson> を Atom 1.0 にシリアル化する方法を次の XML に示します。  
  
```xml  
  <author>  
    <name>Jesper Aaberg</name>  
    <uri>http://Contoso/Aaberg</uri>  
    <email>Jesper.Aaberg@contoso.com</email>  
  </author>  
<contributor>  
    <name>Lene Aaling</name>  
    <uri>http://Contoso/Aaling</uri>  
    <email>Lene.Aaling@contoso.com</email>  
  </contributor>  
```  
  
 <xref:System.ServiceModel.Syndication.SyndicationPerson> コレクションまたは <xref:System.ServiceModel.Syndication.SyndicationPerson> コレクションに、それぞれ `Authors` が 1 つのみ存在する場合に、`Contributors` クラスを RSS 2.0 にシリアル化する方法を次の XML に示します。  
  
```xml  
<author>Jesper.Aaberg@contoso.com</author>  
<a10:contributor>  
    <a10:name>Lene Aaling</a10:name>  
    <a10:uri>http://Contoso/Aaling</a10:uri>  
    <a10:email>Lene.Aaling@contoso.com</a10:email>  
</a10:contributor>  
```  
  
 <xref:System.ServiceModel.Syndication.SyndicationPerson> コレクションまたは <xref:System.ServiceModel.Syndication.SyndicationPerson> コレクションに、それぞれ `Authors` が複数存在する場合に、`Contributors` クラスを RSS 2.0 にシリアル化する方法を次の XML に示します。  
  
```xml  
<a10:author>  
    <a10:name>Jesper Aaberg</a10:name>  
    <a10:uri>http://Contoso/Aaberg</a10:uri>  
    <a10:email>Jesper.Aaberg@contoso.com</a10:email>  
</a10:author>  
<a10:author>  
    <a10:name>Syed Abbas</a10:name>  
    <a10:uri>http://Contoso/Abbas</a10:uri>  
    <a10:email>Syed.Abbas@contoso.com</a10:email>  
</a10:author>  
<a10:contributor>  
    <a10:name>Lene Aaling</a10:name>  
    <a10:uri>http://Contoso/Aaling</a10:uri>  
    <a10:email>Lene.Aaling@contoso.com</a10:email>  
</a10:contributor>  
<a10:contributor>  
    <a10:name>Kim Abercrombie</a10:name>  
    <a10:uri>http://Contoso/Abercrombie</a10:uri>  
    <a10:email>Kim.Abercrombie@contoso.com</a10:email>  
</a10:contributor>  
```  
  
## <a name="syndicationlink"></a>SyndicationLink  
 <xref:System.ServiceModel.Syndication.SyndicationLink> クラスを Atom 1.0 および RSS 2.0 にシリアル化するコード例を次に示します。  
  
 [!code-csharp[SyndicationMapping#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/syndicationmapping/cs/snippets.cs#3)]
 [!code-vb[SyndicationMapping#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/syndicationmapping/vb/snippets.vb#3)]  
  
 <xref:System.ServiceModel.Syndication.SyndicationLink> を Atom 1.0 にシリアル化する方法を次の XML に示します。  
  
 `<link rel="alternate" type="text/html" title="My Link Title" length="2048" href="http://contoso/MyLink" />`  
  
 <xref:System.ServiceModel.Syndication.SyndicationLink> を RSS 2.0.0 にシリアル化する方法を次の XML に示します。  
  
 `<a10:link rel="alternate" type="text/html" title="My Link Title" length="2048" href="http://contoso/MyLink" />`  
  
## <a name="syndicationcategory"></a>SyndicationCategory  
 <xref:System.ServiceModel.Syndication.SyndicationCategory> クラスを Atom 1.0 および RSS 2.0 にシリアル化するコード例を次に示します。  
  
 [!code-csharp[SyndicationMapping#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/syndicationmapping/cs/snippets.cs#4)]
 [!code-vb[SyndicationMapping#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/syndicationmapping/vb/snippets.vb#4)]  
  
 <xref:System.ServiceModel.Syndication.SyndicationCategory> を Atom 1.0 にシリアル化する方法を次の XML に示します。  
  
 `<category term="categoryName" label="categoryLabel" scheme="categoryScheme" />`  
  
 <xref:System.ServiceModel.Syndication.SyndicationCategory> を RSS 2.0.0 にシリアル化する方法を次の XML に示します。  
  
 `<category domain="categoryScheme">categoryName</category>`  
  
## <a name="textsyndicationcontent"></a>TextSyndicationContent  
 <xref:System.ServiceModel.Syndication.TextSyndicationContent> が HTML コンテンツと共に作成される場合に <xref:System.ServiceModel.Syndication.TextSyndicationContent> クラスを Atom 1.0 および RSS 2.0 にシリアル化するコード例を次に示します。  
  
 [!code-csharp[SyndicationMapping#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/syndicationmapping/cs/snippets.cs#5)]
 [!code-vb[SyndicationMapping#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/syndicationmapping/vb/snippets.vb#5)]  
  
 HTML コンテンツ付きの <xref:System.ServiceModel.Syndication.TextSyndicationContent> クラスを Atom 1.0 にシリアル化する方法を次の XML に示します。  
  
 `<content type="html"><html> some html </html></content>`  
  
 HTML コンテンツ付きの <xref:System.ServiceModel.Syndication.TextSyndicationContent> クラスを RSS 2.0 にシリアル化する方法を次の XML に示します。  
  
 `<description><html> some html </html></description>`  
  
 <xref:System.ServiceModel.Syndication.TextSyndicationContent> がプレーンテキスト コンテンツと共に作成される場合に、<xref:System.ServiceModel.Syndication.TextSyndicationContent> クラスを Atom 1.0 および RSS 2.0 にシリアル化するコード例を次に示します。  
  
 [!code-csharp[SyndicationMapping#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/syndicationmapping/cs/snippets.cs#6)]
 [!code-vb[SyndicationMapping#6](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/syndicationmapping/vb/snippets.vb#6)]  
  
 プレーンテキスト コンテンツ付きの <xref:System.ServiceModel.Syndication.TextSyndicationContent> クラスを Atom 1.0 にシリアル化する方法を次の XML に示します。  
  
 `<content type="text">Some Plain Text</content>`  
  
 プレーンテキスト コンテンツ付きの <xref:System.ServiceModel.Syndication.TextSyndicationContent> クラスを RSS 2.0 にシリアル化する方法を次の XML に示します。  
  
 `<description>Some Plain Text</description>`  
  
 <xref:System.ServiceModel.Syndication.TextSyndicationContent> が XHTML コンテンツと共に作成される場合に、<xref:System.ServiceModel.Syndication.TextSyndicationContent> クラスを Atom 1.0 および RSS 2.0 にシリアル化するコード例を次に示します。  
  
 [!code-csharp[SyndicationMapping#7](../../../../samples/snippets/csharp/VS_Snippets_CFX/syndicationmapping/cs/snippets.cs#7)]
 [!code-vb[SyndicationMapping#7](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/syndicationmapping/vb/snippets.vb#7)]  
  
 XHTML コンテンツ付きの <xref:System.ServiceModel.Syndication.TextSyndicationContent> クラスを Atom 1.0 にシリアル化する方法を次の XML に示します。  
  
 `<content type="xhtml">`  
  
 `<html> some xhtml </html>`  
  
 `</content>`  
  
 XHTML コンテンツ付きの <xref:System.ServiceModel.Syndication.TextSyndicationContent> クラスを RSS 2.0 にシリアル化する方法を次の XML に示します。  
  
 `<description><html> some xhtml </html></description>`  
  
## <a name="urlsyndicationcontent"></a>UrlSyndicationContent  
 <xref:System.ServiceModel.Syndication.UrlSyndicationContent> クラスを Atom 1.0 および RSS 2.0 にシリアル化するコード例を次に示します。  
  
 [!code-csharp[SyndicationMapping#8](../../../../samples/snippets/csharp/VS_Snippets_CFX/syndicationmapping/cs/snippets.cs#8)]
 [!code-vb[SyndicationMapping#8](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/syndicationmapping/vb/snippets.vb#8)]  
  
 <xref:System.ServiceModel.Syndication.UrlSyndicationContent> クラスを Atom 1.0 にシリアル化する方法を次の XML に示します。  
  
 `<content type="audio" src="http://someurl/" />`  
  
 XHTML コンテンツ付きの <xref:System.ServiceModel.Syndication.UrlSyndicationContent> クラスを RSS 2.0 にシリアル化する方法を次の XML に示します。  
  
 `<description />`  
  
 `<content type="audio" src="http://Contoso/someurl/" xmlns="http://www.w3.org/2005/Atom" />`  
  
## <a name="xmlsyndicationcontent"></a>XmlSyndicationContent  
 <xref:System.ServiceModel.Syndication.XmlSyndicationContent> クラスを Atom 1.0 および RSS 2.0 にシリアル化するコード例を次に示します。  
  
 [!code-csharp[SyndicationMapping#9](../../../../samples/snippets/csharp/VS_Snippets_CFX/syndicationmapping/cs/snippets.cs#9)]
 [!code-vb[SyndicationMapping#9](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/syndicationmapping/vb/snippets.vb#9)]  
  
 <xref:System.ServiceModel.Syndication.XmlSyndicationContent> クラスを Atom 1.0 にシリアル化する方法を次の XML に示します。  
  
 `<content type="mytype">`  
  
 `<SomeData xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.datacontract.org/2004/07/FeedMapping" />`  
  
 `</content>`  
  
 XHTML コンテンツ付きの <xref:System.ServiceModel.Syndication.XmlSyndicationContent> クラスを RSS 2.0 にシリアル化する方法を次の XML に示します。  
  
 `<content type="mytype" xmlns="http://www.w3.org/2005/Atom">`  
  
 `<SomeData xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.datacontract.org/2004/07/FeedMapping" />`  
  
 `</content>`  
  
## <a name="see-also"></a>関連項目

- [WCF 配信の概要](wcf-syndication-overview.md)
- [配信のアーキテクチャ](architecture-of-syndication.md)
- [方法: 基本的な RSS フィードを作成する](how-to-create-a-basic-rss-feed.md)
- [方法: 基本的な ATOM フィードを作成する](how-to-create-a-basic-atom-feed.md)
- [方法: Atom および RSS の両方としてフィードを公開する](how-to-expose-a-feed-as-both-atom-and-rss.md)
