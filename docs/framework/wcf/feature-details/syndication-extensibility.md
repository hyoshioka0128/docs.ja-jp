---
title: 配信の拡張
ms.date: 03/30/2017
ms.assetid: 4d941175-74a2-4b15-81b3-086e8a95d25f
ms.openlocfilehash: 5e8f47b45897f46e15847c793c986e953523e66b
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84600725"
---
# <a name="syndication-extensibility"></a>配信の拡張
配信 API は、形式に依存せず、さまざま形式で概要コンテンツをネットワークに書き込むことができるプログラミング モデルを提供することを目的としています。 抽象データ モデルは、次のクラスで構成されています。  
  
- <xref:System.ServiceModel.Syndication.SyndicationCategory>  
  
- <xref:System.ServiceModel.Syndication.SyndicationFeed>  
  
- <xref:System.ServiceModel.Syndication.SyndicationItem>  
  
- <xref:System.ServiceModel.Syndication.SyndicationLink>  
  
- <xref:System.ServiceModel.Syndication.SyndicationPerson>  
  
 これらのクラスは、一部の名前が異なっていますが、Atom 1.0 仕様に規定されるコンストラクトに厳密にマップされています。  
  
 配信プロトコルの主な機能は拡張性です。 Atom 1.0 と RSS 2.0 のどちらも、仕様で定義されていない属性と要素を配信フィードに追加できます。 Windows Communication Foundation (WCF) 配信プログラミングモデルには、カスタム属性と拡張機能の操作、緩やかに型指定されたアクセス、および新しいクラスの派生を行うための次の方法が用意されています。  
  
## <a name="loosely-typed-access"></a>弱い型指定のアクセス  
 新しいクラスの派生によって拡張機能を追加するには、追加のコードを記述する必要があります。 別の方法として、弱い型指定で拡張機能にアクセスする方法もあります。 配信抽象データ モデルに定義される型にはすべて、`AttributeExtensions` および `ElementExtensions` という名前のプロパティが含まれます。ただし、<xref:System.ServiceModel.Syndication.SyndicationContent> には `AttributeExtensions` プロパティがありますが、`ElementExtensions` プロパティはありません。 この 2 つのプロパティはそれぞれ、`TryParseAttribute` メソッドと `TryParseElement` メソッドで処理されない拡張機能のコレクションです。 この処理されない拡張機能にアクセスするには、<xref:System.ServiceModel.Syndication.SyndicationElementExtensionCollection.ReadElementExtensions%2A?displayProperty=nameWithType>、`ElementExtensions`、<xref:System.ServiceModel.Syndication.SyndicationFeed>、<xref:System.ServiceModel.Syndication.SyndicationItem>、および <xref:System.ServiceModel.Syndication.SyndicationLink> の <xref:System.ServiceModel.Syndication.SyndicationPerson> プロパティで <xref:System.ServiceModel.Syndication.SyndicationCategory> を呼び出します。 このメソッドのセットは、指定した名前と名前空間を持つ拡張機能をすべて検索し、個別に `TExtension` のインスタンスに逆シリアル化して `TExtension` オブジェクトのコレクションとして返します。  
  
## <a name="deriving-a-new-class"></a>新しいクラスの派生  
 任意の既存抽象データ モデル クラスから、新しいクラスを派生できます。 これは、対象フィードのほとんどに特定の拡張機能が含まれるアプリケーションを実装する際に行います。 このトピックでは、プログラムで処理するフィードのほとんどに、`MyExtension` 拡張機能が含まれています。 プログラミング性を向上するには、次の手順を実行します。  
  
- 拡張機能データを保持するクラスを作成します。 この場合、MyExtension というクラスを作成します。  
  
- プログラミング性を向上するには、<xref:System.ServiceModel.Syndication.SyndicationItem> から MyExtensionItem というクラスを派生させ、MyExtension 型のプロパティを公開します。  
  
- MyExtensionItem クラスの <xref:System.ServiceModel.Syndication.SyndicationItem.TryParseElement%28System.Xml.XmlReader%2CSystem.String%29> をオーバーライドし、MyExtension が読み込まれたら新しい MyExtension インスタンスをインスタンス化します。  
  
- MyExtensionItem クラスの <xref:System.ServiceModel.Syndication.SyndicationItem.WriteElementExtensions%28System.Xml.XmlWriter%2CSystem.String%29> をオーバーライドし、MyExtension プロパティのコンテンツを XML ライターに書き出します。  
  
- <xref:System.ServiceModel.Syndication.SyndicationFeed> から、MyExtensionFeed というクラスを派生させます。  
  
- MyExtensionFeed クラスの <xref:System.ServiceModel.Syndication.SyndicationFeed.CreateItem> をオーバーライドし、既定の <xref:System.ServiceModel.Syndication.SyndicationItem> の代わりに MyExtensionItem をインスタンス化します。 <xref:System.ServiceModel.Syndication.SyndicationFeed> および <xref:System.ServiceModel.Syndication.SyndicationItem> に、<xref:System.ServiceModel.Syndication.SyndicationLink>、<xref:System.ServiceModel.Syndication.SyndicationCategory>、および <xref:System.ServiceModel.Syndication.SyndicationPerson> の各オブジェクトを生成する一連のメソッドが定義されます (たとえば、<xref:System.ServiceModel.Syndication.SyndicationFeed.CreateLink>、<xref:System.ServiceModel.Syndication.SyndicationFeed.CreateCategory>、<xref:System.ServiceModel.Syndication.SyndicationFeed.CreatePerson> など)。 そのどれもが、カスタム派生クラスを作成するためにオーバーライドできます。  
  
## <a name="see-also"></a>関連項目

- [WCF 配信の概要](wcf-syndication-overview.md)
- [配信のアーキテクチャ](architecture-of-syndication.md)
