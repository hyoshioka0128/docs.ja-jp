---
title: アドインの概要
ms.date: 03/30/2017
helpviewer_keywords:
- add-ins and XAML browser applications [WPF]
- add-ins overview [WPF]
- add-ins [WPF], performance
- add-ins [WPF], benefits
- .NET Framework add-in model [WPF]
- add-ins [WPF], user interface
- add-ins and the user interface [WPF]
- add-ins [WPF], architecture
- add-ins [WPF], limitations
ms.assetid: 00b4c776-29a8-4dba-b603-280a0cdc2ade
ms.openlocfilehash: 93904e308932ea41c736ca849ce0efb200502a7e
ms.sourcegitcommit: de17a7a0a37042f0d4406f5ae5393531caeb25ba
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/24/2020
ms.locfileid: "76738944"
---
# <a name="wpf-add-ins-overview"></a>WPF アドインの概要

<a name="Introduction"></a> .NET Framework には、開発者がアドイン機能拡張をサポートするアプリケーションの作成に使用できるアドイン モデルが用意されています。 このアドイン モデルを使用することで、アプリケーション機能に統合され、アプリケーション機能を拡張するアドインを作成できます。 一部のシナリオでは、アドインによって提供されるユーザー インターフェイスをアプリケーションで表示する必要があります。このトピックでは、WPF が .NET Framework アドイン モデルを強化してこうしたシナリオを実現するしくみ、背後にあるアーキテクチャ、その利点、および制限事項について説明します。

<a name="Requirements"></a>

## <a name="prerequisites"></a>必須コンポーネント

.NET Framework アドイン モデルを十分に理解していることが必要です。 詳細については、「[アドインおよび拡張機能](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb384200(v%3dvs.100))」を参照してください。

<a name="AddInsOverview"></a>

## <a name="add-ins-overview"></a>アドインの概要

新しい機能を追加するためにアプリケーションを再コンパイルして再配置する手間を省くことを目的として、アプリケーションは機能拡張メカニズムを実装し、開発者 (ファーストパーティ、サードパーティのいずれも) が元のアプリケーションに統合される別のアプリケーションを作成できるようにしています。 こうした拡張機能をサポートする方法としては、アドイン ("アドオン"、"プラグイン" などとも呼ばれる) の使用が最も一般的です。 アドインによる機能拡張を公開する実際のアプリケーションとして、次のようなものが挙げられます。

- Internet Explorer のアドオン。

- Windows Media Player のプラグイン。

- Visual Studio のアドイン。

たとえば、Windows Media Player のアドイン モデルにおいて、サードパーティの開発者は、Windows Media Player の機能をさまざまな形で拡張する "プラグイン" を実装できます。たとえば、Windows Media Player でネイティブにサポートされていないメディア形式 (DVD、MP3 など) のデコーダーおよびエンコーダー、オーディオ効果、スキンなどを作成できます。 各アドイン モデルは、アプリケーション固有の機能を公開するためにビルドされますが、どのアドイン モデルにも共通するエンティティや動作がいくつかあります。

典型的な機能拡張ソリューションの主な 3 つのエンティティは、*コントラクト*、*アドイン*、および*ホスト アプリケーション*です。 コントラクトは、次の 2 つの方法で、アドインとホスト アプリケーションとの統合方法を定義します。

- アドインは、ホスト アプリケーションによって実装される機能と統合されます。

- ホスト アプリケーションで、アドインを統合するための機能を公開します。

アドインを使用するには、ホスト アプリケーションが実行時にアドインを検索して読み込む必要があります。 したがって、アドインをサポートするアプリケーションには次の機能が必要です。

- **探索**: ホスト アプリケーションによってサポートされるコントラクトに準拠しているアドインを検索します。

- **アクティブ化**: アドインを読み込んで実行し、アドインとの通信を確立します。

- **分離**:アプリケーション ドメインまたはアプリケーション プロセスを使用することで他から切り離すための境界を確立し、アドインの使用に伴うセキュリティおよび実行に関する潜在的な問題からアプリケーションを保護します。

- **通信**: アドインとホスト アプリケーションが分離境界を越えて通信し、メソッドを呼び出したりデータを渡したりできるようにします。

- **有効期間管理**: アプリケーション ドメインとアプリケーション プロセスの読み込みおよびアンロードを、クリーンで予測可能な方法で行います (「[アプリケーション ドメイン](../../app-domains/application-domains.md)」を参照)。

- **バージョン管理**:ホスト アプリケーションとアドインのどちらかに、新バージョンが作成された後も引き続き通信できるようにします。

このことからわかるように、堅牢なアドイン モデルの開発は簡単なことではありません。 そのため、.NET Framework にはアドイン モデルのビルド用のインフラストラクチャが用意されています。

> [!NOTE]
> アドインの詳細については、「[アドインおよび拡張機能](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb384200(v%3dvs.100))」を参照してください。

<a name="NETFrameworkAddInModelOverview"></a>

## <a name="net-framework-add-in-model-overview"></a>.NET Framework アドイン モデルの概要

.NET Framework アドイン モデルは、<xref:System.AddIn> 名前空間にあり、アドイン機能拡張の開発を単純化するために設計された型のセットが用意されています。 .NET Framework アドイン モデルの基本単位は "*コントラクト*" です。コントラクトでは、ホスト アプリケーションとアドイン間の通信方法が定義されています。 コントラクトのホスト アプリケーション固有の*ビュー*を使用して、コントラクトはホスト アプリケーションに公開されます。 同様に、コントラクトのアドイン固有の*ビュー*がアドインに公開されます。 *アダプター*は、ホスト アプリケーションとアドインが、コントラクトの対応するビュー間で通信するために使用されます。 コントラクト、ビュー、およびアダプターはセグメントと見なされ、関連セグメントのセットが*パイプライン*を構成します。 .NET Framework アドイン モデルでは、パイプラインを基盤として、それを基に探索、アクティブ化、セキュリティ分離、実行分離 (アプリケーションのドメインとプロセスを両方使用)、通信、有効期間管理、およびバージョン管理がサポートされます。

このサポート全体を使用して、開発者はホスト アプリケーションの機能を統合するアドインをビルドできます。 ただし、一部のシナリオでは、アドインが提供するユーザー インターフェイスをホスト アプリケーションで表示する必要があります。.NET Framework の各プレゼンテーション テクノロジにはユーザー インターフェイスを実装するための独自のモデルがあるため、.NET Framework アドイン モデルでは特定のプレゼンテーション テクノロジはサポートされていません。 代わりに、WPF では、.NET Framework アドイン モデルが、アドイン用の UI サポートで拡張されます。

<a name="WPFAddInModel"></a>

## <a name="wpf-add-ins"></a>WPF アドイン

WPF を .NET Framework アドイン モデルと併用することで、ホスト アプリケーションでアドインのユーザー インターフェイスを表示する必要があるさまざまなシナリオに対応できます。特に、WPF によるこれらのシナリオの対応には、次の 2 つのプログラミング モデルが使用されます。

1. **アドインが UI を返す**。 アドインでは、コントラクトの定義に従って、メソッド呼び出しを介してホスト アプリケーションに UI が返されます。 このシナリオは、次の場合に使用されます。

    - アドインで返される UI の外観が、動的に生成されるレポートなど、実行時にしか存在しないデータまたは条件に依存している。

    - アドインで提供されるサービスのUI が、そのアドインを使用できるホスト アプリケーションの UI と異なっている。

    - アドインは主にホスト アプリケーション向けのサービスを実行し、UI を使用してホスト アプリケーションにステータスをレポートする。

2. **アドインが UI である**。 アドインが、コントラクトの定義に従う UI です。 このシナリオは、次の場合に使用されます。

    - アドインは表示以外のサービス (広告など) を提供しない。

    - アドインで提供されるサービスの UI が、そのアドインを使用できるすべてのホスト アプリケーションで共通である (電卓、カラー ピッカーなど)。

これらのシナリオでは、UI オブジェクトをホスト アプリケーション ドメインとアドイン アプリケーション ドメインとの間で受け渡しできる必要があります。 .NET Framework アドイン モデルは、アプリケーション ドメイン間の通信においてリモート処理に依存しているため、それらの間で受け渡しされるオブジェクトはリモート処理可能である必要があります。

リモート処理可能なオブジェクトとは、次の 1 つ以上に該当するクラスのインスタンスです。

- <xref:System.MarshalByRefObject> クラスから派生しています。

- <xref:System.Runtime.Serialization.ISerializable> インターフェイスを実装します。

- <xref:System.SerializableAttribute> 属性が適用されています。

> [!NOTE]
> リモート処理可能な .NET Framework オブジェクトの作成の詳細については、「[オブジェクトをリモート処理可能にする](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/wcf3swha(v=vs.100))」を参照してください。

WPF UI 型は、リモート処理可能ではありません。 この問題を解決するため、WPF では .NET Framework アドイン モデルが拡張され、アドインによって作成される WPF UI をホスト アプリケーションで表示できるようになります。 これは WPF によって、<xref:System.AddIn.Contract.INativeHandleContract> インターフェイス、および <xref:System.AddIn.Pipeline.FrameworkElementAdapters> クラスによって実装される 2 つの静的メソッド <xref:System.AddIn.Pipeline.FrameworkElementAdapters.ContractToViewAdapter%2A> と <xref:System.AddIn.Pipeline.FrameworkElementAdapters.ViewToContractAdapter%2A> という、2 つの方法でサポートされています。 大まかに、これらの型とメソッドは次のように使用されます。

1. WPF では、アドインによって提供されるユーザー インターフェイスは、図形、コントロール、ユーザー コントロール、レイアウト パネル、ページなど、<xref:System.Windows.FrameworkElement> から直接または間接的に派生したクラスである必要があります。

2. UI がアドインとホスト アプリケーションとの間で受け渡しされることをコントラクトで宣言する場合、必ず (<xref:System.Windows.FrameworkElement> ではなく) <xref:System.AddIn.Contract.INativeHandleContract> として宣言する必要があります。<xref:System.AddIn.Contract.INativeHandleContract> はアドイン UI のリモート処理可能な表現で、分離境界を越えて受け渡しできます。

3. アドインのアプリケーション ドメインから渡される前に、<xref:System.Windows.FrameworkElement> は、<xref:System.AddIn.Pipeline.FrameworkElementAdapters.ViewToContractAdapter%2A> の呼び出しによって、<xref:System.AddIn.Contract.INativeHandleContract> としてパッケージ化されます。

4. ホスト アプリケーションのアプリケーション ドメインに渡された後、<xref:System.AddIn.Contract.INativeHandleContract> は、<xref:System.AddIn.Pipeline.FrameworkElementAdapters.ContractToViewAdapter%2A> の呼び出しによって、<xref:System.Windows.FrameworkElement> として再パッケージ化する必要があります。

<xref:System.AddIn.Contract.INativeHandleContract>、<xref:System.AddIn.Pipeline.FrameworkElementAdapters.ContractToViewAdapter%2A>、および <xref:System.AddIn.Pipeline.FrameworkElementAdapters.ViewToContractAdapter%2A> の使用方法は、個々のシナリオによって異なります。 以降のセクションでは、各プログラミング モデルについて詳しく説明していきます。

<a name="ReturnUIFromAddInContract"></a>

## <a name="add-in-returns-a-user-interface"></a>ユーザー インターフェイスを返すアドイン

アドインが UI をホスト アプリケーションに返すには、次のことが必要です。

1. ホスト アプリケーション、アドイン、およびパイプラインが、.NET Framework の「[アドインおよび拡張機能](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb384200(v%3dvs.100))」の説明に従って作成されている必要があります。

2. コントラクトで <xref:System.AddIn.Contract.IContract> が実装されている必要があります。また、UI を返すためには、戻り値が <xref:System.AddIn.Contract.INativeHandleContract> 型であるメソッドがコントラクトで宣言されている必要があります。

3. アドインとホスト アプリケーションとの間で受け渡される UI は、直接または間接的に、<xref:System.Windows.FrameworkElement> から派生している必要があります。

4. アドインによって返される UI は、分離境界を越える前に、<xref:System.Windows.FrameworkElement> から <xref:System.AddIn.Contract.INativeHandleContract> に変換される必要があります。

5. 返される UI は、分離境界を越えた後で、<xref:System.AddIn.Contract.INativeHandleContract> から <xref:System.Windows.FrameworkElement> に変換される必要があります。

6. ホスト アプリケーションでは、返された <xref:System.Windows.FrameworkElement> を表示します。

UI を返すアドインを実装する方法の例については、「[UI を返すアドインを作成する](how-to-create-an-add-in-that-returns-a-ui.md)」を参照してください。

<a name="AddInIsAUI"></a>

## <a name="add-in-is-a-user-interface"></a>ユーザー インターフェイスであるアドイン

アドインが UI である場合、次のことが必要です。

1. ホスト アプリケーション、アドイン、およびパイプラインが、.NET Framework の「[アドインおよび拡張機能](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb384200(v%3dvs.100))」の説明に従って作成されている必要があります。

2. アドインのコントラクト インターフェイスで、<xref:System.AddIn.Contract.INativeHandleContract> が実装されている必要があります。

3. ホスト アプリケーションに渡されるアドインが、直接または間接的に、<xref:System.Windows.FrameworkElement> から派生している必要があります。

4. アドインは、分離境界を越える前に <xref:System.Windows.FrameworkElement> から <xref:System.AddIn.Contract.INativeHandleContract> に変換される必要があります。

5. アドインは、分離境界を越えた後で <xref:System.AddIn.Contract.INativeHandleContract> から <xref:System.Windows.FrameworkElement> に変換される必要があります。

6. ホスト アプリケーションでは、返された <xref:System.Windows.FrameworkElement> を表示します。

UI であるアドインを実装する方法の例については、「[UI であるアドインを作成する](how-to-create-an-add-in-that-is-a-ui.md)」を参照してください。

<a name="ReturningMultipleUIsFromAnAddIn"></a>

## <a name="returning-multiple-uis-from-an-add-in"></a>複数の UI を返すアドイン

アドインで提供される複数のユーザー インターフェイスをホスト アプリケーションで表示することはよくあります。 たとえば、UI であるアドインが、ホスト アプリケーションにステータス情報も UI として提供するとします。 このようなアドインは、[ユーザー インターフェイスを返すアドイン](#ReturnUIFromAddInContract)のモデルと[ユーザー インターフェイスであるアドイン](#AddInIsAUI)のモデルの両方の手法を組み合わせることで実装できます。

<a name="AddInsAndXBAPs"></a>

## <a name="add-ins-and-xaml-browser-applications"></a>アドインと XAML ブラウザー アプリケーション

ここまでの例では、ホスト アプリケーションはスタンドアロン アプリケーションとしてインストールされています。 XAML ブラウザー アプリケーション (XBAP) はアドインをホストすることもできますが、そのためには次に示すビルドと実装の要件を満たす必要があります。

- パイプライン (フォルダーとアセンブリ) とアドイン アセンブリを、XBAP と同じフォルダーにある、クライアント コンピューターの ClickOnce アプリケーション キャッシュにダウンロードするよう、XBAP アプリケーション マニフェストを特別に構成する必要があります。

- アドインを探索して読み込む XBAP コードで、XBAP の ClickOnce アプリケーション キャッシュを、パイプラインとアドインの場所として使用する必要があります。

- XBAP では、アドインが起点サイトにある圧縮しないファイルを参照する場合、アドインを特別なセキュリティ コンテキストの下で読み込む必要があります。XBAP によってホストされる場合、アドインが参照できるのは、ホスト アプリケーションの起点サイトにある圧縮しないファイルのみです。

これらのタスクについて、次のサブセクションで詳しく説明します。

### <a name="configuring-the-pipeline-and-add-in-for-clickonce-deployment"></a>ClickOnce 配置のためのパイプラインとアドインの構成

XBAP では、ClickOnce 配置キャッシュの安全なフォルダーにダウンロードされ、そこから実行されます。 XBAP でアドインをホストするには、パイプラインとアドインのアセンブリも同じ安全なフォルダーにダウンロードする必要があります。 このためには、パイプラインとアドインのどちらのアセンブリもダウンロード対象に含まれるよう、アプリケーション マニフェストを構成する必要があります。 これは、Visual Studio で実行することが最も簡単ですが、Visual Studio でパイプラインをアセンブリとして検出するには、パイプラインとアドインのアセンブリが、ホスト XBAP プロジェクトのルート フォルダーに存在する必要があります。

したがって、まず、パイプライン アセンブリとアドイン アセンブリの各プロジェクトのビルド出力を設定し、パイプラインとアドインのアセンブリを XBAP プロジェクトのルートにビルドします。 次の表は、ホストの XBAP プロジェクトと同じソリューションとルートのフォルダーに格納される、パイプライン アセンブリ プロジェクトとアドイン アセンブリ プロジェクトのビルド出力パスを示します。

表 1:XBAP でホストされるパイプライン アセンブリのビルド出力パス

|パイプライン アセンブリ プロジェクト|ビルド出力パス|
|-------------------------------|-----------------------|
|コントラクト|`..\HostXBAP\Contracts\`|
|アドイン ビュー|`..\HostXBAP\AddInViews\`|
|アドイン側のアダプター|`..\HostXBAP\AddInSideAdapters\`|
|ホスト側のアダプター|`..\HostXBAP\HostSideAdapters\`|
|アドイン|`..\HostXBAP\AddIns\WPFAddIn1`|

次に、パイプライン アセンブリとアドイン アセンブリを XBAP コンテンツ ファイルとして Visual Studio に指定します。手順は次のとおりです。

1. ソリューション エクスプローラーで各パイプライン フォルダーを右クリックし、 **[プロジェクトに含める]** を選択して、パイプラインとアドインのアセンブリをプロジェクトに含めます。

2. **[プロパティ]** ウィンドウで、パイプライン アセンブリとアドイン アセンブリそれぞれについて、 **[ビルド アクション]** を **[コンテンツ]** に設定します。

最後に、パイプラインとアドインのどちらのアセンブリ ファイルもダウンロード対象に含まれるよう、アプリケーション マニフェストを構成します。 ファイルは、XBAP アプリケーションが占有する ClickOnce キャッシュ内のフォルダーのルートにあるフォルダー内に存在している必要があります。 この構成は、次の手順に従って、Visual Studio で行うことができます。

1. XBAP プロジェクトを右クリックして、 **[プロパティ]** 、 **[発行]** の順にクリックし、 **[アプリケーション ファイル]** ボタンをクリックします。

2. **[アプリケーション ファイル]** ダイアログ ボックスで、各パイプラインとアドインの DLL の **[発行の状況]** を **[含める (自動)]** に設定し、各パイプラインとアドインの DLL の **[ダウンロード グループ]** を **[(必須)]** に設定します。

### <a name="using-the-pipeline-and-add-in-from-the-application-base"></a>アプリケーション ベースからのパイプラインとアドインの使用

パイプラインとアドインは ClickOnce 配置用に構成されると、XBAP と同じ ClickOnce キャッシュ フォルダーにダウンロードされます。 このパイプラインとアドインを XBAP から使用するには、XBAP コードでそれらをアプリケーション ベースから取得する必要があります。 .NET Framework アドイン モデルのさまざまな型やメンバーでは、パイプラインおよびアドインを使用できるよう、このシナリオ用に特別なサポートが提供されています。 まず、パスは <xref:System.AddIn.Hosting.PipelineStoreLocation.ApplicationBase> 列挙値で識別されます。 この値を適切なアドイン メンバーのオーバーロードと併用することで、次のようなパイプラインを使用できます。

- <xref:System.AddIn.Hosting.AddInStore.FindAddIns%28System.Type%2CSystem.AddIn.Hosting.PipelineStoreLocation%29?displayProperty=nameWithType>

- <xref:System.AddIn.Hosting.AddInStore.FindAddIns%28System.Type%2CSystem.AddIn.Hosting.PipelineStoreLocation%2CSystem.String%5B%5D%29?displayProperty=nameWithType>

- <xref:System.AddIn.Hosting.AddInStore.Rebuild%28System.AddIn.Hosting.PipelineStoreLocation%29?displayProperty=nameWithType>

- <xref:System.AddIn.Hosting.AddInStore.Update%28System.AddIn.Hosting.PipelineStoreLocation%29?displayProperty=nameWithType>

### <a name="accessing-the-hosts-site-of-origin"></a>ホストの起点サイトへのアクセス

アドインが起点サイトのファイルを参照できるように、アドインはホスト アプリケーションと等価なセキュリティ分離を使用して読み込む必要があります。 このセキュリティ レベルは <xref:System.AddIn.Hosting.AddInSecurityLevel.Host?displayProperty=nameWithType> 列挙値によって示され、アドインがアクティブ化されると <xref:System.AddIn.Hosting.AddInToken.Activate%2A> メソッドに渡されます。

<a name="WPFAddInModelArchitecture"></a>

## <a name="wpf-add-in-architecture"></a>WPF アドイン アーキテクチャ

これまで見てきたように、最上位のレベルでは、WPF を使用することによって、.NET Framework アドインで、(<xref:System.Windows.FrameworkElement> から直接または間接的に派生した) ユーザー インターフェイス を、<xref:System.AddIn.Contract.INativeHandleContract>、<xref:System.AddIn.Pipeline.FrameworkElementAdapters.ViewToContractAdapter%2A>、および <xref:System.AddIn.Pipeline.FrameworkElementAdapters.ContractToViewAdapter%2A> を使用して実装できます。 その結果、ホスト アプリケーションに <xref:System.Windows.FrameworkElement> が返され、ホスト アプリケーションの UI で表示されます。

簡単な UI アドイン シナリオでは、開発者に必要な詳細はこれだけです。 より複雑なシナリオ、特にレイアウト、リソース、データ バインディングなど、追加の WPF サービスの活用を想定したシナリオでは、その利点と制約を把握するために UI をサポートする .NET Framework アドイン モデルが、WPF で拡張されるしくみについて詳しい知識が必要です。

基本的に、WPF ではアドインからホスト アプリケーションに UI は渡されません。その代わり、WPF では UI の Win32 ウィンドウ ハンドルが WPF 相互運用性を使用して渡されます。 つまり、アドインの UI がホスト アプリケーションに渡されると、次の処理が行われます。

- アドイン側では、WPF によって、ホスト アプリケーションによって表示される UI のウィンドウ ハンドルが取得されます。 このウィンドウ ハンドルは、<xref:System.Windows.Interop.HwndSource> から派生し、<xref:System.AddIn.Contract.INativeHandleContract> を実装する内部 WPF クラスによってカプセル化されます。 このクラスのインスタンスは、<xref:System.AddIn.Pipeline.FrameworkElementAdapters.ViewToContractAdapter%2A> によって返され、アドインのアプリケーション ドメインからホスト アプリケーションのアプリケーション ドメインにマーシャリングされます。

- ホスト アプリケーション側では、<xref:System.Windows.Interop.HwndSource> は、<xref:System.Windows.Interop.HwndHost> から派生し、<xref:System.AddIn.Contract.INativeHandleContract> を消費する内部 WPF クラスとして、WPF によって再パッケージ化されます。 このクラスのインスタンスは、<xref:System.AddIn.Pipeline.FrameworkElementAdapters.ContractToViewAdapter%2A> によってホスト アプリケーションに返されます。

<xref:System.Windows.Interop.HwndHost> は、ウィンドウ ハンドルによって識別されるユーザー インターフェイスを WPF ユーザー インターフェイスで表示するために存在します。 詳細については、「[WPF と Win32 の相互運用性](../advanced/wpf-and-win32-interoperation.md)」を参照してください。

まとめると、<xref:System.AddIn.Contract.INativeHandleContract>、<xref:System.AddIn.Pipeline.FrameworkElementAdapters.ViewToContractAdapter%2A>、および <xref:System.AddIn.Pipeline.FrameworkElementAdapters.ContractToViewAdapter%2A> は、WPF UI のウィンドウ ハンドルを、アドインからホスト アプリケーションに渡すために存在します。渡されると、<xref:System.Windows.Interop.HwndHost> によってカプセル化され、ホスト アプリケーションの UI を表示します。

> [!NOTE]
> ホスト アプリケーションは <xref:System.Windows.Interop.HwndHost> を取得するので、ホスト アプリケーションでは <xref:System.AddIn.Pipeline.FrameworkElementAdapters.ContractToViewAdapter%2A> から返されるオブジェクトを、アドインによって実装された型 (<xref:System.Windows.Controls.UserControl> など) に変換できません。

その特質上、<xref:System.Windows.Interop.HwndHost> には、ホスト アプリケーションの使用に影響する制約があります。 ただし、WPF では、<xref:System.Windows.Interop.HwndHost> がアドイン シナリオ用の複数の機能で拡張されます。 その利点と制約について、以下に説明します。

<a name="WPFAddInModelBenefits"></a>

## <a name="wpf-add-in-benefits"></a>WPF アドインの利点

WPF アドインのユーザー インターフェイスは、<xref:System.Windows.Interop.HwndHost> から派生する内部クラスを使用してホスト アプリケーションで表示されるため、そのようなユーザー インターフェイスは、レイアウト、レンダリング、データ バインディング、スタイル、テンプレート、リソースなどの WPF UI サービスに関して、<xref:System.Windows.Interop.HwndHost> の機能の制約を受けます。 ただし、WPF では、その内部 <xref:System.Windows.Interop.HwndHost> サブクラスが、次のような追加機能で強化されます。

- ホスト アプリケーションの UI とアドインの UI との間を Tab キーで移動できます。 "アドインが UI である" プログラミング モデルでは、アドインが完全に信頼されているか部分的に信頼されているかに関係なく、アドイン側のアダプターが <xref:System.AddIn.Pipeline.ContractBase.QueryContract%2A> をオーバーライドして、Tab キーによる移動処理を有効にする必要があります。

- ホスト アプリケーションのユーザー インターフェイスで表示されるアドインのユーザー インターフェイスのアクセシビリティ要件を順守します。

- アプリケーション ドメインが複数あるシナリオで WPF アプリケーションが安全に実行されます。

- アドインがセキュリティ分離を使用して実行されている場合 (部分的に信頼されているセキュリティ サンドボックス)、アドイン UI ウィンドウ ハンドルへの不正アクセスを回避します。 <xref:System.AddIn.Pipeline.FrameworkElementAdapters.ViewToContractAdapter%2A> を呼び出すことでこのセキュリティが保証されます。

  - "アドインが IU を返す" プログラミング モデルで、アドイン UI のウィンドウ ハンドルを分離境界を越えて渡す唯一の方法は、<xref:System.AddIn.Pipeline.FrameworkElementAdapters.ViewToContractAdapter%2A> を呼び出すことです。

  - "アドインが UI である" プログラミング モデルでは、アドイン側のアダプターで <xref:System.AddIn.Pipeline.ContractBase.QueryContract%2A> をオーバーライドして <xref:System.AddIn.Pipeline.FrameworkElementAdapters.ViewToContractAdapter%2A> を呼び出すこと (前の例に従って) が、アドイン側のアダプターの `QueryContract` 実装をホスト側のアダプターから呼び出すことに相当する処理として必要です。

- アプリケーション ドメインの実行を何重にも保護します。 アプリケーション ドメインの制約に起因して、アドイン アプリケーション ドメインでスローされた未処理の例外は、分離境界が存在していても、アプリケーション全体のクラッシュにつながります。 ただし、WPF と .NET Framework アドイン モデルでは、この問題を回避して、アプリケーションの安定性を向上させる簡単な手段が提供されます。 UI を表示する WPF アドインでは、ホスト アプリケーションが WPF アプリケーションである場合に、アプリケーション ドメインが実行されているスレッドの <xref:System.Windows.Threading.Dispatcher> が作成されます。 WPF アドインの <xref:System.Windows.Threading.Dispatcher> の <xref:System.Windows.Threading.Dispatcher.UnhandledException> イベントを処理することで、アプリケーション ドメインで発生した未処理の例外をすべて検出できます。 <xref:System.Windows.Threading.Dispatcher.CurrentDispatcher%2A> プロパティから <xref:System.Windows.Threading.Dispatcher> を取得できます。

<a name="WPFAddInModelLimitations"></a>

## <a name="wpf-add-in-limitations"></a>WPF アドインの制約

WPF には、<xref:System.Windows.Interop.HwndSource>、<xref:System.Windows.Interop.HwndHost>、ウィンドウ ハンドルによって提供される既定の動作が強化される利点もありますが、ホスト アプリケーションで表示されるアドイン ユーザー インターフェイスに対する制約もあります。

- ホスト アプリケーションで表示されるアドイン ユーザー インターフェイスでは、ホスト アプリケーションのクリッピング動作が考慮されません。

- 相互運用性シナリオの*空域*の概念もアドインに適用されます (「[技術領域の概要](../advanced/technology-regions-overview.md)」を参照)。

- リソースの継承、データ バインディング、コマンド実行など、ホスト アプリケーションの UI サービスは、アドイン ユーザー インターフェイスで自動的には使用可能になりません。 これらのサービスをアドインに提供するには、パイプラインを更新する必要があります。

- アドイン UI に回転、拡大縮小、傾斜などの変換は適用できません (「[変換の概要](../graphics-multimedia/transforms-overview.md)」を参照)。

- <xref:System.Drawing> 名前空間の描画操作によってレンダリングされるアドイン ユーザー インターフェイス内のコンテンツに、アルファ ブレンド効果を含めることができます。 ただし、それを含むアドイン UI とホスト アプリケーション UI のいずれも、100% 不透明である必要があります。言い換えると、どちらについても `Opacity` プロパティが 1 に設定されている必要があります。

- アドイン UI が含まれるホスト アプリケーションのウィンドウの <xref:System.Windows.Window.AllowsTransparency%2A> プロパティが `true` の場合、アドインは非表示になります。 このことは、アドイン UI が 100% 不透明 (`Opacity` プロパティの値が 1) の場合にも該当します。

- アドイン UI は、同じトップレベル ウィンドウ内の他の WPF 要素より前面に表示する必要があります。

- アドインの UI には、<xref:System.Windows.Media.VisualBrush> を使用してレンダリングできる部分はありません。 その代わり、アドインは生成された UI のスナップショットを取り、コントラクトで定義されているメソッドを使用してホスト アプリケーションに渡すことができるビットマップを作成できます。

- メディア ファイルをアドイン UI 内の <xref:System.Windows.Controls.MediaElement> で再生することはできません。

- ホスト アプリケーションがアドイン UI 用に生成されたマウス イベントを受け取ったり、発生させたりすることはなく、ホスト アプリケーション UI の `IsMouseOver` プロパティの値は `false` に設定されます。

- アドイン UI 内のコントロール間を、フォーカスが移動しても、`GotFocus` イベントや `LostFocus` イベントをホスト アプリケーションで受け取ったり、発生したりすることはありません。

- アドイン UI を含むホスト アプリケーション部分は、印刷時には白く出力されます。

- アドイン UI によって作成されたすべてのディスパッチャー (<xref:System.Windows.Threading.Dispatcher> を参照) は、ホスト アプリケーションが実行を継続する場合、オーナー アドインがアンロードされる前に手動でシャットダウンする必要があります。 コントラクトは、アドインがアンロードされる前にホスト アプリケーションがアドインにシグナルを送信するためのメソッドを実装でき、それによりアドイン UI がそのディスパッチャーをシャットダウンできます。

- アドイン UI が <xref:System.Windows.Controls.InkCanvas> である場合、または <xref:System.Windows.Controls.InkCanvas> を含んでいる場合、そのアドインをアンロードすることはできません。

<a name="PerformanceOptimization"></a>

## <a name="performance-optimization"></a>パフォーマンスの最適化

既定では、複数のアプリケーション ドメインが使用されていると、各アプリケーションで必要とされているさまざまな .NET Framework アセンブリがすべてそのアプリケーションのドメインに読み込まれます。 その結果、新しいアプリケーション ドメインを作成してその中でアプリケーションを開始するために必要な時間がパフォーマンスに影響します。 ただし、.NET Framework には、アセンブリが既に読み込まれている場合に、それをアプリケーション ドメイン間で共有するようアプリケーションに指示することで開始時間を短縮する手段が用意されています。 これを実行するには、<xref:System.LoaderOptimizationAttribute> 属性を使用します。これを、エントリ ポイント メソッド (`Main`) に適用する必要があります。 この場合、アプリケーション定義を実装するコードのみを使用する必要があります (「[アプリケーション管理の概要](application-management-overview.md)」を参照)。

## <a name="see-also"></a>関連項目

- <xref:System.LoaderOptimizationAttribute>
- [アドインおよび拡張機能](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb384200(v%3dvs.100))
- [アプリケーション ドメイン](../../app-domains/application-domains.md)
- [.NET Framework リモート処理の概要](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/kwdt6w2k(v=vs.100))
- [オブジェクトをリモート処理可能にする](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/wcf3swha(v=vs.100))
- [方法トピック](how-to-topics.md)
