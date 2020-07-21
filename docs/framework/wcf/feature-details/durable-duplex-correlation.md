---
title: 永続的な二重の相関関係
ms.date: 03/30/2017
ms.assetid: 8eb0e49a-6d3b-4f7e-a054-0d4febee2ffb
ms.openlocfilehash: bb73cef5190a0b146e713ef1adae24219dc2eed8
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79185175"
---
# <a name="durable-duplex-correlation"></a>永続的な二重の相関関係
永続的な二重の相関関係 (コールバック相関関係) は、ワークフロー サービスがコールバックを最初の呼び出し元に送信する必要がある場合に便利です。 WCF の二重とは異なり、コールバックは、将来のどの時点でも発生する可能性があり、同じチャネルにも同じチャネルの有効期間にも関連付けられていません。唯一の要件は、呼び出し元にコールバック メッセージをリッスンするアクティブなエンドポイントを用意することです。 このため、2 つのワークフロー サービスが長時間のメッセージ交換を使用して通信できます。 このトピックでは、永続的な二重の相関関係について概説します。  
  
## <a name="using-durable-duplex-correlation"></a>永続的な二重の相関関係の使用  
 永続的な二重の相関関係を使用するには、2 つのサービスが、<xref:System.ServiceModel.NetTcpContextBinding> や <xref:System.ServiceModel.WSHttpContextBinding> など、双方向の操作をサポートするコンテキスト対応バインドを使用する必要があります。 呼び出し側サービスは、クライアントの <xref:System.ServiceModel.WSHttpContextBinding.ClientCallbackAddress%2A> で使用するバインドを指定して <xref:System.ServiceModel.Endpoint> を登録します。 受信側サービスは、このデータを最初の呼び出しで受信し、呼び出し側サービスへのコールバックを行う <xref:System.ServiceModel.Endpoint> アクティビティにおいて、受信側サービス自体の <xref:System.ServiceModel.Activities.Send> でこのデータを使用します。 次の例では、2 つのサービスが互いに通信しています。 1 つ目のサービスは、2 つ目のサービスに対してメソッドを呼び出し、応答を待機します。 2 つ目のサービスでは、コールバック メソッドの名前が認識されていますが、このメソッドを実装するサービスのエンドポイントは、設計時には認識されていません。  
  
> [!NOTE]
> エンドポイントの <xref:System.ServiceModel.Channels.AddressingVersion> が <xref:System.ServiceModel.Channels.AddressingVersion.WSAddressing10%2A> で構成される場合は、永続的な二重のみが使用できます。 それ以外の場合は、<xref:System.InvalidOperationException>次のメッセージで例外がスローされます: "メッセージには[、EndpointingVersion](http://schemas.xmlsoap.org/ws/2004/08/addressing)のエンドポイント参照を含むコールバック コンテキスト ヘッダーが含まれています。 コールバック コンテキストは、アドレスバージョンが 'WSAddressing10' で構成されている場合にのみ送信できます。
  
 次の例では、<xref:System.ServiceModel.Endpoint> を使用してコールバック <xref:System.ServiceModel.WSHttpContextBinding> を作成するワークフロー サービスがホストされます。  
  
```csharp  
// Host WF Service 1.  
string baseAddress1 = "http://localhost:8080/Service1";  
WorkflowServiceHost host1 = new WorkflowServiceHost(GetWF1(), new Uri(baseAddress1));  
  
// Add the callback endpoint.  
WSHttpContextBinding Binding1 = new WSHttpContextBinding();  
host1.AddServiceEndpoint("ICallbackItemsReady", Binding1, "ItemsReady");  
  
// Add the service endpoint.  
host1.AddServiceEndpoint("IService1", Binding1, baseAddress1);  
  
// Open the first workflow service.  
host1.Open();  
Console.WriteLine("Service1 waiting at: {0}", baseAddress1);  
```  
  
 このワークフロー サービスを実装するワークフローは、ワークフロー自体の <xref:System.ServiceModel.Activities.Send> アクティビティを使用してコールバック相関関係を初期化し、<xref:System.ServiceModel.Activities.Receive> と相関関係にある <xref:System.ServiceModel.Activities.Send> アクティビティからこのコールバック エンドポイントを参照します。 次の例は、`GetWF1` メソッドから返されるワークフローです。  
  
```csharp  
Variable<CorrelationHandle> CallbackHandle = new Variable<CorrelationHandle>();  
  
Receive StartOrder = new Receive  
{  
    CanCreateInstance = true,  
    ServiceContractName = "IService1",  
    OperationName = "StartOrder"  
};  
  
Send GetItems = new Send  
{  
    CorrelationInitializers =
    {  
        new CallbackCorrelationInitializer  
        {  
            CorrelationHandle = CallbackHandle  
        }  
    },  
    ServiceContractName = "IService2",  
    OperationName = "StartItems",  
    Endpoint = new Endpoint  
    {  
        AddressUri = new Uri("http://localhost:8081/Service2"),  
        Binding = new WSHttpContextBinding  
        {  
            ClientCallbackAddress = new Uri("http://localhost:8080/Service1/ItemsReady")
        }  
    }  
};  
  
Receive ItemsReady = new Receive  
{  
    ServiceContractName = "ICallbackItemsReady",  
    OperationName = "ItemsReady",  
    CorrelatesWith = CallbackHandle,  
};  
  
Activity wf = new Sequence  
{  
    Variables =  
    {  
        CallbackHandle  
    },  
    Activities =  
    {  
        StartOrder,  
        new WriteLine  
        {  
            Text = "WF1 - Started"  
        },  
        GetItems,  
        new WriteLine  
        {  
            Text = "WF1 - Request Submitted"  
        },  
        ItemsReady,  
        new WriteLine  
        {  
            Text = "WF1 - Items Received"  
        }  
     }  
};  
```  
  
 2 つ目のワークフロー サービスは、システムが提供するコンテキスト ベースのバインドを使用してホストされます。  
  
```csharp  
// Host WF Service 2.  
string baseAddress2 = "http://localhost:8081/Service2";  
WorkflowServiceHost host2 = new WorkflowServiceHost(GetWF2(), new Uri(baseAddress2));  
  
// Add the service endpoint.  
WSHttpContextBinding Binding2 = new WSHttpContextBinding();  
host2.AddServiceEndpoint("IService2", Binding2, baseAddress2);  
  
// Open the second workflow service.  
host2.Open();  
Console.WriteLine("Service2 waiting at: {0}", baseAddress2);  
```  
  
 このワークフロー サービスを実装するワークフローは、<xref:System.ServiceModel.Activities.Receive> アクティビティから開始されます。 この受信アクティビティは、このサービスのコールバック相関関係を初期化し、一定の遅延時間を設けて長時間の作業をシミュレーションして、サービスへの最初の呼び出しで渡されたコールバック コンテキストを使用して、最初のサービスにコールバックします。 次の例は、`GetWF2` への呼び出しから返されるワークフローです。 <xref:System.ServiceModel.Activities.Send> アクティビティには、`http://www.contoso.com` のプレースホルダー アドレスが設定されていることに注意してください。実行時に使用される実際のアドレスは、指定されたコールバック アドレスです。  
  
```csharp  
Variable<CorrelationHandle> ItemsCallbackHandle = new Variable<CorrelationHandle>();  
  
Receive StartItems = new Receive  
{  
    CorrelationInitializers =
    {  
        new CallbackCorrelationInitializer  
        {  
            CorrelationHandle = ItemsCallbackHandle  
        }  
    },  
    CanCreateInstance = true,  
    ServiceContractName = "IService2",  
    OperationName = "StartItems"  
};  
  
Send ItemsReady = new Send  
{  
    CorrelatesWith = ItemsCallbackHandle,  
    Endpoint = new Endpoint  
    {  
        // The callback address on the binding is used  
        // instead of this placeholder address.  
        AddressUri = new Uri("http://www.contoso.com"),  
  
        Binding = new WSHttpContextBinding()  
    },  
    OperationName = "ItemsReady",  
    ServiceContractName = "ICallbackItemsReady"  
};  
  
Activity wf = new Sequence  
{  
    Variables =  
    {  
        ItemsCallbackHandle  
    },  
    Activities =  
    {  
        StartItems,  
        new WriteLine  
        {  
            Text = "WF2 - Request Received"  
        },  
        new Delay  
        {  
            Duration = TimeSpan.FromMinutes(90)  
        },  
        new WriteLine  
        {  
            Text = "WF2 - Sending items"  
        },  
        ItemsReady,  
        new WriteLine  
        {  
            Text = "WF2 - Items sent"  
        }  
     }  
};  
```  
  
 `StartOrder` メソッドが最初のワークフローで呼び出されると、次の出力が表示されます。これは、2 つのワークフローの実行フローを示しています。  
  
```output  
Service1 waiting at: http://localhost:8080/Service1  
Service2 waiting at: http://localhost:8081/Service2  
Press enter to exit.
WF1 - Started  
WF2 - Request Received  
WF1 - Request Submitted  
WF2 - Sending items  
WF2 - Items sent  
WF1 - Items Received  
```  
  
 この例では、どちらのワークフローも <xref:System.ServiceModel.Activities.CallbackCorrelationInitializer> を使用して相関関係を明示的に管理しています。 サンプル ワークフローには相関関係が 1 つしかないため、既定の <xref:System.ServiceModel.Activities.CorrelationHandle> で十分に管理できます。
