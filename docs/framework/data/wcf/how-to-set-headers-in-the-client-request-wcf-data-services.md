---
title: '方法: クライアント要求のヘッダーを設定する (WCF Data Services)'
description: SendingRequest イベントを処理し、要求メッセージを WCF Data Services のデータ サービスに送信する前に新しいヘッダーを要求メッセージに追加する方法について説明します。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WCF Data Services, customizing requests
ms.assetid: 3d55168d-5901-4f48-8117-6c93da3ab5ae
ms.openlocfilehash: fab1fcfdf92d275f51f433845aa0c253a00ec99d
ms.sourcegitcommit: 358a28048f36a8dca39a9fe6e6ac1f1913acadd5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85247766"
---
# <a name="how-to-set-headers-in-the-client-request-wcf-data-services"></a>方法: クライアント要求のヘッダーを設定する (WCF Data Services)
WCF Data Services クライアント ライブラリを使用して、Open Data Protocol (OData) をサポートするデータ サービスにアクセスする場合、クライアント ライブラリにより、データ サービスに送信される要求メッセージに必要な HTTP ヘッダーが自動的に設定されます。 ただし、クライアント ライブラリでは、データ サービスがクレーム ベース認証やクッキーを要求する場合など、特定の場合に必要とされるメッセージ ヘッダーを設定することはできません。 詳細については、「 [Securing WCF Data Services](securing-wcf-data-services.md#clientAuthentication)」を参照してください。 このような場合は、要求メッセージを送信する前にそのメッセージ ヘッダーを手動で設定する必要があります。 このトピックの例では、<xref:System.Data.Services.Client.DataServiceContext.SendingRequest> イベントを処理して、要求メッセージをデータ サービスに送信する前に新しいヘッダーを要求メッセージに追加する方法を示します。  
  
 このトピックの例では、Northwind サンプル データ サービスおよび自動生成されたクライアント データ サービス クラスを使用します。 このサービスとクライアント データ クラスは、「[WCF Data Services クイックスタート](quickstart-wcf-data-services.md)」を完了すると作成されます。 OData の Web サイトで公開されている [Northwind サンプル データ サービス](https://services.odata.org/Northwind/Northwind.svc/)を使用することもできます。このサンプル データ サービスは読み取り専用で、変更を保存しようとするとエラーが返されます。 OData の Web サイトのサンプル データ サービスでは、匿名認証が許可されます。  
  
## <a name="example"></a>例  
 次の例では、<xref:System.Data.Services.Client.DataServiceContext.SendingRequest> イベントのハンドラーを登録し、データ サービスに対してクエリを実行します。  
  
> [!NOTE]
> 要求ごとにメッセージ ヘッダーを手動で設定することがデータ サービスで必要とされる場合は、データ サービスを表すエンティティ コンテナー (この場合は <xref:System.Data.Services.Client.DataServiceContext.SendingRequest>) で `OnContextCreated` 部分メソッドをオーバーライドして、`NorthwindEntities` イベントのハンドラーを登録することを検討してください。  
  
[!code-csharp[Astoria Northwind Client#RegisterHeadersQuery](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#registerheadersquery)]
[!code-vb[Astoria Northwind Client#RegisterHeadersQuery](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#registerheadersquery)]
  
## <a name="example"></a>例  
 次のメソッドは、<xref:System.Data.Services.Client.DataServiceContext.SendingRequest> イベントを処理し、認証ヘッダーを要求に追加します。  
  
 [!code-csharp[Astoria Northwind Client#OnSendingRequest](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#onsendingrequest)]  
 [!code-vb[Astoria Northwind Client#OnSendingRequest](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#onsendingrequest)]  
  
## <a name="see-also"></a>関連項目

- [WCF Data Services のセキュリティ保護](securing-wcf-data-services.md)
- [WCF Data Services クライアント ライブラリ](wcf-data-services-client-library.md)
