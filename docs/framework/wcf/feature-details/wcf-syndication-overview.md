---
title: WCF 配信の概要
ms.date: 03/30/2017
ms.assetid: af6d4c39-e5e8-4099-aee6-5261feff9107
ms.openlocfilehash: 4f72a6d797f195108401a361cc73d74d309d5602
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84600959"
---
# <a name="wcf-syndication-overview"></a>WCF 配信の概要
Windows Communication Foundation (WCF) は、WCF サービスから配信フィードを公開するためのサポートを提供します。 配信は、サーバーがフィードと呼ばれる相互運用可能な形式でアプリケーション データの一部を公開するためのアプリケーション統合の機構です。 フィードはアプリケーション データのコレクションであり、フィード レベルのメタデータ (タイトル、作成者、URL、およびその他のメタデータ) と一連のフィード アイテムから構成されます。 フィード内で、フィード アイテムは通常、発生の逆順に並べられます。 フィード アイテムは、アイテム レベルのメタデータの標準セット (タイトル、URL、作成日時、カテゴリ、およびその他のアイテム レベルのメタデータ) と任意の大きさのアプリケーション固有のデータから構成されます。 最も一般的な2種類の配信フィードは、非常に単純な配信 (RSS) 2.0 と Atom 1.0 です。どちらも WCF でサポートされています。  
  
## <a name="object-model"></a>オブジェクト モデル  
 WCF は、フィード、フィードアイテム、および関連するメタデータを形式に依存しない方法 <xref:System.ServiceModel.Syndication.SyndicationFeed> (、、 <xref:System.ServiceModel.Syndication.SyndicationItem> <xref:System.ServiceModel.Syndication.SyndicationPerson> 、 <xref:System.ServiceModel.Syndication.SyndicationLink> 、およびその他の配信固有のクラス) で使用できるようにする、配信固有のクラスのセットを定義します。 WCF は、WCF REST プログラミングモデル上に構築されるインフラストラクチャクラスも定義します。これは、、およびなどの配信をサポートするためのものです <xref:System.ServiceModel.Syndication.Atom10FeedFormatter> <xref:System.ServiceModel.Syndication.Rss20FeedFormatter> 。 フィード フォーマッタ クラスは、オブジェクト モデルの RSS 2.0 と Atom 1.0 に対する双方向のシリアル化をサポートしています。  
  
## <a name="scenarios"></a>シナリオ  
 現在、配信はブログで広く使用されています。ブログの作成者は、さまざまな種類の情報を定期的に公開します。 たとえば、文字、画像、音声などの情報です。 多くの新聞や雑誌でも、配信を使用してニュースや記事を公開しています。 このようなフィードを定期受信することで、ユーザーはこれらのサイトから発信されるすべての最新情報を得ることができます。 配信は一般的にブログや出版社で使用されますが、一連の情報を公開する任意のアプリケーションで使用することもできます。たとえば、配信フィードを使用したバグ データベースの公開が考えられます。 という操作を公開する WCF サービスを作成でき `CodeDefects` ます。 この操作では、調べたいバグを報告した人の電子メール アドレスを指定するパラメーターを使用できます。 クライアントは、次の URL を使用して操作を呼び出すことができ `http://someserver/bugDatabase/CodeDefects?user=johndoe` ます。  
  
## <a name="syndication-formats"></a>配信フォーマット  
 WCF 配信プラットフォームでは、RSS 2.0 と Atom 1.0 がサポートされています。  
  
## <a name="see-also"></a>関連項目

- [WCF Web HTTP プログラミング モデル](wcf-web-http-programming-model.md)
