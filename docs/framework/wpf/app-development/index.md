---
title: アプリケーション開発
description: Windows Presentation Foundation (WPF) のフレームワークを使用してさまざまなアプリケーションを構築する方法について説明します。
ms.date: 01/26/2018
helpviewer_keywords:
- WPF [WPF], about application development
- application development [WPF], about
ms.assetid: 2996ce5e-81e9-49ae-881b-952db3dd1b7e
ms.openlocfilehash: ac4227785f2fc398217b3aa8984176844264bbaa
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85613736"
---
# <a name="application-development"></a>アプリケーション開発
<a name="introduction"></a> Windows Presentation Foundation (WPF) は、次のような種類のアプリケーションの開発に使用できるプレゼンテーション フレームワークです。  
  
- スタンドアロン アプリケーション (クライアント コンピューターにインストールし、そこから実行できる実行可能アセンブリとしてビルドされた従来スタイルの Windows アプリケーション)。  
  
- XAML ブラウザー アプリケーション (XBAP) (Microsoft Internet Explorer や Mozilla Firefox などの Web ブラウザーでホストされ、実行可能アセンブリとしてビルドされたナビゲーション ページで構成されるアプリケーション)。  
  
- カスタム コントロール ライブラリ (再利用可能なコントロールを含む被実行可能アセンブリ)。  
  
- クラス ライブラリ (再利用可能なクラスを含む非実行可能アセンブリ)。  
  
> [!NOTE]
> Windows サービスで WPF 型を使用するのは避けることを強くお勧めします。 Windows サービスでこれらの機能を使用すると、期待どおりの動作が得られない場合があります。  
  
 WPF では、このような一連のアプリケーションをビルドするサービスを多数実装しています。 このトピックでは、これらのサービスの概要を説明し、詳細情報へのリンクを示します。  

<a name="Application_Management"></a>
## <a name="application-management"></a>アプリケーション構成の管理  
 実行可能 WPF アプリケーションは、一般に次のコアな機能セットを必要とします。  
  
- 共通アプリケーション インフラストラクチャを作成し、管理する (エントリ ポイント メソッドと、システム メッセージおよび入力メッセージを受け取るための Windows メッセージ ループの作成を含む)。  
  
- アプリケーションの有効期間を追跡し、これと相互作用する。  
  
- コマンド ライン パラメーターを取得し、処理する。  
  
- アプリケーション スコープのプロパティと [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] リソースを共有する。  
  
- 未処理の例外を検出し、処理する。  
  
- 終了コードを返す。  
  
- スタンドアロン アプリケーションのウィンドウを管理する。  
  
- XAML ブラウザー アプリケーション (XBAP) や、ナビゲーション ウィンドウとフレームを持つスタンドアロン アプリケーションで、ナビゲーションを追跡する。  
  
 これらの機能は <xref:System.Windows.Application> クラスで実装します。このクラスをアプリケーションに追加するには、*アプリケーション定義*を使用します。  
  
 詳細については、「[アプリケーション管理の概要](application-management-overview.md)」を参照してください。  
  
<a name="WPF_Application_Resource__Content__and_Data_Files"></a>
## <a name="wpf-application-resource-content-and-data-files"></a>WPF アプリケーションのリソース ファイル、コンテンツ ファイル、およびデータ ファイル  
 WPF では、埋め込みリソースを扱う Microsoft .NET Framework のコア サポートが拡張され、リソース、コンテンツ、データの 3 種類の非実行可能データ ファイルを追加サポートしています。 詳細については、「[WPF アプリケーションのリソース、コンテンツ ファイル、およびデータ ファイル](wpf-application-resource-content-and-data-files.md)」を参照してください。  
  
 WPF の非実行可能データ ファイルをサポートすることの重要なコンポーネントは、一意の URI を使用して、これらのファイルを識別し、読み込むことができることです。 詳細については、「[WPF におけるパック URI](pack-uris-in-wpf.md)」を参照してください。  
  
<a name="Windows_and_Dialog_Boxes"></a>
## <a name="windows-and-dialog-boxes"></a>ウィンドウとダイアログ ボックス  
 ユーザーは、ウィンドウを使用して、WPF スタンドアロン アプリケーションとやり取りします。 ウィンドウの目的は、アプリケーションのコンテンツをホストし、コンテンツとやり取りするためにユーザーが利用できるアプリケーション機能を公開することです。 WPF では、ウィンドウは <xref:System.Windows.Window> クラスにカプセル化されます。このクラスは、次の機能を備えています。  
  
- ウィンドウを作成し、表示する。  
  
- 所有者と所有ウィンドウの関係を確立する。  
  
- ウィンドウの外観を構成する (サイズ、位置、アイコン、タイトル バーのテキスト、境界など)。  
  
- ウィンドウの有効期間を追跡し、これと相互作用する。  
  
 詳細については、「[WPF ウィンドウの概要](wpf-windows-overview.md)」を参照してください。  
  
 <xref:System.Windows.Window> では、ダイアログ ボックスと呼ばれる特別な種類のウィンドウを作成できます。 モーダル ダイアログ ボックスとモードレス ダイアログ ボックスの両方の種類のダイアログ ボックスを作成できます。  
  
 使いやすさと、アプリケーション間での再利用性およびユーザー エクスペリエンスの整合性というメリットの実現に、WPF では、<xref:Microsoft.Win32.OpenFileDialog>、<xref:Microsoft.Win32.SaveFileDialog>、<xref:System.Windows.Controls.PrintDialog> という 3 つの一般的な Windows のダイアログ ボックスを公開しています。  
  
 メッセージ ボックスは、重要な情報をテキストでユーザーに表示し、単純な [はい]、[いいえ]、[OK]、[キャンセル] の応答を求めるために使用する特別なダイアログ ボックスです。 メッセージ ボックスを作成および表示するには <xref:System.Windows.MessageBox> クラスを使用します。  
  
 詳細については、「[ダイアログ ボックスの概要](dialog-boxes-overview.md)」を参照してください。  
  
<a name="Navigation"></a>
## <a name="navigation"></a>ナビゲーション  
 WPF では、ページ (<xref:System.Windows.Controls.Page>) およびハイパーリンク (<xref:System.Windows.Documents.Hyperlink>) を使用した Web スタイルのナビゲーションをサポートしています。 ナビゲーションは、次のようなさまざまな方法で実装できます。  
  
- Web ブラウザーでホストされるスタンドアロンのページ。  
  
- Web ブラウザーでホストされる XBAP にコンパイルされるページ。  
  
- スタンドアロン アプリケーションにコンパイルされ、ナビゲーション ウィンドウ (<xref:System.Windows.Navigation.NavigationWindow>) によってホストされるページ。  
  
- フレーム (<xref:System.Windows.Controls.Frame>) によってホストされるページ。フレームは、スタンドアロン ページか、XBAP またはスタンドアロン アプリケーションにコンパイルされたページでホストできます。  
  
 WPF では、ナビゲーションに役立つ次の機能が実装されています。  
  
- ナビゲーション要求を処理する共有ナビゲーション エンジンである <xref:System.Windows.Navigation.NavigationService>。このエンジンは <xref:System.Windows.Controls.Frame>、<xref:System.Windows.Navigation.NavigationWindow>、XBAP で使用され、アプリケーション内ナビゲーションをサポートします。  
  
- ナビゲーションを開始するためのナビゲーション メソッド。  
  
- ナビゲーションの有効期間を追跡し、これと相互作用するためのナビゲーション イベント。  
  
- 履歴を使用した前方や後方へのナビゲーションの記憶。履歴は、調べたり、操作したりすることもできます。  
  
 詳細については、「[ナビゲーションの概要](navigation-overview.md)」を参照してください。  
  
 WPF は、構造化ナビゲーションと呼ばれる特別な種類のナビゲーションもサポートしています。 構造化ナビゲーションを使用すると、呼び出し元関数との一貫性が保たれた、構造化されて予測可能な形式でデータを返す 1 つ以上のページを呼び出す事ができます。 この機能は <xref:System.Windows.Navigation.PageFunction%601> クラスに依存します。このクラスの詳細については、「[構造化ナビゲーションの概要](structured-navigation-overview.md)」を参照してください。 また、<xref:System.Windows.Navigation.PageFunction%601> を使用すると、複雑なナビゲーション トポロジを簡単に作成することもできます。詳細については、「[ナビゲーション トポロジの概要](navigation-topologies-overview.md)」を参照してください。  
  
<a name="Hosting"></a>
## <a name="hosting"></a>ホスト  
 XBAP は、Microsoft Internet Explorer または Firefox でホストできます。 ホストのモデルによって考慮事項や制約が異なります。詳細については、「[ホスティング](hosting-wpf-applications.md)」を参照してください。  
  
<a name="Build_and_Deploy"></a>
## <a name="build-and-deploy"></a>ビルドと配置  
 単純な WPF アプリケーションはコマンドライン コンパイラを使用してコマンド プロンプトでビルドできますが、WPF に Visual Studio が統合されていることで、開発とビルドのプロセスを簡略化する追加のサポートがあります。 詳細については、「[WPF アプリケーションのビルド](building-a-wpf-application-wpf.md)」を参照してください。  
  
 ビルドするアプリケーションの種類によって、選択する配置オプションが異なります。 詳細については、「[WPF アプリケーションの配置](deploying-a-wpf-application-wpf.md)」を参照してください。  
  
<a name="related_topics"></a>
## <a name="related-topics"></a>関連トピック  
  
|Title|説明|  
|-----------|-----------------|  
|[アプリケーション管理の概要](application-management-overview.md)|アプリケーションの有効期間、ウィンドウ、アプリケーション リソース、ナビゲーションの管理など、<xref:System.Windows.Application> クラスの概要について説明します。|  
|[WPF のウィンドウ](windows-in-wpf-applications.md)|<xref:System.Windows.Window> クラスおよびダイアログ ボックスの使い方など、アプリケーション内のウィンドウ管理の詳細について説明します。|  
|[ナビゲーションの概要](navigation-overview.md)|アプリケーション内のページ間でのナビゲーション管理の概要について説明します。|  
|[ホスティング](hosting-wpf-applications.md)|XAML ブラウザー アプリケーション (XBAP) の概要について説明します。|  
|[ビルドと配置](building-and-deploying-wpf-applications.md)|WPF アプリケーションをビルドして配置する方法について説明します。|  
|[Visual Studio での WPF の概要](../getting-started/introduction-to-wpf-in-vs.md)|WPF の主な機能について説明します。|  
|[チュートリアル: 初めての WPF デスクトップ アプリケーション](../getting-started/walkthrough-my-first-wpf-desktop-application.md)|ページ ナビゲーション、レイアウト、コントロール、イメージ、スタイル、バインディングを使用する WPF アプリケーションの作成方法を示すチュートリアルです。|
