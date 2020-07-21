---
title: '方法: 構成ファイルを使用してサービスのメタデータを公開する'
description: 構成ファイルを使用して、WCF サービスのメタデータを公開する方法について説明します。 公開により、クライアントは GET または HTTP/GET 要求を使用してそのメタデータを取得できます。
ms.date: 03/30/2017
ms.assetid: f061443f-92df-4824-b36a-609c4cd14a17
ms.openlocfilehash: d5d425be7f02a204476c4f6e81441aca9ea39fcc
ms.sourcegitcommit: 358a28048f36a8dca39a9fe6e6ac1f1913acadd5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85246819"
---
# <a name="how-to-publish-metadata-for-a-service-using-a-configuration-file"></a>方法: 構成ファイルを使用してサービスのメタデータを公開する
これは、Windows Communication Foundation (WCF) サービスのメタデータの公開を示す2つの操作方法に関するトピックの1つです。 構成ファイルとコードを使用して、サービスがメタデータを公開する手段を指定する方法は 2 つあります。 このトピックでは、構成ファイルを使用してサービスのメタデータを公開する方法について説明します。  
  
> [!CAUTION]
> このトピックでは、セキュリティで保護されていない方法でメタデータを公開する方法について説明します。 クライアントは、サービスからメタデータを取得できます。 セキュリティで保護された方法でメタデータを公開するようサービスに要求する場合は、「[カスタムセキュアメタデータエンドポイント](../samples/custom-secure-metadata-endpoint.md)」を参照してください。  
  
 コードでのメタデータの公開の詳細については、「[方法: コードを使用してサービスのメタデータを公開](how-to-publish-metadata-for-a-service-using-code.md)する」を参照してください。 メタデータを公開すると、クライアントが `?wsdl` クエリ文字列を使用した WS-Transfer GET 要求または HTTP/GET 要求によりメタデータを取得できるようになります。 コードが動作することを確認するには、基本的な WCF サービスを作成します。 簡略化のため、次のコードに基本的な自己ホスト型サービスが用意されています。  
  
```csharp  
using System;  
using System.Runtime.Serialization;  
using System.ServiceModel;  
using System.ServiceModel.Description;  
  
namespace Metadata.Samples  
{  
    [ServiceContract]  
    public interface ISimpleService  
    {  
        [OperationContract]  
        string SimpleMethod(string msg);  
    }  
  
    class SimpleService : ISimpleService  
    {  
        public string SimpleMethod(string msg)  
        {  
            Console.WriteLine("The caller passed in " + msg);  
            return "Hello " + msg;  
        }  
    }  
  
    class Program  
    {  
        static void Main(string[] args)  
        {  
            ServiceHost host = new ServiceHost(typeof(SimpleService),  
                new Uri("http://localhost:8001/MetadataSample"));
            try  
            {  
                // Open the service host to accept incoming calls  
                host.Open();  
  
                // The service can now be accessed.  
                Console.WriteLine("The service is ready.");  
                Console.WriteLine("Press <ENTER> to terminate service.");  
                Console.WriteLine();  
                Console.ReadLine();  
  
                // Close the ServiceHostBase to shutdown the service.  
                host.Close();  
            }  
            catch (CommunicationException commProblem)  
            {  
                Console.WriteLine("There was a communication problem. " + commProblem.Message);  
                Console.Read();  
            }  
        }  
    }  
}  
```  
  
 これは、構成ファイルを使用して構成された自己ホスト型サービスです。 以下の構成ファイルをベースとして使用します。  
  
```xml  
<configuration>  
  <system.serviceModel>  
    <services>  
      <service name="Metadata.Example.SimpleService">  
        <endpoint address=""  
                  binding="basicHttpBinding"  
                  contract="Metadata.Example.ISimpleService" />  
      </service>  
    </services>  
    <behaviors>  
  
    </behaviors>  
  </system.serviceModel>  
</configuration>  
```  
  
### <a name="to-publish-metadata-for-a-wcf-service-using-an-application-configuration-file"></a>アプリケーション構成ファイルを使用して WCF サービスのメタデータを公開するには  
  
1. `</services>` 要素を閉じた後、App.config ファイル内に `<behaviors>` 要素を作成します。  

2. `<behaviors>` 要素内に、`<serviceBehaviors>` 要素を追加します。  

3. `<behavior>`要素に `<serviceBehaviors>` 要素を追加し、`name` 要素の `<behavior>` 属性に値を指定します。  

4. `<serviceMetadata>` 要素を `<behavior>` 要素に追加します。 `httpGetEnabled` 属性を `true` に設定し、`policyVersion` 属性を Policy15 に設定します。 `httpGetEnabled` により、サービスは HTTP GET 要求からのメタデータ要求に応答できるようになります。 `policyVersion` は、サービスに対して、WS-Policy 1.5 準拠でメタデータを生成するように指示します。  

5. 次のコード例に示すように、`behaviorConfiguration` 要素に `<service>` 属性を追加し、手順 1. で追加した `name` 要素の `<behavior>` 属性を指定します。  
  
    ```xml  
    <services>  
      <service  
          name="Metadata.Example.SimpleService"  
          behaviorConfiguration="SimpleServiceBehavior">  
        ...  
      </service>  
    </services>  
    <behaviors>  
      <serviceBehaviors>  
        <behavior name="SimpleServiceBehavior">  
          <serviceMetadata httpGetEnabled="True" policyVersion="Policy15" />  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
    ```  
  
6. 1 つ以上の `<endpoint>` 要素を追加して、コントラクトを `IMetadataExchange` に設定します。コード例を次に示します。  
  
    ```xml  
    <services>  
      <service  
          name="Metadata.Example.SimpleService"  
          behaviorConfiguration="SimpleServiceBehavior">  
  
        <endpoint address=""  
                  binding="wsHttpBinding"  
                  contract="Metadata.Example.ISimpleService" />  
  
        <endpoint address="mex"  
                  binding="mexHttpBinding"  
                  contract="IMetadataExchange" />  
      </service>  
    </services>  
    ```  
  
7. 前の手順で追加したメタデータ エンドポイントについて、`binding` 属性に次のいずれかの値を設定します。  
  
    - HTTP 公開の場合、`mexHttpBinding`  
  
    - HTTPS 公開の場合、`mexHttpsBinding`  
  
    - 名前付きパイプ公開の場合、`mexNamedPipeBinding`  
  
    - TCP 公開の場合、`mexTcpBinding`  
  
8. 前の手順で追加したメタデータ エンドポイントについて、次のいずれかに等しいアドレスを設定します。  
  
    - ベース アドレスがメタデータ バインディングと同じ場合に、公開ポイントとしてホスト アプリケーションのベース アドレスを使用するための空の文字列  
  
    - ホスト アプリケーションにベース アドレスがある場合、相対アドレス  
  
    - 絶対アドレス  
  
9. コンソール アプリケーションをビルドして実行します。  
  
10. Internet Explorer を使用してサービスのベースアドレス ( `http://localhost:8001/MetadataSample` このサンプルでは) を参照し、メタデータの公開が有効になっていることを確認します。 有効になっていない場合は、"このサービスのメタデータ公開は現在は無効になっています。" というメッセージが結果ページの上部に表示されます。  
  
### <a name="to-use-default-endpoints"></a>既定のエンドポイントを使用するには  
  
1. 既定のエンドポイントを使用するサービスでメタデータを構成するには、前の例のように、構成ファイルで <xref:System.ServiceModel.Description.ServiceMetadataBehavior> を指定します。ただし、エンドポイントは指定しないでください。 構成ファイルは、次のようになります。  
  
    ```xml  
    <configuration>  
      <system.serviceModel>  
        <behaviors>  
          <serviceBehaviors>  
            <behavior name="SimpleServiceBehavior">  
              <serviceMetadata httpGetEnabled="True" policyVersion="Policy12" />  
            </behavior>  
          </serviceBehaviors>  
        </behaviors>  
  
      </system.serviceModel>  
    </configuration>  
    ```  
  
     サービスの <xref:System.ServiceModel.Description.ServiceMetadataBehavior> では `httpGetEnabled` が `true` に設定されているため、サービスではメタデータの公開が有効になっています。また、エンドポイントが明示的に追加されていないため、ランタイムは既定のエンドポイントを追加します。 既定のエンドポイントについては、「[Simplified Configuration](../simplified-configuration.md)」 (簡易構成) と「[Simplified Configuration for WCF Services](../samples/simplified-configuration-for-wcf-services.md)」 (WCF サービスの簡易構成) を参照してください。  
  
## <a name="example"></a>例  
 次のコード例は、基本的な WCF サービスと、サービスのメタデータを公開する構成ファイルの実装を示しています。  
  
```csharp  
using System;  
using System.Runtime.Serialization;  
using System.ServiceModel;  
using System.ServiceModel.Description;  
  
namespace Metadata.Samples  
{  
    [ServiceContract]  
    public interface ISimpleService  
    {  
        [OperationContract]  
        string SimpleMethod(string msg);  
    }  
  
    class SimpleService : ISimpleService  
    {  
        public string SimpleMethod(string msg)  
        {  
            Console.WriteLine("The caller passed in " + msg);  
            return "Hello " + msg;  
        }  
    }  
  
    class Program  
    {  
        static void Main(string[] args)  
        {  
            ServiceHost host = new ServiceHost(typeof(SimpleService),  
                new Uri("http://localhost:8001/MetadataSample"));
            try  
            {  
                // Open the service host to accept incoming calls  
                host.Open();  
  
                // The service can now be accessed.  
                Console.WriteLine("The service is ready.");  
                Console.WriteLine("Press <ENTER> to terminate service.");  
                Console.WriteLine();  
                Console.ReadLine();  
  
                // Close the ServiceHostBase to shutdown the service.  
                host.Close();  
            }  
            catch (CommunicationException commProblem)  
            {  
                Console.WriteLine("There was a communication problem. " + commProblem.Message);  
                Console.Read();  
            }  
        }  
    }  
}  
```  
  
```xml  
<configuration>  
  <system.serviceModel>  
    <behaviors>  
      <serviceBehaviors>  
        <behavior name="SimpleServiceBehavior">  
          <serviceMetadata httpGetEnabled="True" policyVersion="Policy12" />  
          <serviceDebug includeExceptionDetailInFaults="False" />  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
  </system.serviceModel>  
</configuration>  
```  
  
## <a name="see-also"></a>関連項目

- <xref:System.ServiceModel.Description.ServiceMetadataBehavior>
- [方法: マネージド アプリケーションで WCF サービスをホストする](../how-to-host-a-wcf-service-in-a-managed-application.md)
- [自己ホスト](../samples/self-host.md)
- [メタデータ アーキテクチャの概要](metadata-architecture-overview.md)
- [メタデータを使用する](using-metadata.md)
- [方法: コードを使用してサービスのメタデータを公開する](how-to-publish-metadata-for-a-service-using-code.md)
