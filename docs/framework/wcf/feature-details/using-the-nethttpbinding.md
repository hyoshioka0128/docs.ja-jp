---
title: NetHttpBinding の使用
ms.date: 03/30/2017
ms.assetid: fe134acf-ceca-49de-84a9-05a37e3841f1
ms.openlocfilehash: ac6fc658731d032051f2dfd4058397f9b9a55828
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84585637"
---
# <a name="using-the-nethttpbinding"></a>NetHttpBinding の使用
<xref:System.ServiceModel.NetHttpBinding> は、HTTP や WebSocket のサービスを使用するために設計されたバインドで、既定ではバイナリ エンコードを使用します。 <xref:System.ServiceModel.NetHttpBinding> は、要求-応答コントラクトと二重のコントラクトのどちらで使用されているかを検出し、一致するように動作を変更します。要求-応答コントラクトには HTTP、二重のコントラクトには Websocket を使用します。 この動作は、<xref:System.ServiceModel.Channels.WebSocketTransportUsage> 設定を使用してオーバーライドできます。  
  
1. <xref:System.ServiceModel.Channels.WebSocketTransportUsage.Always>-これにより、要求/応答コントラクトでも Websocket が強制的に使用されます。  
  
2. <xref:System.ServiceModel.Channels.WebSocketTransportUsage.Never>-Websocket が使用されないようにします。 この設定で二重のコントラクトを使用しようとすると、例外が発生します。  
  
3. <xref:System.ServiceModel.Channels.WebSocketTransportUsage.WhenDuplex>-これは既定値で、前述のように動作します。  
  
 <xref:System.ServiceModel.NetHttpBinding> は、HTTP モードと WebSocket モードの両方で信頼できるセッションをサポートします。 WebSocket モードでは、セッションがトランスポートによって提供されます。  
  
> [!WARNING]
> <xref:System.ServiceModel.NetHttpBinding> を使用していて、バインドの TransferMode が TransferMode.Streamed に設定されている場合、大きいストリームによってデッドロックが発生する可能性があり、呼び出しがタイムアウトします。 この問題を回避するには、小さいメッセージを送信するか、TransferMode.Buffered を使用してください。  
  
## <a name="configuring-a-service-to-use-nethttpbinding"></a>NetHttpBinding を使用するサービスの構成  
 <xref:System.ServiceModel.NetHttpBinding> は、他のバインドと同様に構成できます。 次の構成スニペットは、<xref:System.ServiceModel.NetHttpBinding> を使用して WCF サービスを構成する方法を示しています。  
  
```xml  
<system.serviceModel>  
    <services>  
      <service name="WcfService1.Service1">  
        <endpoint address=""  
                  binding="netHttpBinding"  
                  contract="WcfService1.IService1"/>  
        <endpoint address="mex"  
                  binding="mexHttpBinding"  
                  contract="IMetadataExchange"/>  
      </service>  
    </services>  
    <bindings>  
      <netHttpBinding>  
        <binding name="My_NetHttpBindingConfig">  
          <webSocketSettings transportUsage="WhenDuplex"/>  
        </binding>  
      </netHttpBinding>  
    </bindings>  
    ...
  </system.serviceModel>  
```  
  
 次のコード スニペットは、コードで <xref:System.ServiceModel.NetHttpBinding> を追加する方法を示しています。  
  
```csharp  
ServiceHost svchost = new ServiceHost(typeof(Service1), baseAddress);  
            NetHttpBinding binding = new NetHttpBinding();  
            svchost.AddServiceEndpoint(typeof(IService1), binding, address);
        }  
```  
  
## <a name="see-also"></a>関連項目

- [サービスのバインディングの構成](../configuring-bindings-for-wcf-services.md)
- [バインド](bindings.md)
- [システム標準のバインディング](../system-provided-bindings.md)
- [双方向サービス](duplex-services.md)
