---
title: '方法: ASP.NET AJAX エンドポイントのために HTTP POST または HTTP GET を選択する'
ms.date: 03/30/2017
ms.assetid: b47de82a-4c92-4af6-bceb-a5cb8bb8ede9
ms.openlocfilehash: c74b1acdf3802ab680123cd9d676919fe47236e8
ms.sourcegitcommit: 0edbeb66d71b8df10fcb374cfca4d731b58ccdb2
ms.contentlocale: ja-JP
ms.lasthandoff: 07/07/2020
ms.locfileid: "86051585"
---
# <a name="how-to-choose-between-http-post-and-http-get-requests-for-aspnet-ajax-endpoints"></a>方法: ASP.NET AJAX エンドポイントのために HTTP POST または HTTP GET を選択する

Windows Communication Foundation (WCF) を使用すると、クライアント Web サイトの JavaScript から呼び出すことができる ASP.NET AJAX 対応エンドポイントを公開するサービスを作成できます。 このようなサービスを構築するための基本的な手順については、 [「方法: 構成を使用して ASP.NET AJAX エンドポイントを追加](how-to-use-configuration-to-add-an-aspnet-ajax-endpoint.md)する」および[「方法: 構成を使用せずに ASP.NET ajax エンドポイントを追加する](how-to-add-an-aspnet-ajax-endpoint-without-using-configuration.md)」を説明しています。  
  
 ASP.NET AJAX では、HTTP POST 動詞および HTTP GET 動詞を使用する操作をサポートしており、HTTP POST が既定となっています。 副作用がなく、返されるデータがほとんど、またはまったく変更されない操作を作成する場合は、代わりに HTTP GET を使用します。 GET 操作の結果はキャッシュされます。つまり、同じ操作についての複数の呼び出し結果がサービスに対する 1 回だけの要求で済むことになります。 キャッシュは WCF では実行されませんが、任意のレベル (ユーザーのブラウザー、プロキシサーバー、およびその他のレベル) で実行できます。キャッシュは、サービスのパフォーマンスを向上させる必要がある場合に便利ですが、データが頻繁に変更されたり、操作が何らかのアクションを実行したりした場合には許容できない可能性があります。  
  
 たとえば、ユーザーの音楽ライブラリを管理するサービスをデザインする場合、アルバムのタイトルに基づいてアーティストを検索する操作では GET の使用は役に立ちますが、ユーザーの個人コレクションにアルバムを追加する操作では POST を使用する必要があります。  
  
 キャッシュの有効期間を制御するには、<xref:System.ServiceModel.Web.OutgoingWebResponseContext> 型を使用します。 たとえば、1 時間ごとに更新される天気予報を返すサービスをデザインする場合、GET を使用することが考えられますが、サービスを使用するユーザーが古いデータにアクセスすることを防止するために、キャッシュの有効期間を 1 時間以内に制限します。  
  
 Script Manager コントロールを使用する ASP.NET AJAX ページからサービスを使用する場合は、Script Manager のメカニズムにより適切な要求の種類が発行されることが保証されているため、操作で GET と POST のどちらを使用しても違いはありません。  
  
 HTTP GET 操作では、複合型データ コントラクト型も含めて、POST 操作でサポートされるすべての入力パラメーターを使用できます。 ただし、多くの場合、キャッシュの効率が低下するため、多数のパラメーター、または複雑すぎるパラメーターを GET 操作で使用しないことをお勧めします。  
  
 このトピックでは、<xref:System.ServiceModel.Web.WebGetAttribute> または <xref:System.ServiceModel.Web.WebInvokeAttribute> 属性を追加することで、サービス コントラクトに適切な操作を GET と POST から選択する方法について説明します。 サービスを実行するために必要な他の手順 (サービスを実装、構成、およびホストする) は、WCF の ASP.NET AJAX サービスで使用される手順と似ています。  
  
 <xref:System.ServiceModel.Web.WebGetAttribute> でマークされた操作では、常に GET 要求が使用されます。 <xref:System.ServiceModel.Web.WebInvokeAttribute> でマークされた操作と、これらの 2 つの属性のどちらでもマークされていない操作では、POST 要求が使用されます。 <xref:System.ServiceModel.Web.WebInvokeAttribute> は、<xref:System.ServiceModel.Web.WebInvokeAttribute.Method%2A> プロパティを介して、GET と POST 以外の HTTP 動詞 (PUT や DELETE など) の使用を許可します。 ただし、これらの動詞は ASP.NET AJAX ではサポートされていません。 Script Manager コントロールを使用して ASP.NET ページからサービスを使用する場合は、<xref:System.ServiceModel.Web.WebInvokeAttribute.Method%2A> プロパティは使用しないでください。  
  
 GET に切り替える実際の例については、 [AJAX サービスの基本的な](../samples/basic-ajax-service.md)サンプルを参照してください。  
  
 POST を使用するサンプルについては、「 [HTTP post サンプルを使用した AJAX サービス](../samples/ajax-service-using-http-post.md)」を参照してください。  
  
## <a name="to-create-a-wcf-service-that-responds-to-http-get-or-http-post-requests"></a>HTTP GET または HTTP POST 要求に応答する WCF サービスを作成するには
  
1. 属性でマークされたインターフェイスを使用して、基本的な WCF サービスコントラクトを定義 <xref:System.ServiceModel.ServiceContractAttribute> します。 各操作を <xref:System.ServiceModel.OperationContractAttribute> でマークします。 <xref:System.ServiceModel.Web.WebGetAttribute> 属性を追加して、操作が HTTP GET 要求に応答するように指定します。 HTTP POST を明示的に指定するために <xref:System.ServiceModel.Web.WebInvokeAttribute> 属性を追加することもできます。また、属性を指定しなければ、既定で HTTP POST となります。
  
    ```csharp
    [ServiceContract]  
    public interface IMusicService  
    {  
        //This operation uses a GET method.  
        [OperationContract]  
        [WebGet]  
        string LookUpArtist(string album);  
  
        //This operation will use a POST method.  
        [OperationContract]  
        [WebInvoke]  
        void AddAlbum(string user, string album);  
  
        //This operation will use POST method by default  
        //since nothing else is explicitly specified.  
        [OperationContract]  
        string[] GetAlbums(string user);  
  
        //Other operations omitted…  
  
    }  
    ```  
  
2. `IMusicService` を使用して、`MusicService` サービス コントラクトを実装します。
  
    ```csharp
    public class MusicService : IMusicService  
    {  
        public void AddAlbum(string user, string album)  
        {  
            //Add implementation here.  
        }  
  
         //Other operations omitted…  
    }  
    ```  
  
3. アプリケーションで、.svc という拡張子を付けて新しい service ファイルを作成します。 このファイルを編集するには、サービスに適切な[ \@ ServiceHost](../../configure-apps/file-schema/wcf-directive/servicehost.md)ディレクティブ情報を追加します。 <xref:System.ServiceModel.Activation.WebScriptServiceHostFactory>ASP.NET AJAX エンドポイントを自動的に構成するために、 [ \@ ServiceHost](../../configure-apps/file-schema/wcf-directive/servicehost.md)ディレクティブでを使用することを指定します。  
  
    ```aspx-csharp
    <%@ServiceHost
        language=c#
        Debug="true"
        Service="Microsoft.Ajax.Samples.MusicService"  
        Factory=System.ServiceModel.Activation.WebScriptServiceHostFactory  
    %>  
    ```  
  
## <a name="to-call-the-service"></a>サービスを呼び出すには  
  
1. ブラウザーを使用すると、クライアントのコードなしでサービスの GET 操作をテストできます。 たとえば、サービスがアドレスで構成されている場合、 `http://example.com/service.svc` `http://example.com/service.svc/LookUpArtist?album=SomeAlbum` ブラウザーのアドレスバーに「」と入力すると、サービスが呼び出され、応答がダウンロードまたは表示されます。
  
2. GET 操作によるサービスは、他の ASP.NET AJAX サービスと同様に、サービス URL を ASP.NET AJAX Script Manager コントロールのスクリプト コレクションに入力することで使用できます。 例については、「[基本的な AJAX サービス](../samples/basic-ajax-service.md)」を参照してください。
  
## <a name="see-also"></a>関連項目

- [ASP.NET AJAX 用の WCF サービスの作成](creating-wcf-services-for-aspnet-ajax.md)
- [方法: AJAX 対応 ASP.NET Web サービスを WCF に移行する](how-to-migrate-ajax-enabled-aspnet-web-services-to-wcf.md)
