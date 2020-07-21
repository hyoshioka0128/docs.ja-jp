---
title: WCF Web HTTP 書式設定
ms.date: 03/30/2017
ms.assetid: e2414896-5463-41cd-b0a6-026a713eac2c
ms.openlocfilehash: 011ff4f2e667268fac1aa2d82c0a2c4ffefc8dde
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84585559"
---
# <a name="wcf-web-http-formatting"></a>WCF Web HTTP 書式設定
WCF Web HTTP プログラミング モデルでは、サービス操作で返す応答の最適な形式を動的に判断できます。 適切な形式を判断するための方法として、自動と明示的の 2 つがサポートされます。  
  
## <a name="automatic-formatting"></a>自動書式  
 有効にした場合は、応答を返す最適な形式が自動選択によって選択されます。 最適な形式の判断は、次の項目をこの順序で確認することで行われます。  
  
1. 要求メッセージの Accept ヘッダーのメディアの種類。  
  
2. 要求メッセージのコンテンツの種類。  
  
3. その処理での既定の形式設定。  
  
4. WebHttpBehavior での既定の形式設定。  
  
 要求メッセージに Accept ヘッダーが含まれている場合は、Windows Communication Foundation (WCF) インフラストラクチャによって、サポートされている型が検索されます。 `Accept` ヘッダーにメディアの種類のプロパティが指定されている場合は、それに従います。 適切な形式が `Accept` ヘッダーで見つからない場合は、要求メッセージのコンテンツの種類が使用されます。 適切なコンテンツの種類が指定されていない場合は、その操作の既定の形式設定が使用されます。 既定の形式は、`ResponseFormat` の <xref:System.ServiceModel.Web.WebGetAttribute> パラメーターおよび <xref:System.ServiceModel.Web.WebInvokeAttribute> 属性で設定されます。 その操作に既定の形式が指定されていない場合は、<xref:System.ServiceModel.Description.WebHttpBehavior.DefaultOutgoingResponseFormat%2A> プロパティの値が使用されます。 形式の自動選択は、<xref:System.ServiceModel.Description.WebHttpBehavior.AutomaticFormatSelectionEnabled%2A> プロパティに依存します。 このプロパティが `true` に設定されている場合は、使用する最適な形式が WCF インフラストラクチャで決定されます。 形式の自動選択は、既定で、下位互換性のために無効になっています。 形式の自動選択は、プログラムで有効にすることも、構成ファイルを使用して有効にすることもできます。 形式の自動選択をコードで有効にする方法を次の例に示します。  
  
```csharp
// This code assumes the service name is MyService and the service contract is IMyContract
Uri baseAddress = new Uri("http://localhost:8000");  
  
WebServiceHost host = new WebServiceHost(typeof(MyService), baseAddress)  
try  
{  
   ServiceEndpoint sep = host.AddServiceEndpoint(typeof(IMyContract), new WebHttpBinding(), "");  
   // Check it see if the WebHttpBehavior already exists  
   WebHttpBehavior whb = sep.Behaviors.Find<WebHttpBehavior>();  
  
   if (whb != null)  
   {  
      whb.AutomaticFormatSelectionEnabled = true;  
   }  
   else  
   {  
      WebHttpBehavior webBehavior = new WebHttpBehavior();  
      webBehavior.AutomaticFormatSelectionEnabled = true;  
      sep.Behaviors.Add(webBehavior);  
   }  
         // Open host to start listening for messages  
   host.Open();
  
  // ...  
}  
  catch(CommunicationException ex)  
  {  
     Console.WriteLine("An exception occurred: " + ex.Message());  
  }  
```  
  
 形式の自動選択は、構成ファイルを使用して有効にすることもできます。 <xref:System.ServiceModel.Description.WebHttpBehavior.AutomaticFormatSelectionEnabled%2A> プロパティは、<xref:System.ServiceModel.Description.WebHttpBehavior> で直接、または <xref:System.ServiceModel.Description.WebHttpEndpoint> を使用して設定できます。 形式の自動選択を <xref:System.ServiceModel.Description.WebHttpBehavior> で有効にする方法を次の例に示します。  
  
```xml  
<system.serviceModel>  
  <behaviors>  
    <endpointBehaviors>  
      <behavior>  
        <webHttp automaticFormatSelectionEnabled="true" />  
      </behavior>  
    </endpointBehaviors>  
  </behaviors>  
  <standardEndpoints>  
    <webHttpEndpoint>  
      <!-- the "" standard endpoint is used by WebServiceHost for auto creating a web endpoint. -->  
      <standardEndpoint name="" helpEnabled="true" />  
    </webHttpEndpoint>  
  </standardEndpoints>  
</system.serviceModel>  
```  
  
 形式の自動選択を、<xref:System.ServiceModel.Description.WebHttpEndpoint> を使用して有効にする方法を次の例に示します。  
  
```xml  
<system.serviceModel>  
    <standardEndpoints>  
      <webHttpEndpoint>  
        <!-- the "" standard endpoint is used by WebServiceHost for auto creating a web endpoint. -->  
        <standardEndpoint name="" helpEnabled="true" automaticFormatSelectionEnabled="true"  />  
      </webHttpEndpoint>  
    </standardEndpoints>  
  </system.serviceModel>  
```  
  
## <a name="explicit-formatting"></a>明示的な書式設定  
 名前が示すように、形式の明示的な選択では、操作コード内に使用する最適な形式を開発者が判断します。 最適な形式が XML または JSON の場合は、開発者が <xref:System.ServiceModel.Web.OutgoingWebResponseContext.Format%2A> を <xref:System.ServiceModel.Web.WebMessageFormat.Xml> または <xref:System.ServiceModel.Web.WebMessageFormat.Json> のいずれかに設定します。 <xref:System.ServiceModel.Web.OutgoingWebResponseContext.Format%2A> プロパティが明示的に設定されていない場合は、その操作の既定の形式が使用されます。  
  
 次の例では、使用する形式に対する形式クエリ文字列パラメーターを確認します。 指定されている場合、その操作の形式は <xref:System.ServiceModel.Web.OutgoingWebResponseContext.Format%2A> を使用して設定されます。  
  
```csharp
public class Service : IService  
{  
    [WebGet]  
     public string EchoWithGet(string s)  
    {  
        // if a format query string parameter has been specified, set the response format to that. If no such
        // query string parameter exists the Accept header will be used
        string formatQueryStringValue = WebOperationContext.Current.IncomingRequest.UriTemplateMatch.QueryParameters["format"];  
        if (!string.IsNullOrEmpty(formatQueryStringValue))  
        {  
            if (formatQueryStringValue.Equals("xml", System.StringComparison.OrdinalIgnoreCase))  
            {
                WebOperationContext.Current.OutgoingResponse.Format = WebMessageFormat.Xml;
            }
            else if (formatQueryStringValue.Equals("json", System.StringComparison.OrdinalIgnoreCase))  
            {  
                WebOperationContext.Current.OutgoingResponse.Format = WebMessageFormat.Json;  
            }  
            else  
            {  
                throw new WebFaultException<string>($"Unsupported format '{formatQueryStringValue}'",   HttpStatusCode.BadRequest);
            }  
        }  
        return "You said " + s;  
    }  
```  
  
 XML または JSON 以外の形式をサポートする必要がある場合は、操作に <xref:System.ServiceModel.Channels.Message> の戻り値の型があるように定義します。 操作コード内で、使用する適切な形式を決定し、次のメソッドのいずれかを使用して <xref:System.ServiceModel.Channels.Message> オブジェクトを作成します。  
  
- `WebOperationContext.CreateAtom10Response`  
  
- `WebOperationContext.CreateJsonResponse`  
  
- `WebOperationContext.CreateStreamResponse`  
  
- `WebOperationContext.CreateTextResponse`  
  
- `WebOperationContext.CreateXmlResponse`  
  
 これらの各メソッドでは、この適切な形式でコンテンツを取得してメッセージを作成します。 `WebOperationContext.Current.IncomingRequest.GetAcceptHeaderElements` メソッドは、クライアントで優先される形式の一覧を優先度が高い順に取得するために使用できます。 次の例では、`WebOperationContext.Current.IncomingRequest.GetAcceptHeaderElements` を使用して使用形式を決定し、適切な作成応答メソッドを使用して応答メッセージを作成する方法を示します。  
  
```csharp
public class Service : IService  
{  
    public Message EchoListWithGet(string list)  
    {  
        List<string> returnList = new List<string>(list.Split(new char[] { ',' }, StringSplitOptions.RemoveEmptyEntries));  
        IList<ContentType> acceptHeaderElements = WebOperationContext.Current.IncomingRequest.GetAcceptHeaderElements();  
        for (int x = 0; x < acceptHeaderElements.Count; x++)  
        {  
            string normalizedMediaType = acceptHeaderElements[x].MediaType.ToLowerInvariant();  
            switch (normalizedMediaType)  
            {  
                case "image/jpeg": return CreateJpegResponse(returnList);  
                case "application/xhtml+xml": return CreateXhtmlResponse(returnList);  
                case "application/atom+xml": return CreateAtom10Response(returnList);  
                case "application/xml": return CreateXmlResponse(returnList);  
                case "application/json": return CreateJsonResponse(returnList);  
          }  
    }  
  
    // Default response format is XML  
    return CreateXmlResponse(returnList);  
    }  
}  
```  
  
## <a name="see-also"></a>関連項目

- <xref:System.UriTemplate>
- <xref:System.UriTemplateMatch>
- [WCF Web HTTP プログラミング モデル](wcf-web-http-programming-model.md)
- [UriTemplate と UriTemplateTable](uritemplate-and-uritemplatetable.md)
- [WCF Web HTTP プログラミング モデルの概要](wcf-web-http-programming-model-overview.md)
- [WCF Web HTTP プログラミング オブジェクト モデル](wcf-web-http-programming-object-model.md)
