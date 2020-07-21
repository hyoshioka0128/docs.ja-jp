---
title: '方法: クライアントのメッセージを検査または変更する'
description: 適切なインターフェイスを実装することによって、WCF クライアントまたはサービス全体で受信または送信メッセージを検査または変更する方法について説明します。
ms.date: 03/30/2017
ms.assetid: b8256335-f1c2-419f-b862-9f220ccad84c
ms.openlocfilehash: 6f6a3d20d7f3a9fb79de5cd3e29096e270d0f188
ms.sourcegitcommit: 358a28048f36a8dca39a9fe6e6ac1f1913acadd5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85247508"
---
# <a name="how-to-inspect-or-modify-messages-on-the-client"></a>方法: クライアントのメッセージを検査または変更する
を実装 <xref:System.ServiceModel.Dispatcher.IClientMessageInspector?displayProperty=nameWithType> してクライアントランタイムに挿入することによって、WCF クライアント全体の受信メッセージまたは送信メッセージを検査または変更できます。 詳細については、「[クライアントの拡張](extending-clients.md)」を参照してください。 サービスの同等の機能は、<xref:System.ServiceModel.Dispatcher.IDispatchMessageInspector?displayProperty=nameWithType> です。 完全なコード例については、[メッセージインスペクター](../samples/message-inspectors.md)のサンプルを参照してください。  
  
### <a name="to-inspect-or-modify-messages"></a>メッセージを検査または変更するには  
  
1. <xref:System.ServiceModel.Dispatcher.IClientMessageInspector?displayProperty=nameWithType> インターフェイスを実装します。  
  
2. クライアント メッセージ インスペクターを挿入するスコープに応じて、<xref:System.ServiceModel.Description.IEndpointBehavior?displayProperty=nameWithType> または <xref:System.ServiceModel.Description.IContractBehavior?displayProperty=nameWithType> を実装します。 <xref:System.ServiceModel.Description.IEndpointBehavior?displayProperty=nameWithType>エンドポイントレベルで動作を変更できます。 <xref:System.ServiceModel.Description.IContractBehavior?displayProperty=nameWithType>では、コントラクトレベルでの動作を変更できます。  
  
3. <xref:System.ServiceModel.ClientBase%601.Open%2A?displayProperty=nameWithType> で <xref:System.ServiceModel.ICommunicationObject.Open%2A?displayProperty=nameWithType> メソッドまたは <xref:System.ServiceModel.ChannelFactory%601?displayProperty=nameWithType> メソッドを呼び出す前に、動作を追加します。 詳細については、「動作を使用した[ランタイムの構成と拡張](configuring-and-extending-the-runtime-with-behaviors.md)」を参照してください。  
  
## <a name="example"></a>例  
 下のコード例では、次の項目を順番に示しています。  
  
- クライアント インスペクター実装  
  
- インスペクターを挿入するエンドポイント動作  
  
- 構成ファイルで動作を追加できるようにする <xref:System.ServiceModel.Configuration.BehaviorExtensionElement> 派生クラス。  
  
- クライアント メッセージ インスペクターをクライアント ランタイムに挿入するエンドポイント動作を追加する構成ファイル。  
  
```csharp  
// Client message inspector  
public class SimpleMessageInspector : IClientMessageInspector  
{  
    public void AfterReceiveReply(ref System.ServiceModel.Channels.Message reply, object correlationState)  
    {  
        // Implement this method to inspect/modify messages after a message  
        // is received but prior to passing it back to the client
        Console.WriteLine("AfterReceiveReply called");  
    }  
  
    public object BeforeSendRequest(ref System.ServiceModel.Channels.Message request, IClientChannel channel)  
    {  
        // Implement this method to inspect/modify messages before they
        // are sent to the service  
        Console.WriteLine("BeforeSendRequest called");  
        return null;  
    }  
}  
```  
  
```csharp  
// Endpoint behavior  
public class SimpleEndpointBehavior : IEndpointBehavior  
{  
    public void AddBindingParameters(ServiceEndpoint endpoint, System.ServiceModel.Channels.BindingParameterCollection bindingParameters)  
    {  
         // No implementation necessary  
    }  
  
    public void ApplyClientBehavior(ServiceEndpoint endpoint, ClientRuntime clientRuntime)  
    {  
        clientRuntime.MessageInspectors.Add(new SimpleMessageInspector());  
    }  
  
    public void ApplyDispatchBehavior(ServiceEndpoint endpoint, EndpointDispatcher endpointDispatcher)  
    {  
         // No implementation necessary  
    }  
  
    public void Validate(ServiceEndpoint endpoint)  
    {  
         // No implementation necessary  
    }  
}  
```  
  
```csharp  
// Configuration element
public class SimpleBehaviorExtensionElement : BehaviorExtensionElement  
{  
    public override Type BehaviorType  
    {  
        get { return typeof(SimpleEndpointBehavior); }  
    }  
  
    protected override object CreateBehavior()  
    {  
         // Create the  endpoint behavior that will insert the message  
         // inspector into the client runtime  
        return new SimpleEndpointBehavior();  
    }  
}  
```  
  
```xml
<?xml version="1.0" encoding="utf-8" ?>  
<configuration>  
    <system.serviceModel>  
        <client>  
            <endpoint address="http://localhost:8080/SimpleService/"
                      binding="wsHttpBinding"
                      behaviorConfiguration="clientInspectorsAdded"
                      contract="ServiceReference1.IService1"  
                      name="WSHttpBinding_IService1"/>  
        </client>  
  
      <behaviors>  
        <endpointBehaviors>  
          <behavior name="clientInspectorsAdded">  
            <simpleBehaviorExtension />  
          </behavior>  
        </endpointBehaviors>  
      </behaviors>  
      <extensions>  
        <behaviorExtensions>  
          <add  
            name="simpleBehaviorExtension"  
            type="SimpleServiceLib.SimpleBehaviorExtensionElement, Host, Version=0.0.0.0, Culture=neutral, PublicKeyToken=null"/>  
        </behaviorExtensions>  
      </extensions>  
    </system.serviceModel>  
</configuration>  
```  
  
## <a name="see-also"></a>関連項目

- <xref:System.ServiceModel.Dispatcher.IClientMessageInspector?displayProperty=nameWithType>
- <xref:System.ServiceModel.Dispatcher.IDispatchMessageInspector?displayProperty=nameWithType>
- [動作を使用したランタイムの構成と拡張](configuring-and-extending-the-runtime-with-behaviors.md)
