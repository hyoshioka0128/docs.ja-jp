---
title: スタンドアロン診断フィードのサンプル
ms.date: 03/30/2017
ms.assetid: d31c6c1f-292c-4d95-8e23-ed8565970ea5
ms.openlocfilehash: 0402805b7eb5b0b224db32eb07780743e5f32fb3
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84600920"
---
# <a name="stand-alone-diagnostics-feed-sample"></a>スタンドアロン診断フィードのサンプル
このサンプルでは、Windows Communication Foundation (WCF) を使用して配信するために RSS/Atom フィードを作成する方法を示します。 これは基本的な "Hello World" プログラムであり、オブジェクトモデルの基本と、Windows Communication Foundation (WCF) サービスでの設定方法を示しています。  
  
 WCF は、特別なデータ型を返すサービス操作として配信フィードをモデル化し <xref:System.ServiceModel.Syndication.SyndicationFeedFormatter> ます。 <xref:System.ServiceModel.Syndication.SyndicationFeedFormatter> のインスタンスは、フィードを RSS 2.0 形式および Atom 1.0 形式の両方にシリアル化できます。 使用するコントラクトを次のサンプル コードに示します。  
  
```csharp  
[ServiceContract(Namespace = "")]  
    interface IDiagnosticsService  
    {  
        [OperationContract]  
        //The [WebGet] attribute controls how WCF dispatches  
        //HTTP requests to service operations based on a URI suffix  
        //(the part of the request URI after the endpoint address)  
        //using the HTTP GET method. The UriTemplate specifies a relative  
        //path of 'feed', and specifies that the format is  
        //supplied using a query string.
        [WebGet(UriTemplate="feed?format={format}")]  
        [ServiceKnownType(typeof(Atom10FeedFormatter))]  
        [ServiceKnownType(typeof(Rss20FeedFormatter))]  
        SyndicationFeedFormatter GetProcesses(string format);  
    }  
```  
  
 この `GetProcesses` 操作には、 <xref:System.ServiceModel.Web.WebGetAttribute> WCF が HTTP GET 要求をサービス操作にディスパッチする方法を制御し、送信されるメッセージの形式を指定できるようにする属性で注釈が付けられています。  
  
 任意の WCF サービスと同様に、配信フィードは任意のマネージアプリケーションで自己ホストすることができます。 配信サービスが適切に機能するには、特定のバインディング (<xref:System.ServiceModel.WebHttpBinding>) と、特定のエンドポイント動作 (<xref:System.ServiceModel.Description.WebHttpBehavior>) が必要です。 新しい <xref:System.ServiceModel.Web.WebServiceHost> クラスには、特定の構成を使用せずにこのようなエンドポイントを作成する際に便利な API が用意されています。  
  
```csharp  
WebServiceHost host = new WebServiceHost(typeof(ProcessService), new Uri("http://localhost:8000/diagnostics"));  
  
            //The WebServiceHost will automatically provide a default endpoint at the base address  
            //using the proper binding (the WebHttpBinding) and endpoint behavior (the WebHttpBehavior)  
```  
  
 または、IIS でホストされる .svc ファイルから <xref:System.ServiceModel.Activation.WebServiceHostFactory> を使用して、同等の機能を用意することもできます (この手法は、このサンプル コードでは示されません)。  
  
```xml
<% @ServiceHost Language="C#|VB" Debug="true" Service="ProcessService" %>
```
  
 このサービスは標準の HTTP GET を使用して要求を受け取るので、サービスへのアクセスには、RSS または ATOM に対応している任意のクライアントを使用できます。 たとえば、 `http://localhost:8000/diagnostics/feed/?format=atom` RSS 対応のブラウザーでまたはに移動して、このサービスの出力を表示でき `http://localhost:8000/diagnostics/feed/?format=rss` ます。
  
 また、 [WCF 配信オブジェクトモデルが Atom および RSS にマップ](../feature-details/how-the-wcf-syndication-object-model-maps-to-atom-and-rss.md)され、命令型コードを使用してシンジケートデータを読み取り、処理する方法を使用することもできます。  
  
```csharp
XmlReader reader = XmlReader.Create( "http://localhost:8000/diagnostics/feed/?format=rss",
    new XmlReaderSettings()
    {
        //MaxCharactersInDocument can be used to control the maximum amount of data
        //read from the reader and helps prevent OutOfMemoryException
        MaxCharactersInDocument = 1024 * 64
    } );

SyndicationFeed feed = SyndicationFeed.Load(reader);

foreach (SyndicationItem i in feed.Items)
{
    XmlSyndicationContent content = i.Content as XmlSyndicationContent;
    ProcessData pd = content.ReadContent<ProcessData>();

    Console.WriteLine(i.Title.Text);
    Console.WriteLine(pd.ToString());
}
```
  
## <a name="set-up-build-and-run-the-sample"></a>サンプルをセットアップ、ビルド、および実行する
  
1. Windows Communication Foundation のサンプルについては、「 [1 回限りのセットアップ手順](one-time-setup-procedure-for-the-wcf-samples.md)」で説明されているように、コンピューター上で HTTP および HTTPS に対する適切なアドレス登録アクセス許可を持っていることを確認します。

2. ソリューションをビルドします。

3. コンソール アプリケーションを実行します。

4. コンソールアプリケーションの実行中に、RSS 対応のブラウザーに移動するか、を `http://localhost:8000/diagnostics/feed/?format=atom` `http://localhost:8000/diagnostics/feed/?format=rss` 使用します。

> [!IMPORTANT]
> サンプルは、既にコンピューターにインストールされている場合があります。 続行する前に、次の (既定の) ディレクトリを確認してください。
>
> `<InstallDrive>:\WF_WCF_Samples`
>
> このディレクトリが存在しない場合は、 [Windows Communication Foundation (wcf) および Windows Workflow Foundation (WF) のサンプルの .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459)にアクセスして、すべての WINDOWS COMMUNICATION FOUNDATION (wcf) とサンプルをダウンロードして [!INCLUDE[wf1](../../../../includes/wf1-md.md)] ください。 このサンプルは、次のディレクトリに格納されます。
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Syndication\DiagnosticsFeed`

## <a name="see-also"></a>関連項目

- [WCF Web HTTP プログラミング モデル](../feature-details/wcf-web-http-programming-model.md)
- [WCF 配信](../feature-details/wcf-syndication.md)
