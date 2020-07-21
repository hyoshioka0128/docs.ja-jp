---
title: 'チュートリアル: Windows Communication Foundation クライアントを作成する'
description: Wcf アプリケーションの作成を開始する際に役立つ一連の記事の一部として、WCF サービスからメタデータを取得することによって、クライアントを作成する方法について説明します。
ms.date: 03/19/2019
helpviewer_keywords:
- clients [WCF], running
- WCF clients [WCF], running
ms.assetid: a67884cc-1c4b-416b-8c96-5c954099f19f
ms.openlocfilehash: d5a2a2b5175c9e34eaf1dbaff20ac57f34117c4e
ms.sourcegitcommit: 358a28048f36a8dca39a9fe6e6ac1f1913acadd5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85246325"
---
# <a name="tutorial-create-a-windows-communication-foundation-client"></a>チュートリアル: Windows Communication Foundation クライアントを作成する

このチュートリアルでは、基本的な Windows Communication Foundation (WCF) アプリケーションを作成するために必要な5つのタスクのうち、4番目のタスクについて説明します。 チュートリアルの概要については、「[チュートリアル: Windows Communication Foundation アプリケーションの](getting-started-tutorial.md)概要」を参照してください。

WCF アプリケーションを作成するための次のタスクでは、WCF サービスからメタデータを取得してクライアントを作成します。 サービスの MEX エンドポイントからメタデータを取得するサービス参照を追加するには、Visual Studio を使用します。 その後、Visual Studio によって、選択した言語でクライアントプロキシのマネージソースコードファイルが生成されます。 また、クライアント構成ファイル (*App.config*) も作成します。 このファイルにより、クライアントアプリケーションはエンドポイントでサービスに接続できるようになります。

> [!NOTE]
> Visual Studio のクラスライブラリプロジェクトから WCF サービスを呼び出す場合は、**サービス参照の追加**機能を使用して、プロキシおよび関連する構成ファイルを自動的に生成します。 ただし、クラスライブラリプロジェクトではこの構成ファイルを使用しないため、クラスライブラリを呼び出す実行可能ファイルの*App.config*ファイルに、生成された構成ファイルの設定を追加する必要があります。

> [!NOTE]
> 別の方法として、Visual Studio ではなく[ServiceModel メタデータユーティリティツール](#servicemodel-metadata-utility-tool)を使用して、プロキシクラスと構成ファイルを生成することもできます。

クライアント アプリケーションは、生成されたプロキシ クラスを使用してサービスと通信します。 この手順については[、「チュートリアル: クライアントを使用](how-to-use-a-wcf-client.md)する」を参照してください。

このチュートリアルでは、次の作業を行う方法について説明します。
> [!div class="checklist"]
>
> - WCF クライアントのコンソールアプリプロジェクトを作成して構成します。
> - WCF サービスへのサービス参照を追加して、プロキシクラスと構成ファイルを生成します。

## <a name="create-a-windows-communication-foundation-client"></a>Windows Communication Foundation クライアントを作成する

1. Visual Studio でコンソールアプリプロジェクトを作成します。

    1. [**ファイル**] メニューの [プロジェクト/ソリューションを**開く**] を選択し、前の作業で作成し  >  **Project/Solution**た**gettingstarted** (*gettingstarted. .sln*) を参照します。 **[Open (開く)]** を選択します。

    2. [**表示**] メニューの [**ソリューションエクスプローラー**] をクリックします。

    3. [**ソリューションエクスプローラー** ] ウィンドウで、[ **gettingstarted** ] ソリューション (最上位ノード) を選択**Add**し、  >  ショートカットメニューの [**新しいプロジェクト**の追加] をクリックします。

    4. [**新しいプロジェクトの追加**] ウィンドウの左側にある [ **Visual C#** ] または [ **Visual Basic**] の下にある [ **Windows デスクトップ**] カテゴリを選択します。

    5. [**コンソールアプリ (.NET Framework)** ] テンプレートを選択し、**名前**として「 *gettingclient* 」と入力します。 **[OK]** を選択します。

2. **Gettingのクライアント**プロジェクトで、アセンブリに参照を追加し <xref:System.ServiceModel> ます。

    1. [**ソリューションエクスプローラー** ] ウィンドウで、 **gettingclient**プロジェクトの [**参照**] フォルダーを選択し、ショートカットメニューの [**参照の追加**] をクリックします。

    2. [**参照の追加**] ウィンドウの左側にある [**アセンブリ**] で、[**フレームワーク**] を選択します。

    3. [ **System.servicemodel**] を見つけて選択し、[ **OK]** を選択します。

    4. [**ファイル**] [  >  **すべて保存**] の順に選択して、ソリューションを保存します。

3. 電卓サービスへのサービス参照を追加します。

   1. [**ソリューションエクスプローラー** ] ウィンドウで、 **gettingclient**プロジェクトの [**参照**] フォルダーを選択し、ショートカットメニューの [**サービス参照の追加**] を選択します。

   2. [**サービス参照の追加**] ウィンドウで、[**探索**] を選択します。

      電卓サービスが開始され、Visual Studio に [**サービス**] ボックスに表示されます。

   3. [**計算] を選択して**展開し、サービスによって実装されているサービスコントラクトを表示します。 既定の**名前空間**をそのまま使用し、[ **OK]** を選択します。

      Visual Studio によって、 **Gettingclient**プロジェクトの**接続済みサービス**フォルダーの下に新しい項目が追加されます。

### <a name="servicemodel-metadata-utility-tool"></a>ServiceModel メタデータユーティリティツール

次の例は、必要に応じて[ServiceModel Metadata Utility tool (Svcutil.exe)](servicemodel-metadata-utility-tool-svcutil-exe.md)を使用してプロキシクラスファイルを生成する方法を示しています。 このツールでは、プロキシクラスファイルと*App.config*ファイルが生成されます。 次の例では、C# でプロキシを生成する方法と Visual Basic について説明します。

```shell
svcutil.exe /language:cs /out:generatedProxy.cs /config:app.config http://localhost:8000/GettingStarted/CalculatorService
```

```shell
svcutil.exe /language:vb /out:generatedProxy.vb /config:app.config http://localhost:8000/GettingStarted/CalculatorService
```

### <a name="client-configuration-file"></a>クライアント構成ファイル

クライアントを作成すると、Visual Studio によって**Gettingのクライアント**プロジェクトに**App.config**構成ファイルが作成されます。これは、次の例のようになります。

```xml
    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
        <startup>
            <!-- specifies the version of WCF to use-->
            <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.6.1" />
        </startup>
        <system.serviceModel>
            <bindings>
                <!-- Uses wsHttpBinding-->
                <wsHttpBinding>
                    <binding name="WSHttpBinding_ICalculator" />
                </wsHttpBinding>
            </bindings>
            <client>
                <!-- specifies the endpoint to use when calling the service -->
                <endpoint address="http://localhost:8000/GettingStarted/CalculatorService"
                    binding="wsHttpBinding" bindingConfiguration="WSHttpBinding_ICalculator"
                    contract="ServiceReference1.ICalculator" name="WSHttpBinding_ICalculator">
                    <identity>
                        <dns value="localhost" />
                    </identity>
                </endpoint>
            </client>
        </system.serviceModel>
    </configuration>
```

セクションの下で、 [\<system.serviceModel>](../configure-apps/file-schema/wcf/system-servicemodel.md) 要素を確認し [\<endpoint>](../configure-apps/file-schema/wcf/endpoint-element.md) ます。 ** &lt; Endpoint &gt; **要素は、次のように、クライアントがサービスにアクセスするために使用するエンドポイントを定義します。

- アドレス: `http://localhost:8000/GettingStarted/CalculatorService` 。 エンドポイントのアドレス。
- サービスコントラクト: `ServiceReference1.ICalculator` 。 サービスコントラクトは、WCF クライアントとサービス間の通信を処理します。 **サービス参照の追加**関数を使用したときに、Visual Studio によってこのコントラクトが生成されました。 これは基本的に、Gettingの Lib プロジェクトで定義したコントラクトのコピーです。
- バインド: <xref:System.ServiceModel.WSHttpBinding> 。 バインドでは、HTTP をトランスポート、相互運用可能なセキュリティ、およびその他の構成の詳細として指定します。

## <a name="next-steps"></a>次の手順

このチュートリアルでは、以下の内容を学習しました。
> [!div class="checklist"]
>
> - WCF クライアントのコンソールアプリプロジェクトを作成して構成します。
> - WCF サービスへのサービス参照を追加して、プロキシクラスとクライアントアプリケーションの構成ファイルを生成します。

次のチュートリアルに進み、生成されたクライアントの使用方法を学習してください。

> [!div class="nextstepaction"]
> [チュートリアル: WCF クライアントの使用](how-to-use-a-wcf-client.md)
