---
title: '方法: Atom および RSS の両方としてフィードを公開する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: fe374932-67f5-487d-9325-f868812b92e4
ms.openlocfilehash: e4ce1fa7b494c2317a1bddc57ee6b150c84b9a96
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84593147"
---
# <a name="how-to-expose-a-feed-as-both-atom-and-rss"></a>方法: Atom および RSS の両方としてフィードを公開する
Windows Communication Foundation (WCF) を使用すると、配信フィードを公開するサービスを作成できます。 このトピックでは、Atom 1.0 と RSS 2.0 の両方を使用して配信フィードを公開する配信サービスを作成する方法について説明します。 このサービスは、どちらかの配信フォーマットを返すエンドポイントを公開します。 簡略化のため、この例で使用するサービスは自己ホスト型です。 運用環境では、このタイプのサービスは IIS または WAS でホストされます。 さまざまな WCF ホスティングオプションの詳細については、「[ホスティング](hosting.md)」を参照してください。  
  
### <a name="to-create-a-basic-syndication-service"></a>基本的な配信サービスを作成するには  
  
1. <xref:System.ServiceModel.Web.WebGetAttribute> 属性でマークされたインターフェイスを使用して、サービス コントラクトを定義します。 配信フィードとして公開される各操作は、<xref:System.ServiceModel.Syndication.SyndicationFeedFormatter> オブジェクトを返します。 <xref:System.ServiceModel.Web.WebGetAttribute> のパラメーターに注意してください。 `UriTemplate` は、このサービス操作を呼び出すために使用される URL を指定します。 このパラメーターの文字列には、リテラルと変数が中かっこ ({*format*}) で格納されています。 この変数は、サービス操作の `format` パラメーターに対応します。 詳細については、「<xref:System.UriTemplate>」を参照してください。 `BodyStyle` は、このサービス操作が送受信するメッセージの書き方に影響を与えます。 <xref:System.ServiceModel.Web.WebMessageBodyStyle.Bare> は、このサービス操作に送受信されるデータが、インフラストラクチャにより定義された XML 要素でラップされないことを指定します。 詳細については、「<xref:System.ServiceModel.Web.WebMessageBodyStyle>」を参照してください。  
  
     [!code-csharp[htAtomRss#0](../../../../samples/snippets/csharp/VS_Snippets_CFX/htatomrss/cs/program.cs#0)]
     [!code-vb[htAtomRss#0](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htatomrss/vb/program.vb#0)]  
  
    > [!NOTE]
    > このインターフェイスのサービス操作により返される型を指定するには、<xref:System.ServiceModel.ServiceKnownTypeAttribute> を使用します。  
  
2. サービス コントラクトを実装します。  
  
     [!code-csharp[htAtomRss#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/htatomrss/cs/program.cs#1)]
     [!code-vb[htAtomRss#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htatomrss/vb/program.vb#1)]  
  
3. <xref:System.ServiceModel.Syndication.SyndicationFeed> オブジェクトを作成し、作成者、カテゴリ、および説明を追加します。  
  
     [!code-csharp[htAtomRss#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/htatomrss/cs/program.cs#2)]
     [!code-vb[htAtomRss#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htatomrss/vb/program.vb#2)]  
  
4. 複数の <xref:System.ServiceModel.Syndication.SyndicationItem> オブジェクトを作成します。  
  
     [!code-csharp[htAtomRss#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/htatomrss/cs/program.cs#3)]
     [!code-vb[htAtomRss#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htatomrss/vb/program.vb#3)]  
  
5. <xref:System.ServiceModel.Syndication.SyndicationItem> オブジェクトをフィードに追加します。  
  
     [!code-csharp[htAtomRss#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/htatomrss/cs/program.cs#4)]
     [!code-vb[htAtomRss#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htatomrss/vb/program.vb#4)]  
  
6. format パラメーターを使用して、要求された形式を返します。  
  
     [!code-csharp[htAtomRss#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/htatomrss/cs/program.cs#5)]
     [!code-vb[htAtomRss#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htatomrss/vb/program.vb#5)]  
  
### <a name="to-host-the-service"></a>サービスをホストするには  
  
1. <xref:System.ServiceModel.Web.WebServiceHost> オブジェクトを作成します。 <xref:System.ServiceModel.Web.WebServiceHost> クラスは、エンドポイントがコードまたは構成で指定されない限り、自動的にエンドポイントをサービスのベース アドレスで追加します。 次の例は、既定のエンドポイントが公開されるので、エンドポイントは指定されません。  
  
     [!code-csharp[htAtomRss#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/htatomrss/cs/program.cs#6)]
     [!code-vb[htAtomRss#6](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htatomrss/vb/program.vb#6)]  
  
2. サービス ホストを開き、サービスからフィードを読み込み、フィードを表示してから、ユーザーが Enter キーを押すのを待ちます。  
  
     [!code-csharp[htAtomRss#8](../../../../samples/snippets/csharp/VS_Snippets_CFX/htatomrss/cs/program.cs#8)]
     [!code-vb[htAtomRss#8](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htatomrss/vb/program.vb#8)]  
  
### <a name="to-call-getblog-with-an-http-get"></a>HTTP GET を使用して GetBlog を呼び出すには  
  
1. Internet Explorer を開き、次の URL を入力して、enter キーを押します `http://localhost:8000/BlogService/GetBlog` 。
  
     URL には、サービスのベースアドレス ( `http://localhost:8000/BlogService` )、エンドポイントの相対アドレス、および呼び出すサービス操作が含まれます。  
  
### <a name="to-call-getblog-from-code"></a>コードから GetBlog() を呼び出すには  
  
1. ベース アドレスと呼び出すメソッドを使用して <xref:System.Xml.XmlReader> を作成します。  
  
     [!code-csharp[htAtomRss#9](../../../../samples/snippets/csharp/VS_Snippets_CFX/htatomrss/cs/snippets.cs#9)]
     [!code-vb[htAtomRss#9](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htatomrss/vb/snippets.vb#9)]  
  
2. 静的な <xref:System.ServiceModel.Syndication.SyndicationFeed.Load%28System.Xml.XmlReader%29> メソッドを呼び出し、作成した <xref:System.Xml.XmlReader> を渡します。  
  
     [!code-csharp[htAtomRss#10](../../../../samples/snippets/csharp/VS_Snippets_CFX/htatomrss/cs/snippets.cs#10)]
     [!code-vb[htAtomRss#10](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htatomrss/vb/snippets.vb#10)]  
  
     これにより、サービス操作が呼び出され、サービス操作から返されたフォーマッタが新しい <xref:System.ServiceModel.Syndication.SyndicationFeed> に設定されます。  
  
3. フィード オブジェクトにアクセスします。  
  
     [!code-csharp[htAtomRss#11](../../../../samples/snippets/csharp/VS_Snippets_CFX/htatomrss/cs/snippets.cs#11)]
     [!code-vb[htAtomRss#11](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htatomrss/vb/snippets.vb#11)]  
  
## <a name="example"></a>例  
 この例の完全なコードの一覧を以下に示します。  
  
 [!code-csharp[htAtomRss#12](../../../../samples/snippets/csharp/VS_Snippets_CFX/htatomrss/cs/program.cs#12)]  
  
## <a name="compiling-the-code"></a>コードのコンパイル  
 上記のコードのコンパイル時には、System.ServiceModel.dll と System.ServiceModel.Web.dll が参照されます。  
  
## <a name="see-also"></a>関連項目

- <xref:System.ServiceModel.WebHttpBinding>
- <xref:System.ServiceModel.Web.WebGetAttribute>
