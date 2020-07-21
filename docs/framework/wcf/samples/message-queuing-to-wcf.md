---
title: Windows Communication Foundation へのメッセージ キュー
ms.date: 03/30/2017
ms.assetid: 6d718eb0-9f61-4653-8a75-d2dac8fb3520
ms.openlocfilehash: 82e71afc911bff2504be15f7f9f2e736d943972b
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84584962"
---
# <a name="message-queuing-to-windows-communication-foundation"></a>Windows Communication Foundation へのメッセージ キュー

このサンプルでは、メッセージキュー (MSMQ) アプリケーションが MSMQ メッセージを Windows Communication Foundation (WCF) サービスに送信する方法を示します。 サービスは自己ホスト型コンソール アプリケーションであるので、キューに置かれたメッセージをサービスが受信するようすを観察できます。

 サービス コントラクトは `IOrderProcessor` です。これは、キューでの使用に適した一方向サービスを定義します。 MSMQ メッセージには Action ヘッダーがないので、さまざまな MSMQ メッセージを操作コントラクトに自動的にマッピングすることはできません。 したがって、存在する操作コントラクトは 1 つだけです。 サービスに対して複数の操作コントラクトを定義する場合は、ディスパッチする操作コントラクトを決定するために使用できる、MSMQ メッセージ内のヘッダー (ラベルや correlationID など) に関する情報をアプリケーションで提供する必要があります。

 MSMQ メッセージには、操作コントラクトの別のパラメータにマッピングされるヘッダーに関する情報は含まれません。 パラメータは <xref:System.ServiceModel.MsmqIntegration.MsmqMessage%601> 型の `MsmqMessage<T>` です。これには、基になる MSMQ メッセージが含まれます。 <xref:System.ServiceModel.MsmqIntegration.MsmqMessage%601> (`MsmqMessage<T>`) クラスの型 "T" は、シリアル化されて MSMQ メッセージ本文に含まれているデータを表します。 このサンプルでは、`PurchaseOrder` 型がシリアル化されて MSMQ メッセージ本文になっています。

 発注書処理サービスのサービス コントラクトを次のサンプル コードに示します。

```csharp
// Define a service contract.
[ServiceContract(Namespace = "http://Microsoft.ServiceModel.Samples")]
[ServiceKnownType(typeof(PurchaseOrder))]
public interface IOrderProcessor
{
    [OperationContract(IsOneWay = true, Action = "*")]
    void SubmitPurchaseOrder(MsmqMessage<PurchaseOrder> msg);
}
```

 サービスは自己ホスト型です。 MSMQ を使用する場合、使用するキューをあらかじめ作成しておく必要があります。 手動で作成することもコードで作成することもできます。 このサンプルでは、サービスはキューの存在を確認し、必要な場合はキューを作成します。 キュー名は構成ファイルから読み込まれます。

```csharp
public static void Main()
{
    // Get the MSMQ queue name from the application settings in
    // configuration.
    string queueName = ConfigurationManager.AppSettings["queueName"];
    // Create the MSMQ queue if necessary.
    if (!MessageQueue.Exists(queueName))
        MessageQueue.Create(queueName, true);
    …
}
```

 サービスは、<xref:System.ServiceModel.ServiceHost> の `OrderProcessorService` を作成して開きます。次のサンプル コードを参照してください。

```csharp
using (ServiceHost serviceHost = new ServiceHost(typeof(OrderProcessorService)))
{
    serviceHost.Open();
    Console.WriteLine("The service is ready.");
    Console.WriteLine("Press <ENTER> to terminate service.");
    Console.ReadLine();
    serviceHost.Close();
}
```

 MSMQ キュー名は、構成ファイルの appSettings セクションに指定されます。次のサンプル構成を参照してください。

> [!NOTE]
> キュー名では、ドット (.) を使用してローカル コンピューターを表し、バックスラッシュを使用してパスを区切ります。 WCF エンドポイントアドレスは、formatname スキーマを指定し、ローカルコンピューターに localhost を使用します。 それぞれの MSMQ 形式名のアドレス指定ガイドラインに対するキューのアドレスが msmq.formatname スキームの後に続きます。

```xml
<appSettings>
    <add key="orderQueueName" value=".\private$\Orders" />
</appSettings>
```

 クライアント アプリケーションは MSMQ アプリケーションです。このアプリケーションでは <xref:System.Messaging.MessageQueue.Send%2A> メソッドを使用して、非揮発性メッセージとトランザクション メッセージをキューに送信します。次のサンプル コードを参照してください。

```csharp
//Connect to the queue.
MessageQueue orderQueue = new MessageQueue(ConfigurationManager.AppSettings["orderQueueName"]);

// Create the purchase order.
PurchaseOrder po = new PurchaseOrder();
po.CustomerId = "somecustomer.com";
po.PONumber = Guid.NewGuid().ToString();

PurchaseOrderLineItem lineItem1 = new PurchaseOrderLineItem();
lineItem1.ProductId = "Blue Widget";
lineItem1.Quantity = 54;
lineItem1.UnitCost = 29.99F;

PurchaseOrderLineItem lineItem2 = new PurchaseOrderLineItem();
lineItem2.ProductId = "Red Widget";
lineItem2.Quantity = 890;
lineItem2.UnitCost = 45.89F;

po.orderLineItems = new PurchaseOrderLineItem[2];
po.orderLineItems[0] = lineItem1;
po.orderLineItems[1] = lineItem2;

// Submit the purchase order.
Message msg = new Message();
msg.Body = po;
//Create a transaction scope.
using (TransactionScope scope = new TransactionScope(TransactionScopeOption.Required))
{

    orderQueue.Send(msg, MessageQueueTransactionType.Automatic);
    // Complete the transaction.
    scope.Complete();

}
Console.WriteLine("Placed the order:{0}", po);
Console.WriteLine("Press <ENTER> to terminate client.");
Console.ReadLine();
```

 サンプルを実行すると、クライアントとサービスのアクティビティがサービスとクライアントの両方のコンソール ウィンドウに表示されます。 サービスがクライアントから受信したメッセージを表示できます。 どちらかのコンソールで Enter キーを押すと、サービスとクライアントがどちらもシャットダウンされます。 キューが使用されているので、クライアントとサービスが同時に実行されている必要はありません。 たとえば、クライアントを実行してシャットダウンした後にサービスを起動しても、サービスはメッセージを受信します。

## <a name="set-up-build-and-run-the-sample"></a>サンプルをセットアップ、ビルド、および実行する

1. [Windows Communication Foundation サンプルの1回限りのセットアップ手順](one-time-setup-procedure-for-the-wcf-samples.md)を実行したことを確認します。

2. サービスを最初に実行すると、サービスはキューが存在するかどうかを確認します。 キューが存在しない場合、サービスによってキューが作成されます。 最初にサービスを実行してキューを作成することも、MSMQ キュー マネージャーでキューを作成することもできます。 Windows 2008 でキューを作成するには、次の手順に従います。

    1. Visual Studio 2012 でサーバーマネージャーを開きます。

    2. [**機能**] タブを展開します。

    3. [**プライベートメッセージキュー**] を右クリックし、[**新規**]、[**プライベートキュー**] の順に選択します。

    4. [**トランザクション**] ボックスをオンにします。

    5. `ServiceModelSamplesTransacted`新しいキューの名前として「」と入力します。

3. ソリューションの C# 版または Visual Basic .NET 版をビルドするには、「 [Building the Windows Communication Foundation Samples](building-the-samples.md)」の手順に従います。

4. 1台のコンピューター構成でサンプルを実行するには、「 [Windows Communication Foundation サンプルの実行](running-the-samples.md)」の手順に従います。

## <a name="run-the-sample-across-computers"></a>コンピューター間でサンプルを実行する

1. サービスのプログラム ファイルを、言語固有のフォルダーにある \service\bin\ フォルダーからサービス コンピューターにコピーします。

2. クライアント プログラム ファイルを、言語固有のフォルダーにある \client\bin\ フォルダーからクライアント コンピューターにコピーします。

3. Client.exe.config ファイルを開き、orderQueueName を変更して "." の代わりにサービス コンピューター名を指定します。

4. サービス コンピューターで、コマンド プロンプトから Service.exe を起動します。

5. クライアント コンピューターで、コマンド プロンプトから Client.exe を起動します。

> [!IMPORTANT]
> サンプルは、既にコンピューターにインストールされている場合があります。 続行する前に、次の (既定の) ディレクトリを確認してください。
>
> `<InstallDrive>:\WF_WCF_Samples`
>
> このディレクトリが存在しない場合は、 [Windows Communication Foundation (wcf) および Windows Workflow Foundation (WF) のサンプルの .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459)にアクセスして、すべての WINDOWS COMMUNICATION FOUNDATION (wcf) とサンプルをダウンロードして [!INCLUDE[wf1](../../../../includes/wf1-md.md)] ください。 このサンプルは、次のディレクトリに格納されます。
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Binding\MSMQIntegration\MsmqToWcf`

## <a name="see-also"></a>関連項目

- [WCF のキュー](../feature-details/queues-in-wcf.md)
- [方法: WCF エンドポイントとメッセージ キュー アプリケーションを使用してメッセージを交換する](../feature-details/how-to-exchange-messages-with-wcf-endpoints-and-message-queuing-applications.md)
- [メッセージ キューイング (Message Queuing)](https://docs.microsoft.com/previous-versions/windows/desktop/legacy/ms711472(v=vs.85))
