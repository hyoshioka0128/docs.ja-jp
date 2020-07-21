---
title: 構成チャネル ファクトリ
ms.date: 03/30/2017
ms.assetid: 3b749493-bd8a-4ccb-893e-5948901a1486
ms.openlocfilehash: 0f00ba5e217420fe416100071d380e413c3df118
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79183949"
---
# <a name="configuration-channel-factory"></a>構成チャネル ファクトリ
このサンプルでは、<xref:System.ServiceModel.Configuration.ConfigurationChannelFactory%601> の使用方法を示します。 WCF<xref:System.ServiceModel.Configuration.ConfigurationChannelFactory%601>クライアント構成の一元管理を可能にします。 これは、アプリケーション ドメインによる読み込みの後に構成が選択または変更される場合にも役立ちます。

## <a name="demonstrates"></a>対象
 <xref:System.ServiceModel.Configuration.ConfigurationChannelFactory%601>

## <a name="discussion"></a>ディスカッション
 このサンプルでは、既定のアプリケーション構成ファイルを使用することなく、<xref:System.ServiceModel.Configuration.ConfigurationChannelFactory%601> を使用して、クライアント アプリケーションに特定の構成ファイルを追加する方法を示します。

 このサンプルは、2 つのプロジェクトで構成されます。 最初のプロジェクトは、クライアントから送信されるメッセージに応答するために実行される単純なサービスです。 2 番目のプロジェクトは、Test.config 構成ファイルの <xref:System.ServiceModel.Configuration.ConfigurationChannelFactory%601> を使用して、2 つの <xref:System.Configuration.ExeConfigurationFileMap> オブジェクトを作成し、サービスとの通信にそれらのオブジェクトを使用するクライアント アプリケーションです。 どちらのクライアントも Test.config で指定された構成を使用してサービスと通信します。

 次のコードでは、カスタム構成ファイルをクライアント アプリケーションに追加します。

```csharp
ExeConfigurationFileMap fileMap = new ExeConfigurationFileMap();
fileMap.ExeConfigFilename = "Test.config";
Configuration newConfiguration = ConfigurationManager.OpenMappedExeConfiguration(fileMap, ConfigurationUserLevel.None);

ConfigurationChannelFactory<ICalculatorChannel> factory1 = new ConfigurationChannelFactory<ICalculatorChannel>("endpoint1", newConfiguration, new EndpointAddress("http://localhost:8000/servicemodelsamples/service"));
ICalculatorChannel client1 = factory1.CreateChannel();
```

#### <a name="to-set-up-build-and-run-the-sample"></a>サンプルをセットアップ、ビルド、および実行するには

1. 管理者特権で Visual Studio 2012 を開きます。

2. ConfigurationChannelFactory ソリューション (2 プロジェクト) を右クリックし、[**プロパティ]** を選択します。

3. [**共通のプロパティ]** で [**スタートアップ プロジェクト**] をクリックし、[**複数のスタートアップ プロジェクト**] をクリックします。

4. **サービス**プロジェクトを一覧の先頭に移動し **、"開始**" アクションを使用して **、サービス**プロジェクトの後に**クライアント**プロジェクトを**Action ‘Start’** 移動します。 **Client** **Service**

5. **[OK]** をクリックし、F5 キー (または Ctrl + F5 キー) を押してサンプルを実行します。

> [!IMPORTANT]
> サンプルは、既にコンピューターにインストールされている場合があります。 続行する前に、次の (既定の) ディレクトリを確認してください。  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> このディレクトリが存在しない場合は[、.NET Framework 4 の Windows コミュニケーション ファウンデーション (WCF) および Windows ワークフローファウンデーション (WF) サンプル](https://www.microsoft.com/download/details.aspx?id=21459)に移動して、すべての Windows 通信基盤 (WCF) とサンプルを[!INCLUDE[wf1](../../../../includes/wf1-md.md)]ダウンロードします。 このサンプルは、次のディレクトリに格納されます。  
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Services\ConfigurationChannelFactory`
