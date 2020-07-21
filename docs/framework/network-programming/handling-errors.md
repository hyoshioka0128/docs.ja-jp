---
title: エラー処理
description: WebRequest と WebResponse によってスローされるシステムおよび Web 固有の例外について学習します。 問題を理解して解決するには、Status プロパティを使用します。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Internet, WebRequest and WebResponse classes exceptions
- Status property
- WebExceptions class, about WebExceptions class
- Timeout enumeration member
- ConnectFailure enumeration member
- TrustFailure enumeration member
- WebRequest class, exceptions
- requesting data from Internet, error handling
- Success enumeration member
- receiving data, errors
- ProtocolError enumeration member
- downloading Internet resources, error handling
- WebResponse class, exceptions
- SendFailure enumeration member
- errors [.NET Framework], WebRequest and WebResponse classes exceptions
- sending data, errors
- response to Internet request, error handling
- NameResolutionFailure enumeration member
- KeepAliveFailure enumeration member
- network resources, WebRequest and WebResponse classes exceptions
- RequestCanceled enumeration member
- ReceiveFailure enumeration member
- ServerProtocolViolation enumeration member
- ConnectionClosed enumeration member
- SecureChannelFailure enumeration member
ms.assetid: 657141cd-5cf5-4fdb-a4b2-4c040eba84b5
ms.openlocfilehash: 786b2bd8bc4d1b394bcfe920053b2f4f55d1cdea
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84502575"
---
# <a name="handling-errors"></a>エラー処理

<xref:System.Net.WebRequest> および <xref:System.Net.WebResponse> クラスでは、システム例外 (<xref:System.ArgumentException> など) と Web 固有の例外 (<xref:System.Net.WebRequest.GetResponse%2A> メソッドでスローされる <xref:System.Net.WebException>) の両方がスローされます。  
  
各 **WebException** には、<xref:System.Net.WebExceptionStatus> 列挙体からの値を含む <xref:System.Net.WebException.Status%2A> プロパティがあります。 **Status** プロパティを調べることで、発生したエラーを特定し、エラーを解決するための適切な手順を実行することができます。  
  
**Status** プロパティの有効な値を次の表に示します。  
  
|Status|説明|  
|------------|-----------------|  
|ConnectFailure|トランスポート レベルでリモート サービスに接続できませんでした。|  
|ConnectionClosed|接続は処理の途中で中断されました。|  
|KeepAliveFailure|サーバーは、Keep-alive ヘッダーの設定による接続を閉じました。|  
|NameResolutionFailure|ドメイン サービスがホスト名を解決できませんでした。|  
|ProtocolError|サーバーから受信された応答は完全でしたが、プロトコル レベルのエラーが示されています。|  
|ReceiveFailure|完全な応答がリモート サーバーから受信されませんでした。|  
|RequestCanceled|要求は取り消されました。|  
|SecureChannelFailure|セキュリティで保護されたチャネル リンクでエラーが発生しました。|  
|SendFailure|リモート サーバーに完全な要求を送信できませでした。|  
|ServerProtocolViolation|サーバーの応答が有効な HTTP 応答ではありません。|  
|成功|エラーは発生しませんでした。|  
|Timeout|要求に対して設定されたタイムアウト時間内で応答が受信されませんでした。|  
|TrustFailure|サーバー証明書を検証できませんでした。|  
|MessageLengthLimitExceeded|要求の送信時またはサーバーから応答の受信時に指定された制限を超えるメッセージが受信されました。|  
|保留|内部非同期要求が保留中です。|  
|PipelineFailure|この値は .NET Framework インフラストラクチャをサポートします。独自に作成したコードで直接使用するためのものではありません。|  
|ProxyNameResolutionFailure|ネーム リゾルバー サービスがプロキシ ホスト名を解決できませんでした。|  
|UnknownError|不明な種類の例外が発生しました。|  
  
**Status** プロパティが **WebExceptionStatus.ProtocolError** である場合は、サーバーからの応答を含む **WebResponse** を使用できます。 この応答を調べることで、プロトコル エラーの実際の原因を判別できます。  
  
次の例は、**WebException** をキャッチする方法を示しています。  
  
```csharp  
try
{  
    // Create a request instance.  
    WebRequest myRequest =
    WebRequest.Create("http://www.contoso.com");  
    // Get the response.  
    WebResponse myResponse = myRequest.GetResponse();  
    //Get a readable stream from the server.
    Stream sr = myResponse.GetResponseStream();  
  
    //Read from the stream and write any data to the console.  
    bytesread = sr.Read( myBuffer, 0, length);  
    while( bytesread > 0 )
    {  
        for (int i=0; i<bytesread; i++) {  
            Console.Write( "{0}", myBuffer[i]);  
        }  
        Console.WriteLine();  
        bytesread = sr.Read( myBuffer, 0, length);  
    }  
    sr.Close();  
    myResponse.Close();  
}  
catch (WebException webExcp)
{  
    // If you reach this point, an exception has been caught.  
    Console.WriteLine("A WebException has been caught.");  
    // Write out the WebException message.  
    Console.WriteLine(webExcp.ToString());  
    // Get the WebException status code.  
    WebExceptionStatus status =  webExcp.Status;  
    // If status is WebExceptionStatus.ProtocolError,
    //   there has been a protocol error and a WebResponse
    //   should exist. Display the protocol error.  
    if (status == WebExceptionStatus.ProtocolError) {  
        Console.Write("The server returned protocol error ");  
        // Get HttpWebResponse so that you can check the HTTP status code.  
        HttpWebResponse httpResponse = (HttpWebResponse)webExcp.Response;  
        Console.WriteLine((int)httpResponse.StatusCode + " - "  
           + httpResponse.StatusCode);  
    }  
}  
catch (Exception e)
{  
    // Code to catch other exceptions goes here.  
}  
```  
  
```vb  
Try  
    ' Create a request instance.  
    Dim myRequest As WebRequest = WebRequest.Create("http://www.contoso.com")  
    ' Get the response.  
    Dim myResponse As WebResponse = myRequest.GetResponse()  
    'Get a readable stream from the server.
    Dim sr As Stream = myResponse.GetResponseStream()  
  
    Dim i As Integer
    'Read from the stream and write any data to the console.  
    bytesread = sr.Read(myBuffer, 0, length)  
    While bytesread > 0  
        For i = 0 To bytesread - 1  
            Console.Write("{0}", myBuffer(i))  
        Next i  
        Console.WriteLine()  
        bytesread = sr.Read(myBuffer, 0, length)  
    End While  
    sr.Close()  
    myResponse.Close()  
Catch webExcp As WebException  
    ' If you reach this point, an exception has been caught.  
    Console.WriteLine("A WebException has been caught.")  
    ' Write out the WebException message.  
    Console.WriteLine(webExcp.ToString())  
    ' Get the WebException status code.  
    Dim status As WebExceptionStatus = webExcp.Status  
    ' If status is WebExceptionStatus.ProtocolError,
    '   there has been a protocol error and a WebResponse
    '   should exist. Display the protocol error.  
    If status = WebExceptionStatus.ProtocolError Then  
        Console.Write("The server returned protocol error ")  
        ' Get HttpWebResponse so that you can check the HTTP status code.  
        Dim httpResponse As HttpWebResponse = _  
           CType(webExcp.Response, HttpWebResponse)  
        Console.WriteLine(CInt(httpResponse.StatusCode).ToString() & _  
           " - " & httpResponse.StatusCode.ToString())  
    End If  
Catch e As Exception  
    ' Code to catch other exceptions goes here.  
End Try  
```  
  
Windows ソケットでエラーが発生した場合、<xref:System.Net.Sockets.Socket> クラスを使用するアプリケーションは <xref:System.Net.Sockets.SocketException> をスローします。 <xref:System.Net.Sockets.TcpClient>、<xref:System.Net.Sockets.TcpListener>、および <xref:System.Net.Sockets.UdpClient> は **Socket** クラスに基づくものであり、同様に **SocketExceptions** をスローします。  
  
**SocketException** がスローされると、**SocketException** クラスは <xref:System.Net.Sockets.SocketException.ErrorCode%2A> プロパティを、最後に発生したオペレーティング システムのソケット エラーに設定します。 ソケット エラー コードの詳細については、MSDN の Winsock 2.0 API エラー コードに関するドキュメントを参照してください。  
  
## <a name="see-also"></a>関連項目

- [.NET での例外の処理とスロー](../../standard/exceptions/index.md)
- [データの要求](requesting-data.md)
