---
title: アプリのデプロイ
description: Windows と .NET Framework が Windows Presentation Foundation (WPF) アプリケーションに使用する配置テクノロジについて説明します。
ms.date: 03/30/2017
helpviewer_keywords:
- WPF applications [WPF], deployment
- deployment [WPF], applications
ms.assetid: 12cadca0-b32c-4064-9a56-e6a306dcc76d
ms.openlocfilehash: 62904ccd47800c8340d68c223e50688902170063
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85619300"
---
# <a name="deploy-a-wpf-application"></a>WPF アプリケーションを配置する

ビルドされた Windows Presentation Foundation (WPF) アプリケーションは、配置する必要があります。 Windows および .NET Framework には、いくつかの配置テクノロジがあります。 WPF アプリケーションの配置に使用される配置テクノロジは、アプリケーションの種類によって決まります。 このトピックでは、それぞれの配置テクノロジの概要と使用法を、それぞれの WPF アプリケーションの種類の配置要件に関連して説明します。

<a name="Deployment_Technologies"></a>
## <a name="deployment-technologies"></a>配置テクノロジ  
 Windows および .NET Framework には、次のような、いくつかの配置テクノロジがあります。  
  
- XCopy による配置。  
  
- Windows インストーラーの配置。  
  
- ClickOnce 配置。  
  
<a name="XCopy_Deployment"></a>
### <a name="xcopy-deployment"></a>XCopy による配置  
 XCopy による配置とは、XCopy コマンド ライン プログラムを使用して、ある場所から別の場所へファイルをコピーすることです。 XCopy による配置は、次のような状況に適しています。  
  
- アプリケーションは自己完結型である。 実行するためにクライアントを更新する必要がない。  
  
- アプリケーション ファイルをある場所から別の場所へ、たとえば、ビルド場所 (ローカル ディスク、UNC ファイル共有など) から公開場所 (Web サイト、UNC ファイル共有など) へ移動する必要がある。  
  
- アプリケーションはシェル統合 ([スタート] メニューのショートカット、デスクトップ アイコンなど) を必要としない。  
  
 XCopy は、単純な配置シナリオには適していますが、複雑な配置機能が必要なシナリオには十分に対応できません。 特に、配置を堅牢な方法で管理する場合、XCopy を使用すると、スクリプトの作成、実行、および維持というオーバーヘッドが生じます。 さらに、XCopy は、バージョン管理、アンインストール、およびロールバックをサポートしません。  
  
<a name="Windows_Installer"></a>
### <a name="windows-installer"></a>Windows インストーラー  
 Windows インストーラーを使用すると、アプリケーションを自己完結型の実行可能ファイルとしてパッケージ化でき、容易にクライアントに配布して、実行できます。 さらに、Windows インストーラーは Windows と共にインストールされるため、デスクトップ、[スタート] メニュー、および [プログラム] コントロール パネルとの統合が可能です。  
  
 Windows インストーラーでは、アプリケーションのインストールとアンインストールが単純化されますが、インストールされたアプリケーションをバージョン管理の観点から最新に保つ機能は提供されません。  
  
 Windows インストーラーの詳細については、「[Windows インストーラー配置](/visualstudio/deployment/deploying-applications-services-and-components#create-an-installer-package-windows-desktop)」を参照してください。
  
<a name="ClickOnce_Deployment"></a>
### <a name="clickonce-deployment"></a>ClickOnce 配置  
 ClickOnce を使用すると、非 Web アプリケーションを Web スタイル アプリケーションと同じように配置できます。 アプリケーションは、Web サーバーまたはファイル サーバーに公開され、これらのサーバーから配置されます。 ClickOnce では、Windows インストーラーによってインストールされるアプリケーションでサポートされるような広い範囲のクライアント機能がサポートされるわけではありませんが、次のような機能がサポートされます。  
  
- [スタート] メニューおよび [プログラム] コントロール パネルとの統合。  
  
- バージョン管理、ロールバック、およびアンインストール。  
  
- アプリケーションを常に配置場所から起動するオンライン インストール モード。  
  
- 新しいバージョンがリリースされたときの自動更新。  
  
- ファイル拡張子の登録。  
  
 ClickOnce の詳細については、「[ClickOnce のセキュリティと配置](/visualstudio/deployment/clickonce-security-and-deployment)」を参照してください。  
  
<a name="Deploying_WPF_Applications"></a>
## <a name="deploying-wpf-applications"></a>WPF アプリケーションの配置  
 WPF アプリケーションの配置オプションは、アプリケーションの種類によって決まります。 配置の観点から見ると、WPF には次の 3 種類のアプリケーションがあります。  
  
- スタンドアロン アプリケーション。  
  
- マークアップのみの [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] アプリケーション。  
  
- XAML ブラウザー アプリケーション (XBAP)。  
  
<a name="Deploying_Standalone_Applications"></a>
### <a name="deploying-standalone-applications"></a>スタンドアロン アプリケーションの配置  
 スタンドアロン アプリケーションは、ClickOnce または Windows インストーラーを使用して配置されます。 いずれの場合も、スタンドアロン アプリケーションを実行するには、アプリケーションが完全に信頼されている必要があります。 Windows インストーラーを使用して配置されたスタンドアロン アプリケーションには、完全な信頼が自動的に付与されます。 ClickOnce を使用して配置されたスタンドアロン アプリケーションには、完全な信頼は自動的に付与されません。 代わりに、スタンドアロン アプリケーションをインストールする前に、ClickOnce によって [セキュリティ警告] ダイアログが表示され、ユーザーがそれを受け入れる必要があります。 受け入れた場合、スタンドアロン アプリケーションがインストールされ、完全な信頼が付与されます。 受け入れなかった場合、スタンドアロン アプリケーションはインストールされません。  
  
<a name="Deploying_Markup_Only_XAML_Applications"></a>
### <a name="deploying-markup-only-xaml-applications"></a>マークアップのみの XAML アプリケーションの配置  
 マークアップのみの [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] ページは、通常、HTML ページと同様に Web サーバーに公開され、Internet Explorer を使用して表示できます。 マークアップのみの [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] ページは、部分信頼セキュリティ サンドボックス内で実行され、インターネット ゾーン アクセス許可セットによって定義された制約が適用されます。 これにより、HTML ベースの Web アプリケーションと同等のセキュリティ サンドボックスが提供されます。  
  
 WPF アプリケーションのセキュリティの詳細については、「[セキュリティ](../security-wpf.md)」を参照してください。  
  
 マークアップのみの [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] ページは、XCopy または Windows インストーラーを使用してローカル ファイル システムにインストールできます。 これらのページは、Internet Explorer または Windows エクスプローラーを使用して表示できます。  
  
 XAML の詳細については、「[XAML の概要 (WPF)](../../../desktop-wpf/fundamentals/xaml.md)」を参照してください。  
  
<a name="Deploying_XAML_Browser_Applications"></a>
### <a name="deploying-xaml-browser-applications"></a>XAML ブラウザー アプリケーションの配置  
 XBAP は、次の 3 つのファイルを配置する必要があるコンパイル済みのアプリケーションです。  
  
- *ApplicationName*.exe:実行可能アセンブリのアプリケーション ファイル。  
  
- *ApplicationName*.xbap:配置マニフェスト。  
  
- *ApplicationName*.exe.manifest:アプリケーション マニフェスト。  
  
> [!NOTE]
> 配置マニフェストおよびアプリケーション マニフェストの詳細については、「[WPF アプリケーションのビルド](building-a-wpf-application-wpf.md)」を参照してください。  
  
 これらのファイルは、XBAP がビルドされるときに生成されます。 詳細については、「[方法:新しい WPF ブラウザー アプリケーション プロジェクトを作成する](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/bb628663(v=vs.100))」を参照してください。 マークアップのみの [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] ページと同様に、XBAP は、通常、Web サーバーに発行され、Internet Explorer を使用して表示されます。  
  
 XBAP は、任意の配置技術を使用してクライアントに配置できます。 ただし、次の機能を備えている ClickOnce をお勧めします。  
  
1. 新しいバージョンが公開されたときの自動更新。  
  
2. 完全な信頼で実行する XBAP の特権の昇格。  
  
 既定では、ClickOnce は、.deploy 拡張子を持つアプリケーション ファイルを公開します。 これは問題になる可能性がありますが、無効にできます。 詳細については、「[ClickOnce 配置でのサーバーおよびクライアント構成の問題](/visualstudio/deployment/server-and-client-configuration-issues-in-clickonce-deployments)」を参照してください。  
  
 XAML ブラウザー アプリケーション (XBAP) の配置の詳細については、「[WPF XAML ブラウザー アプリケーションの概要](wpf-xaml-browser-applications-overview.md)」を参照してください。  
  
<a name="Installing__NET_Framework_3_0"></a>
## <a name="installing-the-net-framework"></a>.NET Framework のインストール  
 WPF アプリケーションを実行するには、クライアントに Microsoft .NET Framework がインストールされている必要があります。 Internet Explorer では、ブラウザーでホストされる WPF アプリケーションが表示されるとき、クライアントに .NET Framework がインストールされているかどうかが自動的に検出されます。 .NET Framework がインストールされていない場合は、Internet Explorer によってユーザーにインストールが求められます。  
  
 .NET Framework がインストールされているかどうかを検出するために、Internet Explorer には、.xaml、.xps、および .application の拡張子を持つコンテンツ ファイルのフォールバック Multipurpose Internet Mail Extensions (MIME) ハンドラーとして登録されているブートストラップ アプリケーションが含まれています。 これらのファイルの種類に移動するとき、.NET Framework がクライアントにインストールされていなかった場合、ブートス トラップ アプリケーションによってインストールの許可を求められます。 許可が与えられなかった場合は、.NET Framework もアプリケーションもインストールされません。  
  
 許可が与えられた場合、Internet Explorer では Microsoft バックグラウンド インテリジェント転送サービス (BITS) を使用して .NET Framework がダウンロードされ、インストールされます。 .NET Framework が正常にインストールされた後、最初に要求されたファイルが新しいブラウザー ウィンドウで開きます。  
  
 詳細については、「[.NET Framework およびアプリケーションの配置](../../deployment/index.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- [WPF アプリケーションのビルド](building-a-wpf-application-wpf.md)
- [セキュリティ](../security-wpf.md)
