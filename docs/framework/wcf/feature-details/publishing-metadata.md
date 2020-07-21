---
title: メタデータの公開
description: 1つ以上のメタデータエンドポイントを公開して WCF サービスがメタデータを公開する方法を説明します。これにより、標準プロトコルを使用してメタデータを使用できるように
ms.date: 03/30/2017
helpviewer_keywords:
- metadata [WCF], publishing
ms.assetid: 3a56831a-cabc-45c0-bd02-12e2e9bd7313
ms.openlocfilehash: 2aa6d877db4e5b09b4c594e6e87b63fb6c04703b
ms.sourcegitcommit: 358a28048f36a8dca39a9fe6e6ac1f1913acadd5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85244960"
---
# <a name="publishing-metadata"></a>メタデータの公開
Windows Communication Foundation (WCF) サービスは、1つまたは複数のメタデータエンドポイントを公開することによってメタデータを公開します。 サービス メタデータを公開すると、そのメタデータで WS-MetadataExchange (MEX) や HTTP/GET 要求などの標準化プロトコルを使用できるようになります。 メタデータのエンドポイントはアドレス、バインディング、コントラクトを持つ他のサービス エンドポイントに類似し、それらは構成か命令コードを使用してサービス ホストに追加することができます。  
  
## <a name="publishing-metadata-endpoints"></a>メタデータ エンドポイントを公開する  
 WCF サービスのメタデータエンドポイントを公開するには、まずサービスの動作をサービスに追加する必要があり <xref:System.ServiceModel.Description.ServiceMetadataBehavior> ます。 <xref:System.ServiceModel.Description.ServiceMetadataBehavior?displayProperty=nameWithType> インスタンスを追加すると、サービスからメタデータ エンドポイントを公開できます。 <xref:System.ServiceModel.Description.ServiceMetadataBehavior?displayProperty=nameWithType> サービス動作を追加すると、MEX プロトコルをサポートするメタデータ エンドポイント、または HTTP/GET 要求に応答するメタデータ エンドポイントを公開できます。  
  
 <xref:System.ServiceModel.Description.ServiceMetadataBehavior?displayProperty=nameWithType> は <xref:System.ServiceModel.Description.WsdlExporter> を使用して、サービス内のすべてのサービス エンドポイント用のメタデータをエクスポートします。 サービスからメタデータをエクスポートする方法の詳細については、「[メタデータのエクスポートとインポート](exporting-and-importing-metadata.md)」を参照してください。  
  
 <xref:System.ServiceModel.Description.ServiceMetadataBehavior?displayProperty=nameWithType> は、<xref:System.ServiceModel.Description.ServiceMetadataExtension> インスタンスをサービス ホストへの拡張として追加します。 <xref:System.ServiceModel.Description.ServiceMetadataExtension?displayProperty=nameWithType> により、メタデータ公開プロトコルを実装することができます。 また、<xref:System.ServiceModel.Description.ServiceMetadataExtension?displayProperty=nameWithType> を使用して、<xref:System.ServiceModel.Description.ServiceMetadataExtension.Metadata%2A?displayProperty=nameWithType> プロパティにアクセスすることにより、実行時にサービスのメタデータを取得できます。  
  
### <a name="mex-metadata-endpoints"></a>MEX メタデータ エンドポイント  
 MEX プロトコルを使用するメタデータ エンドポイントを追加するには、`IMetadataExchange` サービス コントラクトを使用するサービス エンドポイントをサービス ホストに追加します。 WCF には、 <xref:System.ServiceModel.Description.IMetadataExchange> wcf プログラミングモデルの一部として使用できるこのサービスコントラクト名を持つインターフェイスが含まれています。 Ws-metadataexchange エンドポイント (MEX エンドポイント) は、4つの既定のバインディングのいずれかを使用できます。このバインディングは、静的ファクトリメソッドがクラスに公開し、 <xref:System.ServiceModel.Description.MetadataExchangeBindings> WCF ツールが使用する既定のバインディング (Svcutil.exe など) と一致させます。 また、独自のカスタム バインドを使用して MEX メタデータ エンドポイントを構成することもできます。  
  
### <a name="http-get-metadata-endpoints"></a>HTTP GET メタデータ エンドポイント  
 HTTP/GET 要求に応答するメタデータ エンドポイントをサービスに追加するには、<xref:System.ServiceModel.Description.ServiceMetadataBehavior.HttpGetEnabled%2A> の <xref:System.ServiceModel.Description.ServiceMetadataBehavior?displayProperty=nameWithType> プロパティを `true` に設定します。 また、<xref:System.ServiceModel.Description.ServiceMetadataBehavior.HttpsGetEnabled%2A> の <xref:System.ServiceModel.Description.ServiceMetadataBehavior?displayProperty=nameWithType> プロパティを `true` に設定することで、HTTPS を使用するメタデータ エンドポイントを構成することもできます。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [方法: 構成ファイルを使用してサービスのメタデータを公開する](how-to-publish-metadata-for-a-service-using-a-configuration-file.md)  
 クライアントがクエリ文字列を使用して Ws-metadataexchange または HTTP/GET 要求を使用してメタデータを取得できるように、メタデータを公開するように WCF サービスを構成する方法を示し `?wsdl` ます。  
  
 [方法: コードを使用してサービスのメタデータを公開する](how-to-publish-metadata-for-a-service-using-code.md)  
 WCF サービスのメタデータ公開をコードで有効にし、クライアントがクエリ文字列を使用して Ws-metadataexchange または HTTP/GET 要求を使用してメタデータを取得できるようにする方法を示し `?wsdl` ます。  
  
## <a name="reference"></a>関連項目  
 <xref:System.ServiceModel.Description.ServiceMetadataBehavior>  
  
 <xref:System.ServiceModel.Description.IMetadataExchange>  
  
 <xref:System.ServiceModel.Description.ServiceMetadataExtension>  
  
 <xref:System.ServiceModel.Description.MetadataExchangeBindings>  
  
## <a name="see-also"></a>関連項目

- [メタデータのエクスポートとインポート](exporting-and-importing-metadata.md)
