---
title: '方法: 基本的な RSS フィードを作成する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 431879b8-a5f8-4947-ad1e-4768c726aca8
ms.openlocfilehash: 872fe325a6705e79d026cd7f6e1f7cfef5145307
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84599023"
---
# <a name="how-to-create-a-basic-rss-feed"></a>方法: 基本的な RSS フィードを作成する
Windows Communication Foundation (WCF) を使用すると、配信フィードを公開するサービスを作成できます。 ここでは、RSS 配信フィードを公開する配信サービスを作成する方法について説明します。  
  
### <a name="to-create-a-basic-syndication-service"></a>基本的な配信サービスを作成するには  
  
1. <xref:System.ServiceModel.Web.WebGetAttribute> 属性でマークされたインターフェイスを使用して、サービス コントラクトを定義します。 配信フィードとして公開される各操作は、<xref:System.ServiceModel.Syndication.Rss20FeedFormatter> オブジェクトを返す必要があります。  
  
     [!code-csharp[htRssBasic#0](../../../../samples/snippets/csharp/VS_Snippets_CFX/htrssbasic/cs/program.cs#0)]
     [!code-vb[htRssBasic#0](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htrssbasic/vb/program.vb#0)]  
  
    > [!NOTE]
    > <xref:System.ServiceModel.Web.WebGetAttribute> 属性を適用するすべてのサービス操作は、HTTP GET 要求にマッピングされます。 他の HTTP メソッドに操作をマッピングするには、代わりに <xref:System.ServiceModel.Web.WebInvokeAttribute> を使用します。 詳細については、「[方法: 基本的な WCF WEB HTTP サービスを作成](how-to-create-a-basic-wcf-web-http-service.md)する」を参照してください。  
  
2. サービス コントラクトを実装します。  
  
     [!code-csharp[htRssBasic#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/htrssbasic/cs/program.cs#1)]
     [!code-vb[htRssBasic#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htrssbasic/vb/program.vb#1)]  
  
3. <xref:System.ServiceModel.Syndication.SyndicationFeed> オブジェクトを作成し、作成者、カテゴリ、および説明を追加します。  
  
     [!code-csharp[htRssBasic#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/htrssbasic/cs/program.cs#2)]
     [!code-vb[htRssBasic#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htrssbasic/vb/program.vb#2)]  
  
4. 複数の <xref:System.ServiceModel.Syndication.SyndicationItem> オブジェクトを作成します。  
  
     [!code-csharp[htRssBasic#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/htrssbasic/cs/program.cs#3)]
     [!code-vb[htRssBasic#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htrssbasic/vb/program.vb#3)]  
  
5. <xref:System.ServiceModel.Syndication.SyndicationItem> をフィードに追加します。  
  
     [!code-csharp[htRssBasic#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/htrssbasic/cs/program.cs#4)]
     [!code-vb[htRssBasic#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htrssbasic/vb/program.vb#4)]  
  
6. フィードを返します。  
  
     [!code-csharp[htRssBasic#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/htrssbasic/cs/program.cs#5)]
     [!code-vb[htRssBasic#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htrssbasic/vb/program.vb#5)]  
  
### <a name="to-host-a-service"></a>サービスをホストするには  
  
1. <xref:System.ServiceModel.Web.WebServiceHost> オブジェクトを作成します。  
  
     [!code-csharp[htRssBasic#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/htrssbasic/cs/program.cs#6)]
     [!code-vb[htRssBasic#6](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htrssbasic/vb/program.vb#6)]  
  
2. サービス ホストを開き、ユーザーが Enter キーを押すのを待ちます。  
  
     [!code-csharp[htRssBasic#8](../../../../samples/snippets/csharp/VS_Snippets_CFX/htrssbasic/cs/program.cs#8)]
     [!code-vb[htRssBasic#8](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htrssbasic/vb/program.vb#8)]  
  
### <a name="to-call-getblog-with-an-http-get"></a>HTTP GET で GetBlog() を呼び出すには  
  
1. Internet Explorer を開き、次の URL を入力して、enter キーを押します `http://localhost:8000/BlogService/GetBlog` 。 URL には、サービスのベースアドレス ( `http://localhost:8000/BlogService` )、エンドポイントの相対アドレス、および呼び出すサービス操作が含まれます。  
  
### <a name="to-call-getblog-from-code"></a>コードから GetBlog() を呼び出すには  
  
1. ベース アドレスと呼び出すメソッドを使用して <xref:System.Xml.XmlReader> を作成します。  
  
     [!code-csharp[htRssBasic#9](../../../../samples/snippets/csharp/VS_Snippets_CFX/htrssbasic/cs/snippets.cs#9)]
     [!code-vb[htRssBasic#9](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htrssbasic/vb/snippets.vb#9)]  
  
2. 静的な <xref:System.ServiceModel.Syndication.SyndicationFeed.Load%28System.Xml.XmlReader%29> メソッドを呼び出し、作成した <xref:System.Xml.XmlReader> を渡します。  
  
     [!code-csharp[htRssBasic#10](../../../../samples/snippets/csharp/VS_Snippets_CFX/htrssbasic/cs/snippets.cs#10)]
     [!code-vb[htRssBasic#10](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htrssbasic/vb/snippets.vb#10)]  
  
     これにより、サービス操作が呼び出され、サービス操作から返されたフォーマッタが新しい <xref:System.ServiceModel.Syndication.SyndicationFeed> に設定されます。  
  
3. フィード オブジェクトにアクセスします。  
  
     [!code-csharp[htRssBasic#11](../../../../samples/snippets/csharp/VS_Snippets_CFX/htrssbasic/cs/snippets.cs#11)]
     [!code-vb[htRssBasic#11](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htrssbasic/vb/snippets.vb#11)]  
  
## <a name="example"></a>例  
 この例の完全なコードの一覧を以下に示します。  
  
 [!code-csharp[htRssBasic#12](../../../../samples/snippets/csharp/VS_Snippets_CFX/htrssbasic/cs/program.cs#12)]
 [!code-vb[htRssBasic#12](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htrssbasic/vb/program.vb#12)]  
  
## <a name="compiling-the-code"></a>コードのコンパイル  
 上記のコードのコンパイル時には、System.ServiceModel.dll と System.ServiceModel.Web.dll が参照されます。  
  
## <a name="see-also"></a>関連項目

- <xref:System.ServiceModel.WebHttpBinding>
- <xref:System.ServiceModel.Web.WebGetAttribute>
