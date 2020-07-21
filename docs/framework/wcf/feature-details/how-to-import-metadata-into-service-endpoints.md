---
title: '方法: メタデータをサービス エンドポイントにインポートする'
ms.date: 03/30/2017
ms.assetid: b69dbe20-92a1-4911-89d8-ffbc3dad4663
ms.openlocfilehash: 1de316b8e91739d5e3e24ff960e2cdfb33cc7fab
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84597060"
---
# <a name="how-to-import-metadata-into-service-endpoints"></a>方法: メタデータをサービス エンドポイントにインポートする
このトピックでは、サービスエンドポイントのコレクションにメタデータをインポートし、[はじめに](../samples/getting-started-sample.md)で定義されているサービスを使用する方法について説明します。 また、サービスからメタデータをインポートし、次にそのサービスに対して `Add` メソッドを呼び出すクライアント アプリケーションを作成する方法についても説明します。  
  
### <a name="to-import-metadata-into-service-endpoints"></a>メタデータをサービス エンドポイントにインポートするには  
  
1. <xref:System.ServiceModel.EndpointAddress> オブジェクトを定義し、サービスの metadata exchange (MEX) アドレスの URI (Uniform Resource Identifier) を使ってそのオブジェクトを初期化します。  
  
     [!code-csharp[UE_ImportMetadata#0](../../../../samples/snippets/csharp/VS_Snippets_CFX/ue_importmetadata/cs/client.cs#0)]  
  
2. <xref:System.ServiceModel.Description.MetadataExchangeClient> を作成し、MEX アドレスを渡して <xref:System.ServiceModel.Description.MetadataExchangeClient.GetMetadata%2A> を呼び出します。 これにより、メタデータをサービスから取得します。  
  
     [!code-csharp[UE_ImportMetadata#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/ue_importmetadata/cs/client.cs#1)]  
  
3. <xref:System.ServiceModel.Description.WsdlImporter> を作成し、前に取得したメタデータを渡して <xref:System.ServiceModel.Description.WsdlImporter.ImportAllContracts%2A> を呼び出します。 これにより、<xref:System.ServiceModel.Description.ContractDescription> オブジェクトのコレクションを生成します。 必要に応じて、<xref:System.ServiceModel.Description.WsdlImporter.ImportAllEndpoints%2A> または <xref:System.ServiceModel.Description.WsdlImporter.ImportAllBindings%2A> を呼び出すこともできます。  
  
     [!code-csharp[UE_ImportMetadata#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/ue_importmetadata/cs/client.cs#2)]  
  
    > [!NOTE]
    > メタデータのインポートが完了すると、クライアント チャネルの作成もメタデータのエクスポートもできなくなります。 これは、この時点で型情報を使用できないためです。 型情報は、サービスと実際に対話する場合またはメタデータをエクスポートする場合に必要です。 型情報を生成するには、コードを生成する必要があります。これについては、手順 4. ～ 5. で説明します。 別の方法として、<xref:System.ServiceModel.Description.MetadataResolver> ヘルパー クラスを使用することもできます。 詳細については、「[方法: MetadataResolver を使用してバインディングメタデータを動的に取得する](how-to-use-metadataresolver-to-obtain-binding-metadata-dynamically.md)」を参照してください。  
  
4. 各コントラクトに型情報を生成します。  
  
     [!code-csharp[UE_ImportMetadata#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/ue_importmetadata/cs/client.cs#3)]  
  
5. これで、この情報を使用できます。 次の例では、C# ソース コードが生成されます。  
  
     [!code-csharp[UE_ImportMetadata#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/ue_importmetadata/cs/client.cs#4)]  
  
## <a name="see-also"></a>関連項目

- [Metadata](metadata.md)
- [はじめに](../samples/getting-started-sample.md)
