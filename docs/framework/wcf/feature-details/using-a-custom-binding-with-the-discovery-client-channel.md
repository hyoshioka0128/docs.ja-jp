---
title: カスタム バインドを探索クライアント チャネルと共に使用する
ms.date: 03/30/2017
ms.assetid: 36f95e75-04f7-44f3-a995-a0d623624d7f
ms.openlocfilehash: 49983c3ab303d3839350af72b1aa4821c071fe99
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84595038"
---
# <a name="using-a-custom-binding-with-the-discovery-client-channel"></a>カスタム バインドを探索クライアント チャネルと共に使用する
カスタム バインドを <xref:System.ServiceModel.Discovery.DiscoveryClientBindingElement> と共に使用する場合は、<xref:System.ServiceModel.Discovery.DiscoveryEndpointProvider> インスタンスを作成する <xref:System.ServiceModel.Discovery.DiscoveryEndpoint> を定義する必要があります。  
  
## <a name="creating-a-discoveryendpointprovider"></a>DiscoveryEndpointProvider の作成  
 <xref:System.ServiceModel.Discovery.DiscoveryEndpointProvider>は、 <xref:System.ServiceModel.Discovery.DiscoveryEndpoint> 必要に応じてインスタンスを作成します。 探索エンドポイント プロバイダーを定義するには、<xref:System.ServiceModel.Discovery.DiscoveryEndpointProvider> からクラスを派生させ、<xref:System.ServiceModel.Discovery.DiscoveryEndpointProvider.GetDiscoveryEndpoint%2A> メソッドをオーバーライドし、新しい探索エンドポイントを返します。 次の例は、探索エンドポイント プロバイダーを作成する方法を示しています。  
  
```csharp
// Extend DiscoveryEndpointProvider class to change the default DiscoveryEndpoint  
// to the DiscoveryClientBindingElement. The Discovery ClientChannel
// uses this endpoint to send Probe message.  
public class UdpDiscoveryEndpointProvider : DiscoveryEndpointProvider  
{  
   public override DiscoveryEndpoint GetDiscoveryEndpoint()  
   {  
      return new UdpDiscoveryEndpoint(DiscoveryVersion.WSDiscoveryApril2005);  
   }  
}  
```  
  
 探索エンドポイント プロバイダーを定義したら、次の例に示すように、カスタム バインディングを作成し、その探索エンドポイント プロバイダーを参照する <xref:System.ServiceModel.Discovery.DiscoveryClientBindingElement> を追加できます。  
  
```csharp
DiscoveryClientBindingElement discoveryBindingElement = new DiscoveryClientBindingElement();  
  
// Provide the search criteria and the endpoint over which the probe is sent.  
discoveryBindingElement.FindCriteria = new FindCriteria(typeof(ICalculatorService));  
discoveryBindingElement.DiscoveryEndpointProvider = new UdpDiscoveryEndpointProvider();  
  
CustomBinding customBinding = new CustomBinding(new NetTcpBinding());  
// Insert DiscoveryClientBindingElement at the top of the BindingElement stack.  
// An exception is thrown if this binding element is not at the top.  
customBinding.Elements.Insert(0, discoveryBindingElement);  
```  
  
 探索クライアントチャネルの使用方法の詳細については、「[探索クライアントチャネルの使用](using-the-discovery-client-channel.md)」を参照してください。
  
## <a name="see-also"></a>関連項目

- [WCF Discovery の概要](wcf-discovery-overview.md)
- [探索クライアント チャネルの使用](using-the-discovery-client-channel.md)
