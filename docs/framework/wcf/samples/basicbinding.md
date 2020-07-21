---
title: BasicBinding
ms.date: 03/30/2017
ms.assetid: 86fbeb87-4d89-4b61-9577-867e0ac12945
ms.openlocfilehash: 84bfe78aa9e82b9600c48e0a32514f669fcc7d77
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84575655"
---
# <a name="basicbinding"></a>BasicBinding

このサンプルでは、第 1 世代と第 2 世代の Web サービスで HTTP 通信と最大限の相互運用性を実現する、`basicHttpBinding` の使用方法を示します。

> [!NOTE]
> このサンプルのセットアップ手順とビルド手順については、このトピックの最後を参照してください。

> [!IMPORTANT]
> サンプルは、既にコンピューターにインストールされている場合があります。 続行する前に、次の (既定の) ディレクトリを確認してください。
>
> `<InstallDrive>:\WF_WCF_Samples`
>
> このディレクトリが存在しない場合は、 [Windows Communication Foundation (wcf) および Windows Workflow Foundation (WF) のサンプルの .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459)にアクセスして、すべての WINDOWS COMMUNICATION FOUNDATION (wcf) とサンプルをダウンロードして [!INCLUDE[wf1](../../../../includes/wf1-md.md)] ください。 このサンプルは、次のディレクトリに格納されます。
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Binding\Basic\Http`

## <a name="sample-details"></a>サンプルの詳細

このサンプルは、電卓サービスを実装する[はじめに](getting-started-sample.md)に基づいています。

既定の動作で基本的なバインディングを使用する場合、必要なものはバインディング セクション名だけです。 基本的なバインディングを構成してその設定の一部を変更する場合は、バインド構成を定義する必要があります。 エンドポイントは、 `bindingConfiguration` `endpoint` 次のサンプルコードに示すように、<> 要素の属性を使用して、名前によってバインディング構成を参照する必要があります。

```xml
<services>
    <service
        type="Microsoft.ServiceModel.Samples.CalculatorService"
        behaviorConfiguration="CalculatorServiceBehavior">
       <endpoint address=""
             binding="basicHttpBinding"
             bindingConfiguration="Binding1"
             contract="Microsoft.ServiceModel.Samples.ICalculator" />
    </service>
</services>
```

このサンプルでは、バインド構成の名前は `"Binding1"` です。これは次のコード例のように定義されます。

```xml
<bindings>
   <basicHttpBinding>
      <binding name="Binding1"
               hostNameComparisonMode="StrongWildcard"
               receiveTimeout="00:10:00"
               sendTimeout="00:10:00"
               openTimeout="00:10:00"
               closeTimeout="00:10:00"
               maxMessageSize="65536"
               maxBufferSize="65536"
               maxBufferPoolSize="524288"
               transferMode="Buffered"
               messageEncoding="Text"
               textEncoding="utf-8"
               bypassProxyOnLocal="false"
               useDefaultWebProxy="true" >
         <security mode="None" />
      </binding>
   </basicHttpBinding>
</bindings>
```

バインディング要素には、ホスト名比較モード、最大メッセージ サイズ、プロキシ オプション、タイムアウト、メッセージ エンコーディングなど、さまざまなオプションを設定するための属性が用意されています。

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

3. ソリューションの C# 版または Visual Basic .NET 版をビルドするには、「 [Building the Windows Communication Foundation Samples](building-the-samples.md)」の手順に従います。

4. サンプルを単一コンピューター構成または複数コンピューター構成で実行するには、「 [Windows Communication Foundation サンプルの実行](running-the-samples.md)」の手順に従います。
