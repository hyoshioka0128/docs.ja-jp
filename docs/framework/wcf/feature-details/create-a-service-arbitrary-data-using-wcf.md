---
title: '方法: WCF REST プログラミング モデルを使用して任意のデータを受け入れるサービスを作成する'
ms.date: 03/30/2017
ms.assetid: e566c15a-b600-4e4a-be3a-4af43e767dae
ms.openlocfilehash: d908651f7815c102b45ea106f5bec4c07d869950
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84601336"
---
# <a name="how-to-create-a-service-that-accepts-arbitrary-data-using-the-wcf-rest-programming-model"></a>方法: WCF REST プログラミング モデルを使用して任意のデータを受け入れるサービスを作成する
開発者は、データがサービス操作から返される流れを完全に制御する必要が生じることがあります。 これは、サービス操作が、byWCF でサポートされていない形式でデータを返す必要がある場合に当てはまります。 このトピックでは、WCF REST プログラミングモデルを使用して、任意のデータを受信するサービスを作成する方法について説明します。  
  
### <a name="to-implement-the-service-contract"></a>サービス コントラクトを実装するには  
  
1. サービス コントラクトを定義します。 任意のデータを受信する操作には、<xref:System.IO.Stream> 型のパラメーターが必要です。 さらに、このパラメーターは要求の本文に渡される唯一のパラメーターでなければなりません。 この例で説明されている操作では、filename パラメーターも使用できます。 このパラメーターは要求の URL に格納されて渡されます。 <xref:System.UriTemplate> で <xref:System.ServiceModel.Web.WebInvokeAttribute> を指定すると、パラメーターが URL に格納されて渡されるように指定できます。 この場合、このメソッドの呼び出しに使用される URI は、"UploadFile/Some Filename" で終了します。 URI テンプレートの "{filename}" 部分では、操作の filename パラメーターが、操作の呼び出しに使用される URI 内で渡されることを指定します。  
  
    ```csharp  
     [ServiceContract]  
    public interface IReceiveData  
    {  
        [WebInvoke(UriTemplate = "UploadFile/{fileName}")]  
        void UploadFile(string fileName, Stream fileContents);  
    }  
    ```  
  
2. サービス コントラクトを実装します。 コントラクトには、ストリーム内の任意のデータのファイルを受け取る `UploadFile` というメソッドが 1 つだけあります。 操作では、ストリームを読み取り、読み取ったバイト数をカウントしてから、ファイル名と読み取ったバイト数を表示します。  
  
    ```csharp  
    public class RawDataService : IReceiveData  
    {  
        public void UploadFile(string fileName, Stream fileContents)  
        {  
            byte[] buffer = new byte[10000];  
            int bytesRead, totalBytesRead = 0;  
            do  
            {  
                bytesRead = fileContents.Read(buffer, 0, buffer.Length);  
                totalBytesRead += bytesRead;  
            } while (bytesRead > 0);  
            Console.WriteLine("Service: Received file {0} with {1} bytes", fileName, totalBytesRead);  
        }  
    }  
    ```  
  
### <a name="to-host-the-service"></a>サービスをホストするには  
  
1. コンソール アプリケーションを作成し、サービスをホストします。  
  
    ```csharp  
    class Program  
    {  
       static void Main(string[] args)  
       {  
       }  
    }  
    ```  
  
2. 変数を作成し、`Main` メソッド内のサービスに使用するベース アドレスを保持します。  
  
    ```csharp  
    string baseAddress = "http://" + Environment.MachineName + ":8000/Service";  
    ```  
  
3. サービスの <xref:System.ServiceModel.ServiceHost> インスタンスを作成して、サービス クラスとベース アドレスを指定します。  
  
    ```csharp  
    ServiceHost host = new ServiceHost(typeof(RawDataService), new Uri(baseAddress));  
    ```  
  
4. コントラクト、<xref:System.ServiceModel.WebHttpBinding>、および <xref:System.ServiceModel.Description.WebHttpBehavior> を指定するエンドポイントを追加します。  
  
    ```csharp  
    host.AddServiceEndpoint(typeof(IReceiveData), new WebHttpBinding(), "").Behaviors.Add(new WebHttpBehavior());  
    ```  
  
5. サービス ホストを開きます。 サービスは要求を受け取る準備ができました。  
  
    ```csharp  
    host.Open();  
    Console.WriteLine("Host opened");  
    ```  
  
### <a name="to-call-the-service-programmatically"></a>プログラムによってサービスを呼び出すには  
  
1. サービスの呼び出しに使用する URI で <xref:System.Net.HttpWebRequest> を作成します。 このコードでは、ベース アドレスは `"/UploadFile/Text"` と組み合わされています。 URI の `"UploadFile"` 部分で呼び出す操作を指定します。 URI の `"Test.txt"` 部分で `UploadFile` 操作に渡す filename パラメーターを指定します。 これらの項目はいずれも操作コントラクトに適用された <xref:System.UriTemplate> にマップされます。  
  
    ```csharp  
    HttpWebRequest req = (HttpWebRequest)HttpWebRequest.Create(baseAddress + "/UploadFile/Test.txt");  
    ```  
  
2. <xref:System.Net.HttpWebRequest.Method%2A> の <xref:System.Net.HttpWebRequest> プロパティを `POST`、<xref:System.Net.HttpWebRequest.ContentType%2A> プロパティを `"text/plain"` にそれぞれ設定します。 この設定により、サービスはコードがデータを送信し、そのデータがプレーン テキストであることを認識します。  
  
    ```csharp  
    req.Method = "POST";  
    req.ContentType = "text/plain";  
    ```  
  
3. <xref:System.Net.HttpWebRequest.GetRequestStream%2A> を呼び出すと、要求ストリームの取得や送信するデータの作成ができます。また、そのデータの要求ストリームに書き込んだり、ストリームを閉じることもできます。  
  
    ```csharp  
    Stream reqStream = req.GetRequestStream();  
    byte[] fileToSend = new byte[12345];  
    for (int i = 0; i < fileToSend.Length; i++)  
       {  
           fileToSend[i] = (byte)('a' + (i % 26));  
       }  
    reqStream.Write(fileToSend, 0, fileToSend.Length);  
    reqStream.Close();  
    ```  
  
4. <xref:System.Net.HttpWebRequest.GetResponse%2A> を呼び出してサービスから応答を取得すると、応答データをコンソールに表示できます。  
  
    ```csharp  
    HttpWebResponse resp = (HttpWebResponse)req.GetResponse();  
    Console.WriteLine("Client: Receive Response HTTP/{0} {1} {2}", resp.ProtocolVersion, (int)resp.StatusCode, resp.StatusDescription);  
    ```  
  
5. サービス ホストを閉じます。  
  
    ```csharp  
    host.Close();  
    ```  
  
## <a name="example"></a>例  
 この例で使用されているコードの完全な一覧を次に示します。  
  
```csharp  
using System;  
using System.Collections.Generic;  
using System.Text;  
using System.ServiceModel;  
using System.ServiceModel.Web;  
using System.ServiceModel.Description;  
using System.IO;  
using System.Net;  
  
namespace ReceiveRawData  
{  
    [ServiceContract]  
    public interface IReceiveData  
    {  
        [WebInvoke(UriTemplate = "UploadFile/{fileName}")]  
        void UploadFile(string fileName, Stream fileContents);  
    }  
    public class RawDataService : IReceiveData  
    {  
        public void UploadFile(string fileName, Stream fileContents)  
        {  
            byte[] buffer = new byte[10000];  
            int bytesRead, totalBytesRead = 0;  
            do  
            {  
                bytesRead = fileContents.Read(buffer, 0, buffer.Length);  
                totalBytesRead += bytesRead;  
            } while (bytesRead > 0);  
            Console.WriteLine("Service: Received file {0} with {1} bytes", fileName, totalBytesRead);  
        }  
    }  
  
    class Program  
    {  
        static void Main(string[] args)  
        {  
            string baseAddress = "http://" + Environment.MachineName + ":8000/Service";  
            ServiceHost host = new ServiceHost(typeof(RawDataService), new Uri(baseAddress));  
            host.AddServiceEndpoint(typeof(IReceiveData), new WebHttpBinding(), "").Behaviors.Add(new WebHttpBehavior());  
            host.Open();  
            Console.WriteLine("Host opened");  
  
            HttpWebRequest req = (HttpWebRequest)HttpWebRequest.Create(baseAddress + "/UploadFile/Test.txt");  
            req.Method = "POST";  
            req.ContentType = "text/plain";  
            Stream reqStream = req.GetRequestStream();  
            byte[] fileToSend = new byte[12345];  
            for (int i = 0; i < fileToSend.Length; i++)  
            {  
                fileToSend[i] = (byte)('a' + (i % 26));  
            }  
            reqStream.Write(fileToSend, 0, fileToSend.Length);  
            reqStream.Close();  
            HttpWebResponse resp = (HttpWebResponse)req.GetResponse();  
            Console.WriteLine("Client: Receive Response HTTP/{0} {1} {2}", resp.ProtocolVersion, (int)resp.StatusCode, resp.StatusDescription);  
            host.Close();  
  
        }  
    }  
}  
```  
  
## <a name="compiling-the-code"></a>コードのコンパイル  
  
- コードのコンパイル時には、System.ServiceModel.dll と System.ServiceModel.Web.dll を参照します。  
  
## <a name="see-also"></a>関連項目

- [UriTemplate と UriTemplateTable](uritemplate-and-uritemplatetable.md)
- [WCF Web HTTP プログラミング モデル](wcf-web-http-programming-model.md)
- [WCF Web HTTP プログラミング モデルの概要](wcf-web-http-programming-model-overview.md)
