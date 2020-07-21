---
title: HTTPS を介したカスタム バインドの信頼できるセッション
ms.date: 03/30/2017
ms.assetid: 16aaa80d-3ffe-47c4-8b16-ec65c4d25f8d
ms.openlocfilehash: ab2dd4725879ba969afdae8a6423a920a9786125
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84585299"
---
# <a name="custom-binding-reliable-session-over-https"></a>HTTPS を介したカスタム バインドの信頼できるセッション
このサンプルでは、信頼できるセッションを使用した SSL トランスポート セキュリティを示します。 信頼できるセッションは、WS-ReliableMessaging プロトコルを実装しています。 信頼できるセッションを介して WS-Security を構築することにより、セキュリティで保護された信頼できるセッションを持つことができます。 ただし、SSL による HTTP トランスポート セキュリティの使用を選択できる場合もあります。  
  
> [!IMPORTANT]
> サンプルは、既にコンピューターにインストールされている場合があります。 続行する前に、次の (既定の) ディレクトリを確認してください。  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> このディレクトリが存在しない場合は、 [Windows Communication Foundation (wcf) および Windows Workflow Foundation (WF) のサンプルの .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459)にアクセスして、すべての WINDOWS COMMUNICATION FOUNDATION (wcf) とサンプルをダウンロードして [!INCLUDE[wf1](../../../../includes/wf1-md.md)] ください。 このサンプルは、次のディレクトリに格納されます。  
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Binding\Custom\ReliableSessionOverHttps`  
  
## <a name="sample-details"></a>サンプルの詳細  
 SSL では、パケット自体のセキュリティが保護されます。 WS-SecureConversation を使用して、信頼できるセッションのセキュリティを保護する場合とは異なることに注意してください。  
  
 HTTPS を介して信頼できるセッションを使用するには、カスタム バインドを作成する必要があります。 このサンプルは、電卓サービスを実装する[はじめに](getting-started-sample.md)に基づいています。 カスタムバインディングは、信頼できるセッションのバインディング要素とを使用して作成され [\<httpsTransport>](../../configure-apps/file-schema/wcf/httpstransport.md) ます。 カスタム バインドの構成を次に示します。  
  
```xml  
<?xml version="1.0" encoding="utf-8" ?>  
<configuration>  
  <system.serviceModel>  
    <services>  
      <service
          name="Microsoft.ServiceModel.Samples.CalculatorService"  
          behaviorConfiguration="CalculatorServiceBehavior">  
        <!-- use base address provided by host -->  
        <endpoint address=""  
                  binding="customBinding"  
                  bindingConfiguration="reliableSessionOverHttps"
                  contract="Microsoft.ServiceModel.Samples.ICalculator" />  
        <!-- the mex endpoint is exposed as http://localhost/servicemodelsamples/service.svc/mex-->  
        <endpoint address="mex"  
                  binding="mexHttpBinding"  
                  contract="IMetadataExchange"/>  
      </service>  
    </services>  
  
    <bindings>  
      <customBinding>  
        <binding name="reliableSessionOverHttps">  
          <reliableSession />  
          <httpsTransport />  
        </binding>  
      </customBinding>  
    </bindings>  
  
    <!--For debugging purposes set the includeExceptionDetailInFaults attribute to true-->  
    <behaviors>  
      <serviceBehaviors>  
        <behavior name="CalculatorServiceBehavior">  
          <serviceMetadata httpGetEnabled="true" />  
          <serviceDebug includeExceptionDetailInFaults="False" />  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
  
  </system.serviceModel>  
  
</configuration>  
```  
  
 サンプル内のプログラムコードは、[はじめに](getting-started-sample.md)サービスのプログラムコードと同じです。 このサンプルをビルドして実行する前に、証明書を作成し、Web サーバー証明書ウィザードを使用してあらかじめ割り当てておく必要があります。 次に示すクライアント用構成の例のように、構成ファイル設定でエンドポイントとバインディングを定義すると、カスタム バインドの使用が有効になります。  
  
```xml  
<?xml version="1.0" encoding="utf-8" ?>  
<configuration>  
  <system.serviceModel>  
  
    <client>  
      <!-- this endpoint has an https: address -->  
      <endpoint name=""  
                address="https://localhost/servicemodelsamples/service.svc"
                binding="customBinding"
                bindingConfiguration="reliableSessionOverHttps"
                contract="Microsoft.ServiceModel.Samples.ICalculator" />  
    </client>  
  
      <bindings>  
        <customBinding>  
          <binding name="reliableSessionOverHttps">  
            <reliableSession />  
            <httpsTransport />  
          </binding>  
        </customBinding>
    </bindings>  
  
  </system.serviceModel>  
  
</configuration>  
```  
  
 指定されたアドレスはスキームを使用し `https://` ます。  
  
 このサンプルで使用される証明書は、Makecert で作成されたテスト証明書であるため、ブラウザーからなどの https: アドレスにアクセスしようとすると、セキュリティの警告が表示されます `https://localhost/servicemodelsamples/service.svc` 。 Windows Communication Foundation (WCF) クライアントが適切なテスト証明書を使用できるようにするために、セキュリティの警告を抑制するために、いくつかの追加のコードがクライアントに追加されました。 そのためのコードとそれに必要なクラスは、本運用の証明書を使用するときには不要です。  

```csharp
// This code is required only for test certificates like those created by Makecert.exe.  
PermissiveCertificatePolicy.Enact("CN=ServiceModelSamples-HTTPS-Server");  
```

 このサンプルを実行すると、操作要求および応答がクライアントのコンソール ウィンドウに表示されます。 クライアントをシャットダウンするには、クライアント ウィンドウで Enter キーを押します。  
  
```console  
Add(100,15.99) = 115.99  
Subtract(145,76.54) = 68.46  
Multiply(9,81.25) = 731.25  
Divide(22,7) = 3.14285714285714  
  
Press <ENTER> to terminate client.  
```  
  
#### <a name="to-set-up-build-and-run-the-sample"></a>サンプルをセットアップ、ビルド、および実行するには  
  
1. 次のコマンドを使用して、ASP.NET 4.0 をインストールします。  
  
    ```console  
    %windir%\Microsoft.NET\Framework\v4.0.XXXXX\aspnet_regiis.exe /i /enable  
    ```  
  
2. [Windows Communication Foundation サンプルの1回限りのセットアップ手順](one-time-setup-procedure-for-the-wcf-samples.md)を実行したことを確認します。  
  
3. [インターネットインフォメーションサービス (IIS) サーバー証明書のインストール手順](iis-server-certificate-installation-instructions.md)を実行していることを確認します。  
  
4. ソリューションの C# 版または Visual Basic .NET 版をビルドするには、「 [Building the Windows Communication Foundation Samples](building-the-samples.md)」の手順に従います。  
  
5. サンプルを単一コンピューター構成または複数コンピューター構成で実行するには、「 [Windows Communication Foundation サンプルの実行](running-the-samples.md)」の手順に従います。  
