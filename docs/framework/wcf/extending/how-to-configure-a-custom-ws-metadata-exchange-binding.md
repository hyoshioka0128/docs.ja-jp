---
title: '方法: カスタム WS-Metadata Exchange バインディングを構成する'
ms.date: 03/30/2017
helpviewer_keywords:
- WS-Metadata Exchange [WCF]
- WS-Metadata Exchange [WCF], configuring a custom binding
ms.assetid: cdba4d73-da64-4805-bc56-9822becfd1e4
ms.openlocfilehash: 6459e3f0cf0ab72af8027bd6802a0e7aa574aece
ms.sourcegitcommit: 1c1a1f9ec0bd1efb3040d86a79f7ee94e207cca5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/03/2020
ms.locfileid: "80635786"
---
# <a name="how-to-configure-a-custom-ws-metadata-exchange-binding"></a>方法: カスタム WS-Metadata Exchange バインディングを構成する

この記事では、カスタム WS メタデータエクスチェンジ バインディングを構成する方法について説明します。 Wcf (Wcf) には、システム定義のメタデータ バインディングが 4 つ含まれていますが、任意のバインドを使用してメタデータを公開できます。 この記事では、 を使用してメタデータを公開`wsHttpBinding`する方法について説明します。 このバインディングでは、メタデータをセキュリティで保護して公開することができます。 この記事のコードは、[作業の開始](../samples/getting-started-sample.md)に基づいています。  
  
### <a name="using-a-configuration-file"></a>構成ファイルの使用  
  
1. サービスの構成ファイルで、`serviceMetadata` タグを含んだサービス動作を追加します。  
  
    ```xml  
    <behaviors>  
       <serviceBehaviors>  
         <behavior name="CalculatorServiceBehavior">  
           <serviceMetadata httpGetEnabled="True"/>  
         </behavior>  
       </serviceBehaviors>  
    </behaviors>  
    ```  
  
2. この新しい動作を参照する `behaviorConfiguration` 属性をサービス タグに追加します。  
  
    ```xml  
    <service name="Microsoft.ServiceModel.Samples.CalculatorService"  
    behaviorConfiguration="CalculatorServiceBehavior" />
    ```  
  
3. メタデータ エンドポイントを追加し、アドレスに mex、バインディングに `wsHttpBinding`、コントラクトに <xref:System.ServiceModel.Description.IMetadataExchange> をそれぞれ指定します。  
  
    ```xml  
    <endpoint address="mex"  
              binding="wsHttpBinding"  
              contract="IMetadataExchange" />  
    ```  
  
4. メタデータ交換エンドポイントが正常に動作していることを確認するには、クライアント構成ファイルにエンドポイントタグを追加します。  
  
    ```xml  
    <endpoint name="MyMexEndpoint"               address="http://localhost:8000/servicemodelsamples/service/mex"  
              binding="wsHttpBinding"  
              contract="IMetadataExchange"/>  
    ```  
  
5. クライアントの Main() メソッドで、新しい <xref:System.ServiceModel.Description.MetadataExchangeClient> インスタンスを作成し、その <xref:System.ServiceModel.Description.MetadataExchangeClient.ResolveMetadataReferences%2A> プロパティを `true` に設定し、<xref:System.ServiceModel.Description.MetadataExchangeClient.GetMetadata%2A> を呼び出して返されるメタデータのコレクションを反復処理します。  
  
    ```csharp
    string mexAddress = "http://localhost:8000/servicemodelsamples/service/mex";  
  
    MetadataExchangeClient mexClient = new MetadataExchangeClient("MyMexEndpoint");  
    mexClient.ResolveMetadataReferences = true;  
    MetadataSet mdSet = mexClient.GetMetadata(new EndpointAddress(mexAddress));  
    foreach (MetadataSection section in mdSet.MetadataSections)  
    Console.WriteLine("Metadata section: " + section.Dialect.ToString());  
    ```  
  
### <a name="configuring-by-code"></a>コードによる構成  
  
1. <xref:System.ServiceModel.WSHttpBinding> バインディングのインスタンスを作成します。  
  
    ```csharp  
    WSHttpBinding binding = new WSHttpBinding();  
    ```  
  
2. <xref:System.ServiceModel.ServiceHost> インスタンスを作成します。  
  
    ```csharp  
    ServiceHost serviceHost = new ServiceHost(typeof(CalculatorService), baseAddress);  
    ```  
  
3. サービス エンドポイントと <xref:System.ServiceModel.Description.ServiceMetadataBehavior> インスタンスを追加します。  
  
    ```csharp  
    serviceHost.AddServiceEndpoint(typeof(ICalculator), binding, baseAddress);  
    ServiceMetadataBehavior smb = new ServiceMetadataBehavior();  
    smb.HttpGetEnabled = true;  
    serviceHost.Description.Behaviors.Add(smb);  
    ```  
  
4. 前に作成した <xref:System.ServiceModel.WSHttpBinding> を指定する Metadata Exchange エンドポイントを追加します。  
  
    ```csharp  
    serviceHost.AddServiceEndpoint(typeof(IMetadataExchange), binding, mexAddress);  
    ```  
  
5. Metadata Exchange エンドポイントが適切に動作することを確認するには、クライアントの構成ファイルにエンドポイント タグを追加します。  
  
    ```xml  
    <endpoint name="MyMexEndpoint"               address="http://localhost:8000/servicemodelsamples/service/mex"  
              binding="wsHttpBinding"  
              contract="IMetadataExchange"/>  
    ```  
  
6. クライアントの Main() メソッドで、新しい <xref:System.ServiceModel.Description.MetadataExchangeClient> インスタンスを作成し、その <xref:System.ServiceModel.Description.MetadataExchangeClient.ResolveMetadataReferences%2A> プロパティを `true` に設定し、<xref:System.ServiceModel.Description.MetadataExchangeClient.GetMetadata%2A> を呼び出して返されるメタデータのコレクションを反復処理します。  
  
    ```csharp  
    string mexAddress = "http://localhost:8000/servicemodelsamples/service/mex";  
  
    MetadataExchangeClient mexClient = new MetadataExchangeClient("MyMexEndpoint");  
    mexClient.ResolveMetadataReferences = true;  
    MetadataSet mdSet = mexClient.GetMetadata(new EndpointAddress(mexAddress));  
    foreach (MetadataSection section in mdSet.MetadataSections)  
    Console.WriteLine("Metadata section: " + section.Dialect.ToString());  
    ```  
  
## <a name="see-also"></a>関連項目

- [メタデータ公開動作](../samples/metadata-publishing-behavior.md)
- [メタデータの抽出](../samples/retrieve-metadata.md)
- [Metadata](../feature-details/metadata.md)
- [メタデータの公開](../feature-details/publishing-metadata.md)
- [メタデータ エンドポイントを公開する](../publishing-metadata-endpoints.md)
