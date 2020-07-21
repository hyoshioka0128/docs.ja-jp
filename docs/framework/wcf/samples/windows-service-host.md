---
title: Windows サービス ホスト
ms.date: 03/30/2017
helpviewer_keywords:
- NT Service
- NT Service Host Sample [Windows Communication Foundation]
ms.assetid: 1b2f45c5-2bed-4979-b0ee-8f9efcfec028
ms.openlocfilehash: 9c041f6e9505d2ec5865dd512359b497a411cb40
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84602285"
---
# <a name="windows-service-host"></a>Windows サービス ホスト
このサンプルでは、マネージ Windows サービスでホストされている Windows Communication Foundation (WCF) サービスを示します。 Windows サービスは**コントロールパネル**の [サービス] アプレットを使用して制御され、システムの再起動後に自動的に起動するように構成できます。 このサンプルは、クライアント プログラムと Windows サービス プログラムで構成されています。 サービスは .exe プログラムとして実装され、独自のホスティング コードが指定されます。 Windows プロセス アクティブ化サービス (WAS) やインターネット インフォメーション サービス (IIS) などの他のホスト環境では、ホスティング コードを記述する必要はありません。

> [!NOTE]
> このサンプルのセットアップ手順とビルド手順については、このトピックの最後を参照してください。

> [!IMPORTANT]
> サンプルは、既にコンピューターにインストールされている場合があります。 続行する前に、次の (既定の) ディレクトリを確認してください。  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> このディレクトリが存在しない場合は、 [Windows Communication Foundation (wcf) および Windows Workflow Foundation (WF) のサンプルの .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459)にアクセスして、すべての WINDOWS COMMUNICATION FOUNDATION (wcf) とサンプルをダウンロードして [!INCLUDE[wf1](../../../../includes/wf1-md.md)] ください。 このサンプルは、次のディレクトリに格納されます。  
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Services\Hosting\WindowsService`  
  
 このサービスをビルドしたら、他の Windows サービスと同様、Installutil.exe ユーティリティを使用してインストールする必要があります。 サービスを変更する場合は、`installutil /u` を使用して、まずそのサービスをアンインストールする必要があります。 このサンプルに含まれている Setup.bat ファイルは Windows Service をインストールして起動するコマンド ファイルです。同様にこのサンプルに含まれている Cleanup.bat ファイルは、Windows サービスをシャットダウンしてアンインストールするコマンド ファイルです。 WCF サービスは、Windows サービスが実行されている場合にのみ、クライアントに応答できます。 **コントロールパネル**の [サービス] アプレットを使用して Windows サービスを停止し、クライアントを実行すると、 <xref:System.ServiceModel.EndpointNotFoundException> クライアントがサービスにアクセスしようとしたときに例外が発生します。 Windows サービスを再起動してクライアントを再実行した場合は、通信が正常に行われます。  
  
 サービスコードには、インストーラークラス、ICalculator コントラクトを実装する WCF サービス実装クラス、およびランタイムホストとして機能する Windows サービスクラスが含まれています。 インストーラー クラスは <xref:System.Configuration.Install.Installer> を継承します。このクラスを使用すると、Installutil.exe ツールにより、プログラムを NT サービスとしてインストールできます。 サービス実装クラスは、 `WcfCalculatorService` 基本的なサービスコントラクトを実装する WCF サービスです。 この WCF サービスは、という名前の Windows サービスクラス内でホストされ `WindowsCalculatorService` ます。 Windows サービスとして限定するため、このクラスは <xref:System.ServiceProcess.ServiceBase> を継承し、<xref:System.ServiceProcess.ServiceBase.OnStart%28System.String%5B%5D%29> メソッドと <xref:System.ServiceProcess.ServiceBase.OnStop> メソッドを実装しています。 <xref:System.ServiceProcess.ServiceBase.OnStart%28System.String%5B%5D%29> では、<xref:System.ServiceModel.ServiceHost> 型の `WcfCalculatorService` オブジェクトが作成され、開かれます。 <xref:System.ServiceProcess.ServiceBase.OnStop> では、<xref:System.ServiceModel.Channels.CommunicationObject.Close%28System.TimeSpan%29> オブジェクトの <xref:System.ServiceModel.ServiceHost> メソッドが呼び出されて ServiceHost が閉じられます。 ホストのベースアドレスは、要素の子である要素を使用して構成され [\<add>](../../configure-apps/file-schema/wcf/add-of-baseaddresses.md) [\<baseAddresses>](../../configure-apps/file-schema/wcf/baseaddresses.md) [\<host>](../../configure-apps/file-schema/wcf/host.md) ます。これは、要素の子である要素の子です [\<service>](../../configure-apps/file-schema/wcf/service.md) 。  
  
 定義されているエンドポイントは、ベースアドレスとを使用し [\<wsHttpBinding>](../../configure-apps/file-schema/wcf/wshttpbinding.md) ます。 ベース アドレスの構成と CalculatorService を公開するエンドポイントのサンプルを次に示します。  
  
```xml  
<services>  
  <service name="Microsoft.ServiceModel.Samples.WcfCalculatorService"  
           behaviorConfiguration="CalculatorServiceBehavior">  
    <host>  
      <baseAddresses>  
        <add baseAddress="http://localhost:8000/ServiceModelSamples/service"/>  
      </baseAddresses>  
    </host>  
    <!-- This endpoint is exposed at the base address provided by host: http://localhost:8000/ServiceModelSamples/service.  -->  
    <endpoint address=""  
              binding="wsHttpBinding"  
              contract="Microsoft.ServiceModel.Samples.ICalculator" />  
    ...  
  </service>  
</services>  
```  
  
 このサンプルを実行すると、操作要求と応答がサービスとクライアントの両方のコンソール ウィンドウに表示されます。 どちらかのコンソールで Enter キーを押すと、サービスとクライアントがどちらもシャットダウンされます。  
  
### <a name="to-set-up-build-and-run-the-sample"></a>サンプルをセットアップ、ビルド、および実行するには  
  
1. [Windows Communication Foundation サンプルの1回限りのセットアップ手順](one-time-setup-procedure-for-the-wcf-samples.md)を実行したことを確認します。  
  
2. ソリューションの C# 版または Visual Basic .NET 版をビルドするには、「 [Building the Windows Communication Foundation Samples](building-the-samples.md)」の手順に従います。  
  
3. ソリューションがビルドされたら、管理者特権で Visual Studio 2012 コマンドプロンプトから Setup.exe を実行し、Installutil.exe ツールを使用して Windows サービスをインストールします。 このサービスは、[サービス] に表示されます。  
  
4. サンプルを単一コンピューター構成または複数コンピューター構成で実行するには、「 [Windows Communication Foundation サンプルの実行](running-the-samples.md)」の手順に従います。  
  
## <a name="see-also"></a>関連項目

- [AppFabric のホストおよび永続化のサンプル](https://docs.microsoft.com/previous-versions/appfabric/ff383418(v=azure.10))
