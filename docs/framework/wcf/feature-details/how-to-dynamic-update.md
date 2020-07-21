---
title: 動的な更新を行う方法
ms.date: 03/30/2017
ms.assetid: 9b8f6e0d-edab-4a7e-86e3-8c66bebc64bb
ms.openlocfilehash: aaeb4d9d42c289cf34a6aee9212fc2d74b8f8c01
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79184962"
---
# <a name="how-to-dynamic-update"></a>動的な更新を行う方法
ここでは、ルーティング構成の作成および動的な更新に必要な基本的手順について説明します。 この例では、ルーティングの初期構成を構成ファイルから取得し、すべてのメッセージを regularCalc 電卓サービスにルーティングします。ただし、これは、roundingCalc のサービスの提供先となるエンドポイントを変更するために、後でプログラムによって更新されます。  
  
> [!NOTE]
> 多くの実装では、構成が完全に動的で、既定の構成に依存しません。ただし、このトピックのシナリオのように、サービスの開始時は既定の構成の状態を使用することが望ましい場合もあります。  
  
> [!NOTE]
> 動的な更新はメモリ内のみで実行され、構成ファイルが変更されることはありません。  
  
 regularCalc でも roundingCalc でも、同じ加算、減算、乗算、および除算の操作がサポートされますが、roundingCalc では、すべての計算結果が、四捨五入によって最も近い整数値に変換されてから返されます。 regularCalc サービスにすべてのメッセージをルーティングするようにサービスを構成するには、構成ファイルが使用されます。 ルーティング サービスが開始されると、<xref:System.ServiceModel.Routing.RoutingExtension.ApplyConfiguration%2A> を使用して、メッセージを roundingCalc サービスにルーティングするようにルーティング サービスが構成されます。  
  
### <a name="implement-initial-configuration"></a>初期構成の実装  
  
1. サービスによって公開されるサービス エンドポイントを指定することによって、ルーティング サービスの基本的な構成を作成します。 次の例では、メッセージの受信に使用される、単一のサービス エンドポイントを定義します。 また、regularCalc へのメッセージ送信に使用するクライアント エンドポイントも定義します。  
  
    ```xml  
    <services>  
      <service behaviorConfiguration="routingConfiguration"  
               name="System.ServiceModel.Routing.RoutingService">  
        <host>  
          <baseAddresses>  
            <add baseAddress="http://localhost/routingservice/router" />  
          </baseAddresses>  
        </host>  
        <!--Set up the inbound endpoint for the Routing Service-->  
        <endpoint address="calculator"  
                  binding="wsHttpBinding"  
                  name="routerEndpoint"  
                  contract="System.ServiceModel.Routing.IRequestReplyRouter" />  
      </service>  
    </services>  
    <client>  
    <!--set up the destination endpoint-->  
      <endpoint name="regularCalcEndpoint"  
                address="net.tcp://localhost:9090/servicemodelsamples/service/"  
                binding="netTcpBinding"  
                contract="*" />  
    </client>  
    ```  
  
2. 送信先エンドポイントへのメッセージのルーティングに使用するフィルターを定義します。 この例では、MatchAll フィルターを使用して、前に定義した regularCalcEndpoint にすべてのメッセージをルーティングしています。 次の例では、フィルターおよびフィルター テーブルを定義します。  
  
    ```xml  
    <filters>  
      <!--define the message filter-->  
      <filter name="MatchAllFilter" filterType="MatchAll"/>  
    </filters>  
    <filterTables>  
      <filterTable name="filterTable1">  
          <!--add the filter to the message filter table-->  
          <add filterName="MatchAllFilter" endpointName="regularCalcEndpoint"/>  
      </filterTable>  
    </filterTables>  
    ```  
  
3. フィルター テーブルに含まれているフィルターと照合して受信メッセージを評価するには、ルーティング動作を使用して、フィルター テーブルをサービス エンドポイントと関連付ける必要があります。 "filterTable1" をサービス エンドポイントに関連付ける例を次に示します。  
  
    ```xml  
    <behaviors>  
      <!--default routing service behavior definition-->  
      <serviceBehaviors>  
        <behavior name="routingConfiguration">  
          <routing filterTableName="filterTable1" />  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
    ```  
  
## <a name="implement-dynamic-configuration"></a>動的構成の実装  
 ルーティング サービスの動的構成は、コードでのみ実行できます。これを実行するには、新しい <xref:System.ServiceModel.Routing.RoutingConfiguration> を作成し、<xref:System.ServiceModel.Routing.RoutingExtension.ApplyConfiguration%2A> を使用して現在の構成を置き換えます。  この例では、ルーティング サービスがコンソール アプリケーション内に自己ホストされます。 アプリケーションが起動したら、ルーティングの構成を変更できます。メッセージのルーティング先のエンドポイントを構成するには、コンソール ウィンドウで「regular」または「rounding」と入力します。「regular」と入力した場合は regularCalc が、「rounding」と入力した場合は roundingCalc になります。  
  
1. ルーティング サービスをサポートするには、次の using ステートメントを追加する必要があります。  
  
    ```csharp  
    using System;  
    using System.Collections.Generic;  
    using System.ServiceModel;  
    using System.ServiceModel.Channels;  
    using System.ServiceModel.Description;  
    using System.ServiceModel.Dispatcher;  
    using System.ServiceModel.Routing;  
    ```  
  
2. ルーティング サービスをコンソール アプリケーションとして自己ホストするには、次のコードを使用します。 これは、前の手順で説明した構成を使用してルーティング サービスを初期化します。この構成は、アプリケーション構成ファイルに保持されています。 while ループには、ルーティング構成の変更に使用されるコードが設定されています。  
  
    ```csharp  
    // Host the service within this EXE console application.  
    public static void Main()  
    {  
        // Create a ServiceHost for the CalculatorService type.  
        using (ServiceHost serviceHost =  
            new ServiceHost(typeof(RoutingService)))  
        {  
            // Open the ServiceHost to create listeners
            // and start listening for messages.  
            Console.WriteLine("The Routing Service configured, opening....");  
            serviceHost.Open();  
            Console.WriteLine("The Routing Service is now running.");  
             Console.WriteLine("Type 'quit' to terminate router.");  
             Console.WriteLine("<ENTER> to change routing configuration.");  
             while (Console.ReadLine() != "quit")  
             {  
            ....  
            }  
        }  
    }  
    ```  
  
3. ルーティング構成を動的に更新するには、新しいルーティング構成を作成する必要があります。 作成する構成には、新しいルーティング構成に必要なすべてのエンドポイント、フィルター、およびフィルター テーブルの情報が含まれている必要があります。これは、既存のルーティング構成全体が、この構成に置き換えられるためです。 新しいルーティング構成を使用するには、<xref:System.ServiceModel.Routing.RoutingExtension.ApplyConfiguration%2A> を呼び出して新しい構成を渡す必要があります。  
  
     前の手順で定義した while ループに次のコードを追加して、ユーザー入力を基にサービスを再構成できるようにします。  
  
    ```csharp  
    Console.WriteLine("Enter 'regular' or 'rounding' to set the destination endpoint:");  
    string destEndpoint = Console.ReadLine();  
    // Create a new RoutingConfiguration  
    RoutingConfiguration rc = new RoutingConfiguration();  
    // Determine the endpoint to configure for  
    switch (destEndpoint)  
    {  
        case "regular":  
            // Define the destination endpoint  
            ServiceEndpoint regularCalc = new ServiceEndpoint(  
               ContractDescription.GetContract(typeof(IRequestReplyRouter)),  
               new NetTcpBinding(),  
               new EndpointAddress("net.tcp://localhost:9090/servicemodelsamples/service/"));  
            // Create a MatchAll filter and add to the filter table  
            rc.FilterTable.Add(new MatchAllMessageFilter(), new List<ServiceEndpoint> { regularCalc });  
            // Use ApplyConfiguration to update the Routing Service  
            serviceHost.Extensions.Find<RoutingExtension>().ApplyConfiguration(rc);  
            Console.WriteLine("Applied new routing configuration.");  
            break;  
        case "rounding":  
            // Define the destination endpoint  
            ServiceEndpoint roundingCalc = new ServiceEndpoint(  
               ContractDescription.GetContract(typeof(IRequestReplyRouter)),  
               new NetTcpBinding(),  
               new EndpointAddress("net.tcp://localhost:8080/servicemodelsamples/service/"));  
            // Create a MatchAll filter and add to the filter table  
            rc.FilterTable.Add(new MatchAllMessageFilter(), new List<ServiceEndpoint> { roundingCalc });  
            // Use ApplyConfiguration to update the Routing Service  
            serviceHost.Extensions.Find<RoutingExtension>().ApplyConfiguration(rc);  
            Console.WriteLine("Applied new routing configuration.");  
            break;  
        default:  
            Console.WriteLine("Incorrect value entered, no change.");  
            break;  
    }  
    ```  
  
    > [!NOTE]
    > 新しい RoutingConfiguration を提供するメソッドは RoutingExtension service サービス拡張に含まれているため、新しい RoutingConfiguration オブジェクトは、ServiceHost または ServiceExtension (別の ServiceExtension など) への参照を含む WCF 拡張モデル、またはこの参照を取得できる WCF 拡張モデル内の任意の場所で提供できます。
  
## <a name="example"></a>例  

この例で使用するコンソール アプリケーションの完全な一覧を次に示します。
  
```csharp
//-----------------------------------------------------------------  
//  Copyright (c) Microsoft Corporation.  All Rights Reserved.  
//-----------------------------------------------------------------  
  
using System;  
using System.Collections.Generic;  
using System.ServiceModel;  
using System.ServiceModel.Channels;  
using System.ServiceModel.Description;  
using System.ServiceModel.Dispatcher;  
using System.ServiceModel.Routing;  
  
namespace Microsoft.Samples.AdvancedFilters  
{  
    public class Router  
    {  
        // Host the service within this EXE console application.  
        public static void Main()  
        {
            // Create a ServiceHost for the CalculatorService type.  
            using (ServiceHost serviceHost =  
                new ServiceHost(typeof(RoutingService)))  
            {  
                // Open the ServiceHost to create listeners
                // and start listening for messages.  
                Console.WriteLine("The Routing Service configured, opening....");  
                serviceHost.Open();  
                Console.WriteLine("The Routing Service is now running.");  
                Console.WriteLine("Type 'quit' to terminate router.");  
                Console.WriteLine("<ENTER> to change routing configuration.");  
                while (Console.ReadLine() != "quit")  
                {  
                    Console.WriteLine("Enter 'regular' or 'rounding' to set the destination endpoint:");  
                    string destEndpoint = Console.ReadLine();  
                    // Create a new RoutingConfiguration  
                    RoutingConfiguration rc = new RoutingConfiguration();  
                    // Determine the endpoint to configure for  
                    switch (destEndpoint)  
                    {  
                        case "regular":  
                            // Define the destination endpoint  
                            ServiceEndpoint regularCalc = new ServiceEndpoint(  
                            ContractDescription.GetContract(typeof(IRequestReplyRouter)),  
                            new NetTcpBinding(),  
                            new EndpointAddress("net.tcp://localhost:9090/servicemodelsamples/service/"));  
                            // Create a MatchAll filter and add to the filter table  
                            rc.FilterTable.Add(new MatchAllMessageFilter(), new List<ServiceEndpoint> { regularCalc });  
                            // Use ApplyConfiguration to update the Routing Service  
                            serviceHost.Extensions.Find<RoutingExtension>().ApplyConfiguration(rc);  
                            Console.WriteLine("Applied new routing configuration.");  
                            break;  
                        case "rounding":  
                            // Define the destination endpoint  
                            ServiceEndpoint roundingCalc = new ServiceEndpoint(  
                                ContractDescription.GetContract(typeof(IRequestReplyRouter)),  
                                new NetTcpBinding(),  
                                new EndpointAddress("net.tcp://localhost:8080/servicemodelsamples/service/"));  
                            // Create a MatchAll filter and add to the filter table  
                            rc.FilterTable.Add(new MatchAllMessageFilter(), new List<ServiceEndpoint> { roundingCalc });  
                            // Use ApplyConfiguration to update the Routing Service  
                            serviceHost.Extensions.Find<RoutingExtension>().ApplyConfiguration(rc);  
                            Console.WriteLine("Applied new routing configuration.");  
                            break;  
                        default:  
                            Console.WriteLine("Incorrect value entered, no change.");  
                            break;  
                    }  
                }  
            }  
        }  
    }  
}  
```  
  
## <a name="example"></a>例  

この例で使用されている構成ファイルの完全な一覧を次に示します。
  
```xml  
<?xml version="1.0" encoding="utf-8" ?>  
<!-- Copyright (c) Microsoft Corporation. All rights reserved -->  
<configuration>  
  <system.serviceModel>  
    <services>  
      <service behaviorConfiguration="routingConfiguration"  
               name="System.ServiceModel.Routing.RoutingService">  
        <host>  
          <baseAddresses>  
            <add baseAddress="http://localhost/routingservice/router" />  
          </baseAddresses>  
        </host>  
        <!--Set up the inbound endpoint for the Routing Service-->  
        <endpoint address="calculator"  
                  binding="wsHttpBinding"  
                  name="routerEndpoint"  
                  contract="System.ServiceModel.Routing.IRequestReplyRouter" />  
      </service>  
    </services>  
    <behaviors>  
      <!--default routing service behavior definition-->  
      <serviceBehaviors>  
        <behavior name="routingConfiguration">  
          <routing filterTableName="filterTable1" />  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
  
    <client>  
<!--set up the destination endpoint-->  
      <endpoint name="regularCalcEndpoint"  
                address="net.tcp://localhost:9090/servicemodelsamples/service/"  
                binding="netTcpBinding"  
                contract="*" />  
    </client>  
    <routing>  
  
      <filters>  
        <!--define the message filter-->  
        <filter name="MatchAllFilter" filterType="MatchAll"/>  
      </filters>  
      <filterTables>  
        <filterTable name="filterTable1">  
            <!--add the filter to the message filter table-->  
            <add filterName="MatchAllFilter" endpointName="regularCalcEndpoint"/>  
        </filterTable>  
      </filterTables>  
    </routing>  
  </system.serviceModel>  
</configuration>  
```  
  
## <a name="see-also"></a>関連項目

- [ルーティング サービス](../samples/routing-services.md)
