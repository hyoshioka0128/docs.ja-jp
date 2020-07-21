---
title: WCF Data Services の開発と配置
ms.date: 03/30/2017
helpviewer_keywords:
- WCF Data Services, developing
- WCF Data Services, deploying
- deploying [WCF Data Services
- developing applications [WCF Data Services]
ms.assetid: 6557c0e3-5aea-4f6e-bc14-77ad317a168b
ms.openlocfilehash: 7519dce8ed17bc623173f30222296ffaa42b4341
ms.sourcegitcommit: 3492dafceb5d4183b6b0d2f3bdf4a1abc4d5ed8c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2020
ms.locfileid: "86416074"
---
# <a name="develop-and-deploy-wcf-data-services"></a>WCF Data Services の開発と配置

この記事では、WCF Data Services の開発と配置について説明します。 WCF Data Services の基本的な情報については、[作業の開始](getting-started-with-wcf-data-services.md)と[概要](wcf-data-services-overview.md)に関する記事を参照してください。

## <a name="develop-wcf-data-services"></a>WCF Data Services の開発

WCF Data Services を使用して、Open Data Protocol (OData) をサポートするデータ サービスを作成する場合、開発時に次の基本的なタスクを実行する必要があります。

1. **データ モデルを定義する**

     WCF Data Services は、リレーショナル データベースから遅延バインディング データ型に至るさまざまなデータ ソースのデータに基づいてデータ モデルを定義できるようにする各種のデータ サービス プロバイダーをサポートしています。 詳細については、「[Data Services プロバイダー](data-services-providers-wcf-data-services.md)」を参照してください。

2. **データ サービスを作成する**

     最も基本的なデータ サービスでは、 <xref:System.Data.Services.DataService%601> クラスを継承するクラスを `T` 型 (エンティティ コンテナーの名前空間修飾名) と一緒に公開します。 詳細については、「 [Defining WCF Data Services](defining-wcf-data-services.md)の開発と配置について説明します。

3. **データ サービスを構成する**

     既定では、WCF Data Services では、エンティティ コンテナーによって公開されているリソースへのアクセスは無効になります。 <xref:System.Data.Services.DataServiceConfiguration> インターフェイスを使用すると、リソースとサービス操作へのアクセスの構成、サポートされる OData のバージョンの指定、およびサービス全体のその他の動作 (バッチ動作や 1 つの応答フィードで返すことができるエンティティの最大数など) を定義できます。 詳細については、「[データ サービスの構成](configuring-the-data-service-wcf-data-services.md)」を参照してください。

この記事では、主に、Visual Studio を使用したデータ サービスの開発と配置について説明します。 データを OData フィードとして公開できるようにする WCF Data Services の柔軟性については、「[WCF Data Services の定義](defining-wcf-data-services.md)」を参照してください。

### <a name="choose-a-development-web-server"></a>開発 Web サーバーの選択

Visual Studio 2015 を使用して WCF Data Services を ASP.NET アプリケーションまたは ASP.NET Web サイトとして開発する場合、開発時にデータ サービスを実行する Web サーバーを選択できます。 次の Web サーバーを Visual Studio と統合することにより、ローカル コンピューターでデータ サービスを簡単にテストおよびデバッグできるようになります。

1. **ローカル IIS サーバー**

     インターネット インフォメーション サービス (IIS) 上で実行される ASP.NET アプリケーションまたは ASP.NET Web サイトとしてデータ サービスを作成する場合は、ローカル コンピューター上で IIS を使用してデータ サービスを開発およびテストすることをお勧めします。 IIS でデータ サービスを実行すると、デバッグ時における HTTP 要求のトレースが容易になります。 これにより、データ サービスに必要なファイルやデータベースなどのリソースにアクセスするために IIS で必要とされる権限を事前に確認することもできます。 IIS 上でデータ サービスを実行するには、IIS と Windows Communication Foundation (WCF) がインストールされて正しく構成されており、ファイル システムおよびデータベースで IIS アカウントにアクセス権が正しく付与されていることを確認します。 詳細については、[IIS 上で実行する WCF Data Service を開発する](how-to-develop-a-wcf-data-service-running-on-iis.md)」を参照してください。

    > [!NOTE]
    > 開発環境でローカル IIS サーバーを構成できるようにするには、Visual Studio を管理者権限で実行する必要があります。

2. **Visual Studio 開発サーバー**

     Visual Studio には、組み込みの Web サーバーとして、ASP.NET プロジェクトの既定の Web サーバーである Visual Studio 開発サーバーが用意されています。 この Web サーバーは、開発時にローカル コンピューター上で ASP.NET プロジェクトを実行するように設計されています。 [WCF Data Services のクイックスタート](quickstart-wcf-data-services.md)では、Visual Studio 開発サーバーで実行されるデータ サービスを作成する方法を示しています。

     Visual Studio 開発サーバーを使用してデータ サービスを開発する場合は、次の制限事項に注意してください。

    - このサーバーにはローカル コンピューター上でしかアクセスできません。

    - このサーバーは、HTTP メッセージの既定のポートであるポート 80 ではなく、 `localhost` および特定のポートでリッスンします。 詳細については、「 [ASP.NET Web プロジェクト用の Visual Studio の Web サーバー](https://docs.microsoft.com/previous-versions/aspnet/58wxa9w5(v=vs.120))」を参照してください。

    - このサーバーでは、現在のユーザー アカウントのコンテキストでデータ サービスが実行されます。 たとえば、管理者レベルのユーザーとして実行する場合、Visual Studio 開発サーバーで実行されるデータ サービスには、管理者レベルの特権があります。 そのため、データ サービスは、IIS サーバーに配置されたときにはアクセスする権限を持たないリソースにも、アクセスできることになります。

    - このサーバーには、認証など、IIS の必要以上の機能は含まれていません。

    - このサーバーでは、データ サービスから大きなバイナリ データにアクセスするときに WCF Data Services クライアントによって既定で送信されるチャンク HTTP ストリームを処理できません。 詳細については、「[ストリーミング プロバイダー](streaming-provider-wcf-data-services.md)」を参照してください。

    - このサーバーでは、WCF Data Services によってキー値内のピリオド (`.`) 文字がサポートされている場合でも、URL 内のピリオド文字を適切に処理できません。

    > [!TIP]
    > 開発時に Visual Studio 開発サーバーを使用してデータ サービスをテストできる場合でも、IIS を実行する Web サーバーに配置した後でデータ サービスを再度テストする必要があります。

3. **Azure 開発環境**

     Azure Tools for Visual Studio には、Visual Studio 内で Azure サービスを開発するためのツールの統合セットが含まれています。 これらのツールでは、Azure に配置できるデータ サービスを開発し、配置前にローカル コンピューター上でデータ サービスをテストすることができます。 Visual Studio を使用して Azure プラットフォーム上で実行されるデータ サービスを開発する場合は、これらのツールを使用してください。 ツールのインストールの詳細については、「[Azure tools for Visual Studio 2015](../../../azure/vs2015-install.md)」を参照してください。 Azure 上で実行されるデータ サービスの開発の詳細については、「[Azure での OData サービスの配置](https://docs.microsoft.com/archive/blogs/astoriateam/deploying-an-odata-service-in-windows-azure)」の記事を参照してください。

### <a name="development-tips"></a>開発のヒント

データ サービスを開発する際は、次の点を考慮してください。

- ユーザーを認証する場合や、特定のユーザーのアクセスを制限する場合は、データ サービスのセキュリティ要件を決定します。 詳細については、「 [Securing WCF Data Services](securing-wcf-data-services.md)」を参照してください。

- データ サービスをデバッグするときは、HTTP 検査プログラムを使用すると、要求メッセージおよび応答メッセージの内容を検査できるので便利です。 生のパケットを表示できるネットワーク パケット アナライザーを使用すると、データ サービスの HTTP 要求および HTTP 応答を検査できます。

- データ サービスのデバッグ時は、通常の操作時以上に、データ サービスの詳細なエラー情報が必要になることがあります。 データ サービスから詳細なエラー情報を取得するには、 <xref:System.Data.Services.DataServiceConfiguration.UseVerboseErrors%2A> の <xref:System.Data.Services.DataServiceConfiguration> プロパティを `true` に設定し、データ サービス クラスの <xref:System.ServiceModel.Description.ServiceDebugBehavior.IncludeExceptionDetailInFaults%2A> 属性の <xref:System.ServiceModel.Description.ServiceDebugBehavior> プロパティを `true`に設定します。 詳細については、「[WCF Data Services のデバッグ](https://docs.microsoft.com/archive/blogs/phaniraj/debugging-wcf-data-services)」の記事を参照してください。 また、WCF でトレースを有効にして、HTTP メッセージング レイヤーで発生した例外を表示することもできます。 詳細については、「 [Configuring Tracing](../../wcf/diagnostics/tracing/configuring-tracing.md)」を参照してください。

- データ サービスは、通常、ASP.NET アプリケーション プロジェクトとして開発されますが、Visual Studio の ASP.NET Web サイト プロジェクトとしてデータ サービスを作成することもできます。 この 2 種類のプロジェクトの違いについては、「[Visual Studio での Web アプリケーション プロジェクトと Web サイト プロジェクト](https://docs.microsoft.com/previous-versions/aspnet/dd547590(v=vs.110))」を参照してください。

- Visual Studioの **[新しい項目の追加]** ダイアログ ボックスを使用してデータ サービスを作成すると、そのデータ サービスは IIS 内の ASP.NET によってホストされます。 ASP.NET と IIS がデータ サービスの既定のホストですが、その他のホスティング オプションもサポートされています。 詳細については、「[データ サービスのホスティング](hosting-the-data-service-wcf-data-services.md)」を参照してください。

## <a name="deploy-wcf-data-services"></a>WCF Data Services の配置

WCF Data Services では、データ サービスをホストするプロセスを柔軟に選択できます。 Visual Studio を使用して、次のプラットフォームにデータ サービスを配置できます。

- **IIS でホストされる Web サーバー**

    データ サービスを ASP.NET プロジェクトとして開発すると、ASP.NET の標準配置プロセスを使用して IIS Web サーバーに配置することができます。 Visual Studio では、ASP.NET 向けに、配置するデータ サービスをホストする ASP.NET プロジェクトの種類に応じて次の配置テクノロジが提供されます。

  - **ASP.NET Web アプリケーション用の配置テクノロジ**

    - [方法: Visual Studio で Web 配置パッケージを作成する](https://docs.microsoft.com/previous-versions/aspnet/dd465323(v=vs.110))

    - [方法: Visual Studio でワンクリック発行を使用して Web プロジェクトを配置する](https://docs.microsoft.com/previous-versions/aspnet/dd465337(v=vs.110))

  - **ASP.NET Web サイト用の配置テクノロジ**

    - [方法: Web サイトのコピー ツールを使用して Web サイト ファイルをコピーする](https://docs.microsoft.com/previous-versions/aspnet/c95809c0(v=vs.100))

    - [方法: Web サイトを公開する](https://docs.microsoft.com/previous-versions/aspnet/20yh9f1b(v=vs.100))

    - [チュートリアル: XCOPY を使用して ASP.NET Web アプリケーションを配置する](https://docs.microsoft.com/previous-versions/aspnet/f735abw9(v=vs.100))

     ASP.NET アプリケーションの配置オプションの詳細については、「[Visual Studio および ASP.NET の Web の配置の概要](https://docs.microsoft.com/previous-versions/aspnet/dd394698(v=vs.110))」を参照してください。

    > [!TIP]
    > データ サービスを IIS に配置する前に、IIS を実行している Web サーバーへの配置をテストしておく必要があります。 詳細については、[IIS 上で実行する WCF Data Service を開発する](how-to-develop-a-wcf-data-service-running-on-iis.md)」を参照してください。

- **Azure**

     [Azure Tools for Visual Studio](../../../azure/vs2015-install.md) を使用して、データ サービスを Azure に配置できます。 Azure へのデータ サービスの配置の詳細については、「[Azure での OData サービスの配置](https://docs.microsoft.com/archive/blogs/astoriateam/deploying-an-odata-service-in-windows-azure)」を参照してください。

### <a name="deployment-considerations"></a>配置に関する注意事項

データ サービスを配置する際は、次の点を考慮してください。

- Entity Framework プロバイダーを使用して SQL Server データベースにアクセスするデータ サービスを配置する場合、データ サービスの配置でのデータ構造、データ、またはその両方の反映も必要になることがあります。 Visual Studio では対象データベースでこの操作を行うスクリプト (.sql ファイル) を自動的に作成することができ、これらのスクリプトを ASP.NET アプリケーションの Web 配置パッケージに含めることができます。 詳細については、[Web アプリケーション プロジェクトと共にデータベースを配置する](https://docs.microsoft.com/previous-versions/dd465343(v=vs.100))」を参照してください。 ASP.NET Web サイトの場合は、Visual Studio の**データベースの発行ウィザード**を使用してこの操作を実行できます。 詳細については、「[SQL Database の発行](https://docs.microsoft.com/previous-versions/aspnet/bb907585(v=vs.100))」をご覧ください。

- WCF Data Services には基本的な WCF の実装が含まれているので、Windows Server AppFabric を使用して、Windows Server 上で実行されている IIS に配置されたデータ サービスを監視できます。 Server AppFabric を使用したデータ サービスの監視の詳細については、「[Windows Server AppFabric による WCF Data Services の追跡](https://docs.microsoft.com/archive/blogs/rjacobs/tracking-wcf-data-services-with-windows-server-appfabric)」の記事を参照してください。

## <a name="see-also"></a>関連項目

- [データ サービスのホスティング](hosting-the-data-service-wcf-data-services.md)
- [WCF Data Services のセキュリティ保護](securing-wcf-data-services.md)
- [WCF Data Services の定義](defining-wcf-data-services.md)
