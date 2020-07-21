---
title: クライアントの動作の構成
description: WCF が動作を構成する2つの方法について説明します。これは、アプリケーション構成ファイルまたは呼び出し元アプリケーションからプログラムによって実行されます。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: df5b32fa-e73b-4e8e-b66f-357c748e0173
ms.openlocfilehash: 4b83862221cf249455478c3ade159a3101062f3e
ms.sourcegitcommit: 358a28048f36a8dca39a9fe6e6ac1f1913acadd5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85245441"
---
# <a name="configuring-client-behaviors"></a>クライアントの動作の構成
Windows Communication Foundation (WCF) では、2つの方法で動作を構成します。動作構成は、 `<behavior>` クライアントアプリケーション構成ファイルのセクションで定義されるか、または呼び出し元アプリケーションでプログラムによって定義されます。 このトピックでは、両方の方法について説明します。  
  
 構成ファイルを使用する場合、動作の構成には、構成設定の名前付きコレクションがあります。 各動作の構成には、一意の名前を指定する必要があります。 この文字列をエンドポイントの構成の `behaviorConfiguration` 属性で使用し、エンドポイントと動作を関連付けます。  
  
## <a name="example"></a>例  
 `myBehavior` という動作を定義する構成コードを次に示します。 クライアント エンドポイントは、この動作を `behaviorConfiguration` 属性で参照します。  
  
```xml  
<configuration>  
    <system.serviceModel>  
        <behaviors>  
            <endpointBehaviors>  
                <behavior name="myBehavior">  
                    <clientVia />  
                </behavior>  
            </endpointBehaviors>  
        </behaviors>  
        <bindings>  
            <basicHttpBinding>  
                <binding name="myBinding" maxReceivedMessageSize="10000" />  
            </basicHttpBinding>  
        </bindings>  
        <client>  
            <endpoint address="myAddress" binding="basicHttpBinding" bindingConfiguration="myBinding" behaviorConfiguration="myBehavior" contract="myContract" />  
        </client>  
    </system.serviceModel>  
</configuration>  
```  
  
## <a name="using-behaviors-programmatically"></a>プログラムによる動作の使用  
 また、 `Behaviors` クライアントを開く前に、Windows Communication Foundation (WCF) クライアントオブジェクトまたはクライアントチャネルファクトリオブジェクトで適切なプロパティを見つけることで、動作をプログラムによって構成または挿入することもできます。  
  
## <a name="example"></a>例  
 次のコード例は、チャネル オブジェクトの作成前に、<xref:System.ServiceModel.Description.ServiceEndpoint.Behaviors%2A> プロパティから返される <xref:System.ServiceModel.Description.ServiceEndpoint> 上の <xref:System.ServiceModel.ChannelFactory.Endpoint%2A> プロパティにアクセスすることで、プログラムでクライアント動作が挿入される方法を示します。  
  
 [!code-csharp[ChannelFactoryBehaviors#10](../../../samples/snippets/csharp/VS_Snippets_CFX/channelfactorybehaviors/cs/client.cs#10)]
 [!code-vb[ChannelFactoryBehaviors#10](../../../samples/snippets/visualbasic/VS_Snippets_CFX/channelfactorybehaviors/vb/client.vb#10)]  
  
## <a name="see-also"></a>関連項目

- [\<behaviors>](../configure-apps/file-schema/wcf/behaviors.md)
