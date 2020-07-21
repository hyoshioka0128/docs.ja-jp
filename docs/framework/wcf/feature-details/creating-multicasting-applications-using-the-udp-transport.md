---
title: UDP トランスポートを使用するマルチキャスト アプリケーションの作成
ms.date: 03/30/2017
ms.assetid: 7485154a-6e85-4a67-a9d4-9008e741d4df
ms.openlocfilehash: 40944129ce3b01d8422d5aba4cfbf913c56265ed
ms.sourcegitcommit: ee5b798427f81237a3c23d1fd81fff7fdc21e8d3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/28/2020
ms.locfileid: "84144631"
---
# <a name="creating-multicasting-applications-using-the-udp-transport"></a>UDP トランスポートを使用するマルチキャスト アプリケーションの作成
マルチキャスト アプリケーションは、ポイント ツー ポイント接続を確立することなく多数の受信者に小さいメッセージを同時に送信します。 このようなアプリケーションの重点は、信頼性よりも速度です。 つまり、特定のメッセージが実際に受信されるということよりも、迅速にデータを送信することの方が重要です。 WCF は、<xref:System.ServiceModel.UdpBinding> を使用して、書き込みマルチキャスト アプリケーションをサポートします。 このトランスポートは、サービスが複数のクライアントに小さいメッセージを同時に送信する必要がある場合に便利です。 株価表示器のアプリケーションは、このようなサービスの例です。  
  
## <a name="implementing-a-multicast-application"></a>マルチキャスト アプリケーションの実装  
 マルチキャストのアプリケーションを実装するには、サービス コントラクトを定義し、マルチキャストのメッセージに応答する必要がある各ソフトウェア コンポーネントについては、サービス コントラクトを実装します。 たとえば、株価表示器のアプリケーションは、サービス コントラクトを定義する場合があります:  
  
```csharp
// Shared contracts between the client and the service  
[ServiceContract]
interface IStockTicker
{
    [OperationContract(IsOneWay = true)]
    void SendStockInfo(StockInfo[] stockInfo);
}

[DataContract]
class StockInfo
{
    [DataMember]
    public string Symbol;

    [DataMember]
    public float Price;

    public StockInfo(string symbol, float price)
    {
        this.Symbol = symbol;
        this.Price = price;
    }
}
```  
  
 マルチキャストのメッセージを受信する各アプリケーションはこのインターフェイスを公開するサービスをホストする必要があります。  たとえば、マルチキャストのメッセージを受信する方法を示すコード サンプルを次に示します。  
  
```csharp
// Service Address
string serviceAddress = "soap.udp://224.0.0.1:40000";
// Binding
UdpBinding myBinding = new UdpBinding();
// Host
ServiceHost host = new ServiceHost(typeof(StockTickerService), new Uri(serviceAddress));
// Add service endpoint
host.AddServiceEndpoint(typeof(IStockTicker), myBinding, string.Empty);
// Openup the service host
host.Open();

Console.WriteLine("Start receiving stock information");
Console.ReadLine();
```  
  
 アプリケーションはすべてのサービスがリッスンする UDP アドレスを指定します。 新しい <xref:System.ServiceModel.ServiceHost> が作成され、サービス エンドポイントは <xref:System.ServiceModel.UdpBinding>を使用して公開されます。 <xref:System.ServiceModel.ServiceHost> が開き、受信メッセージをリッスンし始めます。  
  
 このような場合、実際にマルチキャストのメッセージを送信するのはクライアントです。 正しい UDP アドレスでリッスンする各サービスはマルチキャストのメッセージを受信します。 マルチキャストのメッセージを送信するクライアントの例を次に示します。  
  
```csharp
// Multicast Address
string serviceAddress = "soap.udp://224.0.0.1:40000";

// Binding
UdpBinding myBinding = new UdpBinding();

// Channel factory
ChannelFactory<IStockTicker> factory
    = new ChannelFactory<IStockTicker>(myBinding,
                new EndpointAddress(serviceAddress));

// Call service
IStockTicker proxy = factory.CreateChannel();

while (true)
{
    // This will continue to mulicast stock information
    proxy.SendStockInfo(GetStockInfo());
    Console.WriteLine($"sent stock info at {DateTime.Now}");
    // Wait for one second before sending another update
    System.Threading.Thread.Sleep(new TimeSpan(0, 0, 1));
}
```  
  
 このコードは、株式の情報を生成し、サービス コントラクト IStockTicker を使用してマルチキャストのメッセージを送信することによって、正しい UDP アドレスでリッスンするサービスを呼び出します。  
  
### <a name="udp-and-reliable-messaging"></a>UDP および信頼できるメッセージング  
  UDP バインディングでは、UDP プロトコルに軽量という性質があるために信頼できるメッセージングをサポートしていません。 メッセージがリモート エンドポイントによって受信されることを確認する必要がある場合は、HTTP や TCP などの信頼できるメッセージングをサポートするトランスポートを使用します。 信頼できるメッセージングの詳細については、「」を参照してください <https://go.microsoft.com/fwlink/?LinkId=231830> 。  
  
### <a name="two-way-multicast-messaging"></a>双方向マルチキャストのメッセージング  
 マルチキャストのメッセージは通常、一方向ですが、UdpBinding は要求または応答メッセージ交換をサポートします。 UDP トランスポートを使用して送信されたメッセージには送信者と宛先のアドレスの両方が含まれます。 送信者のアドレスを使う場合は、送信中に悪意により変更されることがあるため、注意が必要です。  アドレスは、次のコードを使用してチェックすることができます。  
  
```csharp
if (address.AddressFamily == AddressFamily.InterNetwork)
{
    // IPv4
    byte[] addressBytes = address.GetAddressBytes();
    return ((addressBytes[0] & 0xE0) == 0xE0);
}
else
{
    // IPv6
    return address.IsIPv6Multicast;
}
```  
  
 このコードは、送信者のアドレスの先頭バイトをチェックして、アドレスがマルチキャスト アドレスであることを示す 0xE0 が含まれているかどうかを調べます。  
  
### <a name="security-considerations"></a>セキュリティに関する考慮事項  
 マルチキャストのメッセージをリッスンする場合、マルチキャストのアドレスでリッスンしていることを通知するルーターに ICMP パケットが送信されます。 アクセス許可を持つローカル サブネット上に存在するすべてのユーザーが、これらの型のパケットをリッスンし、リッスンしているマルチキャストのアドレスとポートを特定できます。  
  
 セキュリティ上の目的に送信者の IP アドレスを使用しないでください。 この情報は偽装され、アプリケーションが間違ったコンピューターに応答を送信する原因となる場合があります。 この脅威を軽減する方法には、メッセージ レベルのセキュリティを有効にすることがあります。 ネットワーク レベルでは、IPsec (インターネット プロトコル セキュリティ) や NAP (ネットワーク アクセス保護) も使用できます。
