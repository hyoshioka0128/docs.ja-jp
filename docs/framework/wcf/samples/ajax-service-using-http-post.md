---
title: HTTP POST を使用する AJAX サービス
ms.date: 03/30/2017
ms.assetid: 1ac80f20-ac1c-4ed1-9850-7e49569ff44e
ms.openlocfilehash: 143585b40a493983b7265971a17224165de6f36d
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84575889"
---
# <a name="ajax-service-using-http-post"></a>HTTP POST を使用する AJAX サービス

このサンプルでは、Windows Communication Foundation (WCF) を使用して、HTTP POST を使用する AJAX (ASP.NET 非同期 JavaScript and XML) サービスを作成する方法を示します。 AJAX サービスには、Web ブラウザー クライアントから基本的な JavaScript コードを使用してアクセスできます。 このサンプルは、[基本的な AJAX サービス](basic-ajax-service.md)のサンプルに基づいています。2つのサンプルの唯一の違いは、http GET の代わりに HTTP POST を使用することです。

Windows Communication Foundation (WCF) での AJAX サポートは、コントロールを介して ASP.NET AJAX で使用できるように最適化されてい `ScriptManager` ます。 ASP.NET AJAX で WCF を使用する例については、 [ajax のサンプル](ajax-service-using-http-post.md)を参照してください。

> [!NOTE]
> このサンプルのセットアップ手順とビルド手順については、このトピックの最後を参照してください。

次のサンプルのサービスは、AJAX 固有のコードを持たない WCF サービスです。

属性が操作に適用されている場合、または属性が適用されていない場合は、 <xref:System.ServiceModel.Web.WebInvokeAttribute> <xref:System.ServiceModel.Web.WebGetAttribute> 既定の HTTP 動詞 ("POST") が使用されます。 POST 要求は、GET 要求よりも作成が困難ですが、キャッシュされません。キャッシュが不適切な操作に対しては、POST 要求を使用します。

```csharp
[ServiceContract(Namespace = "PostAjaxService")]
public interface ICalculator
{
    [WebInvoke]
    double Add(double n1, double n2);
    //Other operations omitted…
}
```

基本的な AJAX サービスのサンプルの場合と同様に、<xref:System.ServiceModel.Activation.WebScriptServiceHostFactory> を使用してサービスに AJAX エンドポイントを作成します。

GET 要求とは異なり、POST サービスはブラウザーから呼び出すことができません。 たとえば、に移動する `http://localhost/ServiceModelSamples/service.svc/Add?n1=100&n2=200` と、エラーが発生します。これは、POST サービスでは、 `n1` `n2` URL ではなく JSON 形式のメッセージ本文で、およびパラメーターが送信されることを想定しているためです。

クライアントの Web ページの PostAjaxClientPage.aspx には、ユーザーがページ上のいずれかの操作ボタンをクリックするとサービスを呼び出す ASP.NET コードが含まれています。 サービスは、[基本 AJAX サービス](basic-ajax-service.md)サンプルと同じ方法で GET 要求を使用して応答します。

> [!IMPORTANT]
> サンプルは、既にコンピューターにインストールされている場合があります。 続行する前に、次の (既定の) ディレクトリを確認してください。
>
> `<InstallDrive>:\WF_WCF_Samples`
>
> このディレクトリが存在しない場合は、 [Windows Communication Foundation (wcf) および Windows Workflow Foundation (WF) のサンプルの .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459)にアクセスして、すべての WINDOWS COMMUNICATION FOUNDATION (wcf) とサンプルをダウンロードして [!INCLUDE[wf1](../../../../includes/wf1-md.md)] ください。 このサンプルは、次のディレクトリに格納されます。
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Ajax\PostAjaxService`

## <a name="to-set-up-build-and-run-the-sample"></a>サンプルをセットアップ、ビルド、および実行するには

1. [Windows Communication Foundation のサンプルについ](one-time-setup-procedure-for-the-wcf-samples.md)ては、セットアップ手順の1回限りのセットアップ手順を実行してください。

2. 「 [Windows Communication Foundation サンプルのビルド](building-the-samples.md)」の説明に従って、ソリューション postajaxservice.sln をビルドします。

3. に移動 `http://localhost/ServiceModelSamples/PostAjaxClientPage.aspx` します (プロジェクトディレクトリからブラウザーで postajaxclientpage.aspx を開かないでください)。
