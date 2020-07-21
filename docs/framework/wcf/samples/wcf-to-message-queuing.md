---
title: Windows Communication Foundation でのメッセージ キュー
ms.date: 03/30/2017
ms.assetid: 78d0d0c9-648e-4d4a-8f0a-14d9cafeead9
ms.openlocfilehash: 872632dc7d0a8a94f8829ffb3fe8eea2607697c8
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84602345"
---
# <a name="windows-communication-foundation-to-message-queuing"></a>Windows Communication Foundation でのメッセージ キュー

このサンプルでは、Windows Communication Foundation (WCF) アプリケーションがメッセージキュー (MSMQ) アプリケーションにメッセージを送信する方法を示します。 サービスは自己ホスト型コンソール アプリケーションであるので、キューに置かれたメッセージをサービスが受信するようすを観察できます。 サービスとクライアントは同時に実行されていなくてもかまいません。

 サービスは、メッセージをキューから受信して注文を処理します。 サービスはトランザクション キューを作成し、メッセージがメッセージ ハンドラによって受信されるように設定します。次のサンプル コードを参照してください。

```csharp
static void Main(string[] args)
{
    if (!MessageQueue.Exists(
              ConfigurationManager.AppSettings["queueName"]))
       MessageQueue.Create(
           ConfigurationManager.AppSettings["queueName"], true);
        //Connect to the queue
        MessageQueue Queue = new
    MessageQueue(ConfigurationManager.AppSettings["queueName"]);
    Queue.ReceiveCompleted +=
                 new ReceiveCompletedEventHandler(ProcessOrder);
    Queue.BeginReceive();
    Console.WriteLine("Order Service is running");
    Console.ReadLine();
}
```

 メッセージがキュー内で受信されると、メッセージ ハンドラ `ProcessOrder` が呼び出されます。

```csharp
public static void ProcessOrder(Object source,
    ReceiveCompletedEventArgs asyncResult)
{
    try
    {
        // Connect to the queue.
        MessageQueue Queue = (MessageQueue)source;
        // End the asynchronous receive operation.
        System.Messaging.Message msg =
                     Queue.EndReceive(asyncResult.AsyncResult);
        msg.Formatter = new System.Messaging.XmlMessageFormatter(
                                new Type[] { typeof(PurchaseOrder) });
        PurchaseOrder po = (PurchaseOrder) msg.Body;
        Random statusIndexer = new Random();
        po.Status = PurchaseOrder.OrderStates[statusIndexer.Next(3)];
        Console.WriteLine("Processing {0} ", po);
        Queue.BeginReceive();
    }
    catch (System.Exception ex)
    {
        Console.WriteLine(ex.Message);
    }

}
```

 サービスは MSMQ メッセージ本文から `ProcessOrder` を抽出し、注文を処理します。

 MSMQ キュー名は、構成ファイルの appSettings セクションに指定されます。次のサンプル構成を参照してください。

```xml
<appSettings>
    <add key="orderQueueName" value=".\private$\Orders" />
</appSettings>
```

> [!NOTE]
> キュー名では、ドット (.) を使用してローカル コンピューターを表し、バックスラッシュを使用してパスを区切ります。

 クライアントは発注書を作成してトランザクションのスコープ内に送信します。次のサンプル コードを参照してください。

```csharp
// Create the purchase order
PurchaseOrder po = new PurchaseOrder();
// Fill in the details
...

OrderProcessorClient client = new OrderProcessorClient("OrderResponseEndpoint");

MsmqMessage<PurchaseOrder> ordermsg = new MsmqMessage<PurchaseOrder>(po);
using (TransactionScope scope = new TransactionScope(TransactionScopeOption.Required))
{
    client.SubmitPurchaseOrder(ordermsg);
    scope.Complete();
}
Console.WriteLine("Order has been submitted:{0}", po);

//Closing the client gracefully closes the connection and cleans up resources
client.Close();
```

 クライアントは、MSMQ メッセージをキューに送信するためにカスタム クライアントを順に使用します。 メッセージを受信して処理するアプリケーションは MSMQ アプリケーションであり、WCF アプリケーションではないため、2つのアプリケーション間に暗黙のサービスコントラクトはありません。 したがって、このシナリオでは Svcutil.exe ツールを使用してプロキシを作成することはできません。

 カスタムクライアントは、バインディングを使用してメッセージを送信するすべての WCF アプリケーションで基本的に同じです `MsmqIntegration` 。 他のクライアントと異なり、サービス操作の範囲は含まれません。 メッセージ送信操作のみです。

```csharp
[System.ServiceModel.ServiceContractAttribute(Namespace = "http://Microsoft.ServiceModel.Samples")]
public interface IOrderProcessor
{
    [OperationContract(IsOneWay = true, Action = "*")]
    void SubmitPurchaseOrder(MsmqMessage<PurchaseOrder> msg);
}

public partial class OrderProcessorClient : System.ServiceModel.ClientBase<IOrderProcessor>, IOrderProcessor
{
    public OrderProcessorClient(){}

    public OrderProcessorClient(string configurationName)
        : base(configurationName)
    { }

    public OrderProcessorClient(System.ServiceModel.Channels.Binding binding, System.ServiceModel.EndpointAddress address)
        : base(binding, address)
    { }

    public void SubmitPurchaseOrder(MsmqMessage<PurchaseOrder> msg)
    {
        base.Channel.SubmitPurchaseOrder(msg);
    }
}
```

 サンプルを実行すると、クライアントとサービスのアクティビティがサービスとクライアントの両方のコンソール ウィンドウに表示されます。 サービスがクライアントから受信したメッセージを表示できます。 どちらかのコンソールで Enter キーを押すと、サービスとクライアントがどちらもシャットダウンされます。 キューが使用されているので、クライアントとサービスが同時に実行されている必要はありません。 たとえば、クライアントを実行してシャットダウンした後にサービスを起動しても、サービスはメッセージを受信します。

> [!NOTE]
> このサンプルを実行するには、メッセージ キューがインストールされている必要があります。 「[メッセージキュー](https://docs.microsoft.com/previous-versions/windows/desktop/legacy/ms711472(v=vs.85))」のインストール手順を参照してください。

## <a name="set-up-build-and-run-the-sample"></a>サンプルをセットアップ、ビルド、および実行する

1. [Windows Communication Foundation サンプルの1回限りのセットアップ手順](one-time-setup-procedure-for-the-wcf-samples.md)を実行したことを確認します。

2. サービスを最初に実行すると、サービスはキューが存在するかどうかを確認します。 キューが存在しない場合、サービスによってキューが作成されます。 最初にサービスを実行してキューを作成することも、MSMQ キュー マネージャーでキューを作成することもできます。 Windows 2008 でキューを作成するには、次の手順に従います。

    1. Visual Studio 2012 でサーバーマネージャーを開きます。

    2. [**機能**] タブを展開します。

    3. [**プライベートメッセージキュー**] を右クリックし、[**新しい**  >  **プライベートキュー**] を選択します。

    4. [**トランザクション**] ボックスをオンにします。

    5. `ServiceModelSamplesTransacted`新しいキューの名前として「」と入力します。

3. ソリューションの C# または Visual Basic エディションをビルドするには、「 [Windows Communication Foundation サンプルのビルド](building-the-samples.md)」の手順に従います。

4. 1台のコンピューター構成でサンプルを実行するには、「 [Windows Communication Foundation サンプルの実行](running-the-samples.md)」の手順に従います。

## <a name="run-the-sample-across-computers"></a>コンピューター間でサンプルを実行する

1. サービスのプログラム ファイルを、言語固有のフォルダーにある \service\bin\ フォルダーからサービス コンピューターにコピーします。

2. クライアント プログラム ファイルを、言語固有のフォルダーにある \client\bin\ フォルダーからクライアント コンピューターにコピーします。

3. Client.exe.config ファイルで、クライアント エンドポイントのアドレスを変更して "." の代わりにサービス コンピューター名を指定します。

4. サービス コンピューターで、コマンド プロンプトから Service.exe を起動します。

5. クライアント コンピューターで、コマンド プロンプトから Client.exe を起動します。

> [!IMPORTANT]
> サンプルは、既にコンピューターにインストールされている場合があります。 続行する前に、次の (既定の) ディレクトリを確認してください。
>
> `<InstallDrive>:\WF_WCF_Samples`
>
> このディレクトリが存在しない場合は、 [Windows Communication Foundation (wcf) および Windows Workflow Foundation (WF) のサンプルの .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459)にアクセスして、すべての WINDOWS COMMUNICATION FOUNDATION (wcf) とサンプルをダウンロードして [!INCLUDE[wf1](../../../../includes/wf1-md.md)] ください。 このサンプルは、次のディレクトリに格納されます。
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Binding\MSMQIntegration\WcfToMsmq`

## <a name="see-also"></a>関連項目

- [方法: WCF エンドポイントとメッセージ キュー アプリケーションを使用してメッセージを交換する](../feature-details/how-to-exchange-messages-with-wcf-endpoints-and-message-queuing-applications.md)
- [メッセージ キューイング (Message Queuing)](https://docs.microsoft.com/previous-versions/windows/desktop/legacy/ms711472(v=vs.85))
