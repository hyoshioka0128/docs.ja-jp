---
title: SystemWebRouting 統合サンプル
ms.date: 03/30/2017
ms.assetid: f1c94802-95c4-49e4-b1e2-ee9dd126ff93
ms.openlocfilehash: 2f12d80085e3ac27dac8ce80b6bb09f69337bfd8
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79143955"
---
# <a name="systemwebrouting-integration-sample"></a>SystemWebRouting 統合サンプル
このサンプルでは、<xref:System.Web.Routing> 名前空間のクラスとのホスト層の統合を示します。 <xref:System.Web.Routing> 名前空間のクラスを使用すると、物理リソースに直接対応しない URL をアプリケーションで使用できます。 Web ルーティングを使用すると、開発者は HTTP の仮想アドレスを作成し、実際の WCF サービスにマップし直すことができます。 これは、物理ファイルやリソースを配置せずに WCF サービスをホストする必要がある場合、または .html や .aspx などのファイルがない URL を使用してサービスにアクセスする必要がある場合に役立ちます。 このサンプルでは、<xref:System.Web.Routing.RouteTable> クラスを使用して、global.asax で定義された実行中のサービスにマップされる仮想 URI を作成する方法を示します。

> [!NOTE]
> <xref:System.Web.Routing> 名前空間のクラスは、HTTP でホストされるサービスに対してのみ機能します。  
  
この例では、WCF を使用して、フィードとフィード`movies`の 2`channels`つの RSS フィードを作成します。 サービスをアクティブ化する URL には、拡張が含まれておらず、`Application_Start`クラスから派生`Global`したクラスのメソッド<xref:System.Web.HttpApplication>に登録されます。  
  
> [!NOTE]
> このサンプルは、IIS 6.0 が拡張なしの URL をサポートするために別の方法を使用するため、インターネット インフォメーション サービス (IIS) 7.0 以降でのみ動作します。  

#### <a name="to-download-this-sample"></a>このサンプルをダウンロードするには
  
このサンプルは、既にコンピュータにインストールされている可能性があります。 続行する前に、次の (既定の) ディレクトリを確認してください。  

`<InstallDrive>:\WF_WCF_Samples`  

 このディレクトリが存在しない場合は[、.NET Framework 4 の Windows コミュニケーション ファウンデーション (WCF) および Windows ワークフローファウンデーション (WF) サンプル](https://www.microsoft.com/download/details.aspx?id=21459)に移動して、すべての Windows 通信基盤 (WCF) とサンプルを[!INCLUDE[wf1](../../../../includes/wf1-md.md)]ダウンロードします。 このサンプルは、次のディレクトリに格納されます。  

`<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Services\Hosting\WebRoutingIntegration`  
  
#### <a name="to-use-this-sample"></a>このサンプルを使用するには  
  
1. を使用して、Web ルーティング統合.sln ファイルを開きます。  
  
2. ソリューションを実行して Web 開発サーバーを起動するには、F5 キーを押します。  
  
     サンプルのディレクトリの一覧が表示されます。 ファイル拡張子が .svc のファイルがないことに注意してください。  
  
3. アドレス バーで URL`movies`に追加し、URL を`http://localhost:[port]/movies`読み取って Enter キーを押します。  
  
     movies フィードがブラウザーに表示されます。  
  
4. アドレス バーで URL`channels`に追加し、読み取`http://localhost:[port]/channels`りと Enter キーを押します。  
  
     channels フィードがブラウザーに表示されます。  
  
5. Alt キーを押しながら F4 キーを押して Web ブラウザーを閉じます。  
  
     開発サーバーが終了していない場合は、通知領域アイコンを右クリックし、[**停止**] を選択します。  
  
#### <a name="to-use-this-sample-when-hosted-in-iis"></a>このサンプルを使用するには (IIS でホストする場合)  
  
1. を使用して、Web ルーティング統合.sln ファイルを開きます。  
  
2. Ctrl キーと Shift キーを押しながら B キーを押して、プロジェクトをビルドします。  
  
3. インターネット インフォメーション サービス (IIS) マネージャーで Web アプリケーションを作成します。  
  
    1. IIS マネージャで、[既定の**Web サイト**] を右クリックし、[**アプリケーションの追加**] をクリックします。  
  
    2. **エイリアス**に、 を入力`WebRoutingIntegration`します。  
  
    3. [**物理パス**] で、プロジェクト内の [サービス] フォルダを選択します。  
  
    4. [**OK**] を押します。  
  
4. Web アプリケーションを右クリックし、[アプリケーションの**管理**] を選択して **[参照]** を選択し、アプリケーションを起動します。  
  
5. アドレス バーで URL`movies`に追加し、読み取`http://localhost:[port]/movies`りと Enter キーを押します。  
  
     movies フィードがブラウザーに表示されます。  
  
6. アドレス バーで URL`channels`に追加し、読み取`http://localhost:[port]/channels`りと Enter キーを押します。  
  
     channels フィードがブラウザーに表示されます。  
  
7. Alt キーを押しながら F4 キーを押して Web ブラウザーを閉じます。  
  
 このサンプルは、HTTP でホストされたサービスの要求をルーティングするために、<xref:System.Web.Routing> 名前空間のクラスを使用してホスト層を構成できることを示しています。  
  
> [!NOTE]
> バージョン 2 に設定されている場合は、既定のアプリケーション プール バージョンを .NET Framework 4 に更新する必要があります。  
  
## <a name="see-also"></a>関連項目

- [AppFabric のホストおよび永続化のサンプル](https://docs.microsoft.com/previous-versions/appfabric/ff383418(v=azure.10))
