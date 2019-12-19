---
title: .NET Framework 配置ガイド (開発者向け)
ms.custom: updateeachrelease
ms.date: 04/18/2019
helpviewer_keywords:
- developer's guide, deploying .NET Framework
- deployment [.NET Framework], developer's guide
ms.assetid: 094d043e-33c4-40ba-a503-e0b20b55f4cf
ms.openlocfilehash: 1b7fccc673f82986a53dcb3dfcb68e8575b99dfd
ms.sourcegitcommit: 42ed59871db1f29a32b3d8e7abeb20e6eceeda7c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/10/2019
ms.locfileid: "74959993"
---
# <a name="net-framework-deployment-guide-for-developers"></a>.NET Framework 配置ガイド (開発者向け)
このトピックでは、.NET Framework 4.5 から [!INCLUDE[net_current](../../../includes/net-current-version.md)] までの任意のバージョンの .NET Framework を、それぞれのアプリと共にインストールする開発者向けの情報を提供します。

ダウンロード リンクについては、「[頒布可能パッケージ](#redistributable-packages)」を参照してください。 再頒布可能パッケージと言語パックは、Microsoft ダウンロード センターの次のページからダウンロードすることもできます。

- すべてのオペレーティング システムの .NET Framework 4.8 ([Web インストーラー](https://go.microsoft.com/fwlink/?LinkId=2085155)または[オフライン インストーラー](https://go.microsoft.com/fwlink/?linkid=2088631))

- すべてのオペレーティング システムの .NET Framework 4.7.2 ([Web インストーラー](https://go.microsoft.com/fwlink/?LinkId=863262) または [オフライン インストーラー](https://go.microsoft.com/fwlink/p/?LinkId=863265))

- すべてのオペレーティング システムの .NET Framework 4.7.1 ([Web インストーラー](https://go.microsoft.com/fwlink/?LinkId=852095) または [オフライン インストーラー](https://go.microsoft.com/fwlink/p/?LinkId=852107))

- すべてのオペレーティング システムの .NET Framework 4.7 ([Web インストーラー](https://go.microsoft.com/fwlink/?LinkId=825299)または[オフライン インストーラー](https://go.microsoft.com/fwlink/p/?LinkId=825303))

- すべてのオペレーティング システムの .NET Framework 4.6.2 ([Web インストーラー](https://go.microsoft.com/fwlink/?LinkId=780597)または[オフライン インストーラー](https://go.microsoft.com/fwlink/p/?LinkId=780601))

- すべてのオペレーティング システムの .NET Framework 4.6.1 ([Web インストーラー](https://go.microsoft.com/fwlink/?LinkId=671729)または[オフライン インストーラー](https://go.microsoft.com/fwlink/p/?LinkId=671744))

- すべてのオペレーティング システムの .NET Framework 4.6 ([Web インストーラー](https://go.microsoft.com/fwlink/?LinkId=528222)または[オフライン インストーラー](https://go.microsoft.com/fwlink/p/?LinkId=528232))

- すべてのオペレーティング システムの .NET Framework 4.5.2 ([Web インストーラー](https://go.microsoft.com/fwlink/p/?LinkId=397703) または [オフライン インストーラー](https://go.microsoft.com/fwlink/p/?LinkId=397706))

- すべてのオペレーティング システムの .NET Framework 4.5.1 ([Web インストーラー](https://go.microsoft.com/fwlink/p/?LinkId=310158) または [オフライン インストーラー](https://go.microsoft.com/fwlink/p/?LinkId=310159))

- [.NET Framework 4.5](https://go.microsoft.com/fwlink/p/?LinkId=245484)

 重要なメモ:

> [!NOTE]
> ".NET Framework 4.5 とそのポイント リリース" という表記は、.NET Framework 4.5 およびそれ以降のすべてのバージョンを指します。

- .NET Framework 4.5.1 から [!INCLUDE[net_current](../../../includes/net-current-version.md)] までの .NET Framework のバージョンは、.NET Framework 4.5 へのインプレース更新です。つまり、同じバージョンのランタイムを使用しますが、アセンブリのバージョンが更新され、新しい型とメンバーが含まれます。

- .NET Framework 4.5 とそのポイント リリースは、.NET Framework 4 の上にインクリメンタル方式でビルドされます。 .NET Framework 4 がインストールされたシステムに .NET Framework 4.5 またはそのポイント リリースをインストールすると、バージョン 4 のアセンブリが新しいバージョンに置き換えられます。

- アプリで Microsoft [帯域外のパッケージ](../get-started/the-net-framework-and-out-of-band-releases.md) を参照している場合、アセンブリはアプリのパッケージに組み込まれます。

- .NET Framework 4.5 とそのポイント リリースをインストールするには、管理者特権が必要です。

- .NET Framework 4.5 は、Windows 8 と Windows Server 2012 に含まれているため、これらのオペレーティング システムではアプリと一緒に配置する必要はありません。 同様に、.NET Framework 4.5.1 は Windows 8.1 と Windows Server 2012 R2 に含まれます。 .NET Framework 4.5.2 はどのオペレーティング システムにも含まれていません。 .NET Framework 4.6 は Windows 10 に含まれます。 .NET Framework 4.6.1 は Windows 10 November Update に含まれます。 .NET Framework 4.6.2 は Windows 10 Anniversary Update に含まれます。  .NET Framework 4.7 は Windows 10 Creators Update に、.NET Framework 4.7.1 は Windows 10 Fall Creators Update に、.NET Framework 4.7.2 は Windows 10 October 2018 Update と Windows 10 April 2018 Update にそれぞれ含まれます。 .NET Framework 4.8 は Windows 10 May 2019 Update に含まれています。 ハードウェア要件とソフトウェア要件の一覧については、「[システム要件](../get-started/system-requirements.md)」を参照してください。

- .NET Framework 4.5 以降では、ユーザーはセットアップ中に、実行されている .NET Framework アプリケーションの一覧を表示し、簡単に終了できます。 これにより、.NET Framework のインストールによるシステムの再起動を回避できます。 「 [システム再起動の削減](reducing-system-restarts.md)」を参照してください。

- .NET Framework 4.5 またはそのポイント リリースのいずれかをアンインストールすると、前に存在していた .NET Framework 4 ファイルも削除されます。 .NET Framework 4 に戻る場合は、そのバージョンとすべての更新プログラムを再インストールする必要があります。 「[.NET Framework 4 のインストール](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/5a4x27ek(v=vs.100))」を参照してください。

- .NET Framework 4.5 再頒布可能パッケージは、2012 年 10 月 9 に更新されています。この更新により、Microsoft によって生成および署名されたファイルへのデジタル署名が途中で有効期限切れになるという、デジタル証明書の不適切なタイムスタンプに関連する問題が解決しました。 2012 年 8 月 16 日付けの .NET Framework 4.5 再頒布可能パッケージをインストールしていた場合は、 [Microsoft ダウンロード センター](https://go.microsoft.com/fwlink/p/?LinkId=245484)から最新の再頒布可能パッケージを入手して更新を行うことをお勧めします。 この問題について詳しくは、「 [マイクロソフト セキュリティ アドバイザリ (2749655)](https://docs.microsoft.com/security-updates/SecurityAdvisories/2012/2749655)」をご覧ください。

システム管理者が .NET Framework とそのシステムの依存関係をネットワーク経由で配置する方法については、[管理者向け配置ガイド](guide-for-administrators.md)に関するページを参照してください。

## <a name="deployment-options-for-your-app"></a>アプリケーションの配置オプション

ユーザーがアプリケーションをインストールできるように Web サーバーまたは他の一元的な場所にアプリケーションを発行する準備ができたら、複数の配置方法から選択できます。 これらの一部は、Visual Studio に装備されています。 次の表に、アプリケーションの配置オプションの一覧と、各オプションをサポートする .NET Framework 再頒布可能パッケージを示します。 これらに加えて、アプリケーション用のカスタム セットアップ プログラムを作成できます。詳細については、「 [アプリケーションのセットアップへの .NET Framework のインストールのチェーン](#chaining)」を参照してください。

|アプリケーションの配置戦略|使用できる配置方法|使用する .NET Framework 再頒布可能パッケージ|
|--------------------------------------|----------------------------------|-------------------------------------------|
|Web からのインストール|- [InstallAware](#installaware-deployment)<br />- [InstallShield](#installshield-deployment)<br />- [WiX ツールセット](#wix)<br />- [手動インストール](#installing_manually)|[Web installer](#redistributable-packages)|
|ディスクからのインストール|- [InstallAware](#installaware-deployment)<br />- [InstallShield](#installshield-deployment)<br />- [WiX ツールセット](#wix)<br />- [手動インストール](#installing_manually)|[Offline installer](#redistributable-packages)|
|ローカル エリア ネットワークからのインストール (エンタープライズ アプリケーションの場合)|- [ClickOnce](#clickonce-deployment)|[Web インストーラー](#redistributable-packages) (制約については「 [ClickOnce](#clickonce-deployment) 」を参照) または [オフライン インストーラー](#redistributable-packages)|

## <a name="redistributable-packages"></a>頒布可能パッケージ

.NET Framework は、Web インストーラー (ブートストラップ) とオフライン インストーラー (スタンドアロン再頒布可能パッケージ) の 2 種類の再頒布可能パッケージで入手できます。 2 つのパッケージの比較を次の表に示します。

||Web インストーラー|オフライン インストーラー|
|-|-------------------|-----------------------|
|ファイルのダウンロード|.NET Framework 4.8: <br/>[ndp48-web.exe](https://go.microsoft.com/fwlink/?LinkId=2085155)<br/><br/>.NET Framework 4.7.2: <br/>[NDP472-KB4054531-Web.exe](https://go.microsoft.com/fwlink/?LinkId=863262)<br/><br/>.NET Framework 4.7.1: <br/>[NDP471-KB4033344-Web.exe](https://go.microsoft.com/fwlink/?LinkId=852092)<br/><br/>.NET Framework 4.7: <br />[NDP47-KB3186500-Web.exe](https://go.microsoft.com/fwlink/?LinkId=825298) <br /><br />.NET Framework 4.6.2: <br />[NDP462-KB3151802-Web.exe](https://go.microsoft.com/fwlink/?LinkId=780596)<br /><br /> .NET Framework 4.6.1:<br />[NDP461-KB3102438-Web.exe](https://go.microsoft.com/fwlink/?LinkId=671728)<br /><br /> .NET Framework 4.6:<br />[NDP46-KB3045560-Web.exe](https://go.microsoft.com/fwlink/?LinkId=528222)<br /><br /> .NET Framework 4.5.2: <br />[NDP452-KB2901954-Web.exe](https://go.microsoft.com/fwlink/?LinkId=397707)<br /><br /> .NET Framework 4.5.1: <br />[NDP451-KB2859818-Web.exe](https://go.microsoft.com/fwlink/?LinkId=322115)<br /><br /> .NET Framework 4.5: <br />[dotNetFx45_Full_setup.exe](https://go.microsoft.com/fwlink/?LinkId=225704)|.NET Framework 4.8: <br/>[NDP48-x86-x64-AllOS-ENU.exe](https://go.microsoft.com/fwlink/?linkid=2088631)<br/><br/>.NET Framework 4.7.2: <br/>[NDP472-KB4054530-x86-x64-AllOS-ENU.exe](https://go.microsoft.com/fwlink/?LinkId=863265)<br/><br/>.NET Framework 4.7.1: <br />[NDP471-KB4033342-x86-x64-AllOS-ENU.exe](https://go.microsoft.com/fwlink/?LinkId=852104) <br /><br />.NET Framework 4.7: <br />[NDP47-KB3186497-x86-x64-AllOS-ENU.exe](https://go.microsoft.com/fwlink/?LinkId=825302) <br /><br />.NET Framework 4.6.2: <br />[NDP462-KB3151800-x86-x64-AllOS-ENU.exe](https://go.microsoft.com/fwlink/?LinkId=780600)<br /><br /> .NET Framework 4.6.1: <br />[NDP461-KB3102436-x86-x64-AllOS-ENU.exe](https://go.microsoft.com/fwlink/?LinkId=671743)<br /><br /> .NET Framework 4.6: <br />[NDP46-KB3045557-x86-x64-AllOS-ENU.exe](https://go.microsoft.com/fwlink/?LinkId=528232)<br /><br /> .NET Framework 4.5.2: <br />[NDP452-KB2901907-x86-x64-AllOS-ENU.exe](https://go.microsoft.com/fwlink/?LinkId=397708)<br /><br /> .NET Framework 4.5.1: <br />[NDP451-KB2858728-x86-x64-AllOS-ENU.exe](https://go.microsoft.com/fwlink/?LinkId=322116)<br /><br /> .NET Framework 4.5: <br />[dotNetFx45_Full_x86_x64.exe](https://go.microsoft.com/fwlink/?LinkId=225702)|
|インターネット接続の必要性|はい|いいえ|
|ダウンロードのサイズ|小 (ターゲット プラットフォームのインストーラーのみを含む)*|Larger*|
|言語パック|含む**|すべてのオペレーティング システムを対象とするパッケージを使用しない場合は、 [個別にインストールする](#chain_langpack)必要があります|
|配置方法|すべてのメソッドをサポート<br /><br />- [ClickOnce](#clickonce-deployment)<br />- [InstallAware](#installaware-deployment)<br />- [InstallShield](#installshield-deployment)<br />- [Windows インストーラー XML (WiX)](#wix)<br />- [手動インストール](#installing_manually)<br />- [カスタム セットアップ (チェーン)](#chaining)|すべてのメソッドをサポート<br /><br /> - [ClickOnce](#clickonce-deployment)<br />- [InstallAware](#installaware-deployment)<br />- [InstallShield](#installshield-deployment)<br />- [Windows インストーラー XML (WiX)](#wix)<br />- [手動インストール](#installing_manually)<br />- [カスタム セットアップ (チェーン)](#chaining)|
|ClickOnce 配置のダウンロード場所|Microsoft ダウンロード センター:<br /><br /> - [.NET Framework 4.8](https://go.microsoft.com/fwlink/?LinkId=2085155) <br/> - [.NET Framework 4.7.2](https://go.microsoft.com/fwlink/?LinkId=863262) <br/> - [.NET Framework 4.7.1](https://go.microsoft.com/fwlink/?LinkId=852092) <br/> - [.NET Framework 4.7](https://go.microsoft.com/fwlink/?LinkId=825298) <br/> - [.NET Framework 4.6.2](https://go.microsoft.com/fwlink/?LinkId=780596)<br />- [.NET Framework 4.6.1](https://go.microsoft.com/fwlink/?LinkId=671728)<br />- [.NET Framework 4.6](https://go.microsoft.com/fwlink/?LinkId=528222)<br />- [.NET Framework 4.5.2](https://go.microsoft.com/fwlink/?LinkId=397703)<br />- [.NET Framework 4.5.1](https://go.microsoft.com/fwlink/p/?LinkId=310158)<br />- [.NET Framework 4.5](https://go.microsoft.com/fwlink/p/?LinkId=245484)|独自のサーバーまたは Microsoft ダウンロード センター:<br /><br /> - [.NET Framework 4.8](https://go.microsoft.com/fwlink/?linkid=2088631)<br /> - [.NET Framework 4.7.2](https://go.microsoft.com/fwlink/?LinkId=863265)<br /> - [.NET Framework 4.7.1](https://go.microsoft.com/fwlink/?LinkId=852104)<br /> - [.NET Framework 4.7](https://go.microsoft.com/fwlink/?LinkId=825302)<br /> - [.NET Framework 4.6.2](https://go.microsoft.com/fwlink/?LinkId=780600)<br />- [.NET Framework 4.6.1](https://go.microsoft.com/fwlink/?LinkId=671743)<br />- [.NET Framework 4.6](https://go.microsoft.com/fwlink/?LinkId=528232)<br />- [.NET Framework 4.5.2](https://go.microsoft.com/fwlink/p/?LinkId=397706)<br />- [.NET Framework 4.5.1](https://go.microsoft.com/fwlink/p/?LinkId=310159)<br />- [.NET Framework 4.5](https://go.microsoft.com/fwlink/p/?LinkId=245484)|

\* オフライン インストーラーは、すべての対象プラットフォームのコンポーネントを含むため、より大きくなっています。 セットアップの実行が終了すると、Windows オペレーティング システムは使用されたインストーラーのみキャッシュします。 オフライン インストーラーがインストール後に削除されると、使用されるディスク領域は Web インストーラーに使用される領域と同じになります。 アプリのセットアップ プログラムの作成に使用するツール (たとえば、[InstallAware](#installaware-deployment) または [InstallShield](#installshield-deployment)) によって、インストール後に削除されるセットアップ ファイル フォルダーが提供される場合は、オフライン インストーラーをそのセットアップ フォルダー内に配置することで自動的に削除できます。

\*\* カスタム設定の Web インストーラーを使用する場合は、ユーザーの複数言語ユーザー インターフェイス (MUI) 設定に基づいて既定の言語設定を使用するか、コマンド ラインで `/LCID` オプションを使用して別の言語パックを指定できます。 例については、「 [既定の .NET Framework の UI を使用したチェーン](#chaining_default) 」を参照してください。

## <a name="deployment-methods"></a>配置方法

 4 つの配置方法を使用できます。

- .NET Framework の依存関係を設定できます。 これらのメソッドのいずれかを使用して、アプリケーションのインストールで必須コンポーネントとして .NET Framework を指定できます。

  - [ClickOnce 配置](#clickonce-deployment) を使用します (Visual Studio で使用可能)

  - [InstallAware プロジェクト](#installaware-deployment)を作成します (Visual Studio ユーザーが使用できる無償のエディション)

  - [InstallShield プロジェクト](#installshield-deployment) を作成します (Visual Studio で使用可能)

  - [Windows インストーラー XML (WiX) ツール セット](#wix)を使用します。

- [.NET Framework を手動でインストール](#installing_manually)するようにユーザーに依頼できます。

- アプリケーションのセットアップに .NET Framework セットアップ プロセスをチェイン (インクルード) して、.NET Framework のインストール環境をどのように処理するかを決定できます。

  - [既定の UI を使用](#chaining_default)します。 .NET Framework のインストーラーによりインストール環境が提供されます。

  - [UI をカスタマイズ](#chaining_custom) して、一元化されたインストール エクスペリエンスを提供し、.NET Framework のインストールの進行状況を監視します。

これらの配置方法の詳細については、以降のセクションで説明します。

## <a name="setting-a-dependency-on-the-net-framework"></a>.NET Framework の依存関係の設定

アプリケーションの配置に ClickOnce、InstallAware、InstallShield、または WiX を使用した場合、.NET Framework の依存関係を追加して、アプリケーションの一部としてインストールできます。

### <a name="clickonce-deployment"></a>ClickOnce 配置

ClickOnce 配置は、Visual Basic および Visual C# を使用して作成したプロジェクトに使用できますが、Visual C++ には使用できません。

Visual Studio で ClickOnce 配置を選択し、.NET Framework の依存関係を追加するには:

1. 発行するアプリケーション プロジェクトを開きます。

2. ソリューション エクスプローラーで、プロジェクトのショートカット メニューを開き、 **[プロパティ]** を選択します。

3. **[発行]** ペインを選択します。

4. **[必須コンポーネント]** ボタンをクリックします。

5. **[必須コンポーネント]** ダイアログ ボックスの **[必須コンポーネントをインストールするセットアップ プログラムを作成する]** チェック ボックスをオンにします。

6. 必須コンポーネントの一覧で、プロジェクトのビルドに使用した .NET Framework のバージョンを検索して選択します。

7. 必須コンポーネントのソースの場所を指定するオプションを選択し、 **[OK]** をクリックします。

     .NET Framework のダウンロード場所の URL を指定する場合は、Microsoft ダウンロード センター サイトまたは独自のサイトを指定できます。 再頒布可能パッケージを独自のサーバーに配置する場合は、Web インストーラーではなく、オフライン インストーラーを使用する必要があります。 Microsoft ダウンロード センターの Web インストーラーにのみリンクできます。 URL には、独自のアプリケーションを配布する CD を指定することもできます。

8. **[プロパティ ページ]** ダイアログ ボックスの **[OK]** をクリックします。

<a name="installaware"></a>

### <a name="installaware-deployment"></a>InstallAware の配置

InstallAware は、Windows アプリ (APPX)、Windows インストーラー (MSI)、ネイティブ コード (EXE)、および App-V (アプリケーションの仮想化) パッケージを、1 つのソースからビルドします。 必要に応じて[既定のスクリプトを編集](https://www.installaware.com/msicode.htm)してインストールをカスタマイズし、[任意のバージョンの .NET Framework を含める](https://www.installaware.com/one-click-pre-requisite-installer.htm)ことが簡単にできます。 たとえば、InstallAware は Windows 7 に証明書をあらかじめインストールします (これがない場合、.NET Framework 4.7 のセットアップは失敗します)。 InstallAware の詳細については、[Windows インストーラー用 InstallAware](https://www.installaware.com/) の Web サイトをご覧ください。

### <a name="installshield-deployment"></a>InstallShield 配置

Visual Studio で InstallShield 配置を選択し、.NET Framework の依存関係を追加するには:

1. Visual Studio メニュー バーで、 **[ファイル]** 、 **[新規作成]** 、 **[プロジェクト]** の順に選択します。

2. **[新しいプロジェクト]** ダイアログ ボックスの左ペインで、 **[その他のプロジェクトの種類]** 、 **[セットアップと配置]** 、 **[InstallShield LE]** の順に選択します。

3. **[名前]** ボックスにプロジェクト名を入力し、 **[OK]** をクリックします。

4. 初めてセットアップと配置プロジェクトを作成する場合、 **[Go to InstallShield]\(InstallShield に移動\)** または **[InstallShield Limited Edition の有効化]** を選択し、ご使用の Microsoft Visual Studio のバージョンの InstallShield Limited Edition をダウンロードします。 Visual Studio を再起動します。

5. **プロジェクト アシスタント** ウィザードに移動し、 **[アプリケーション ファイル]** をクリックしてプロジェクト出力を追加します。 このウィザードを使用して、他のプロジェクト属性を設定できます。

6. **[インストール要件]** に移動し、オペレーティング システムと、インストールする .NET Framework のバージョンを選択します。

7. セットアップ プロジェクトのショートカット メニューを開き、 **[ビルド]** を選択します。

<a name="wix"></a>

### <a name="windows-installer-xml-wix-deployment"></a>Windows インストーラー XML (WiX) 配置

Windows インストーラー XML (WiX) ツールセットは、XML ソース コードから Windows インストール パッケージをビルドします。 WiX は、MSI と MSM セットアップ パッケージのビルド処理に統合できるコマンド ライン環境をサポートします。 WiX を使用すると、 [.NET Framework を必須コンポーネントとして指定](https://wixtoolset.org/documentation/manual/v3/howtos/redistributables_and_install_checks/install_dotnet.html)するか、 [チェーン元を作成](https://wixtoolset.org/documentation/manual/v3/xsd/wix/exepackage.html) して、.NET Framework の配置操作を完全制御できます。 WiX について詳しくは、「 [Windows インストーラー XML (WiX) ツールセット](https://wixtoolset.org/) 」の Web サイトをご覧ください。

<a name="installing_manually"></a>

## <a name="installing-the-net-framework-manually"></a>.NET Framework の手動インストール

アプリと一緒に .NET Framework を自動的にインストールすることが適切でない場合もあります。 そのような場合は、ユーザーが .NET Framework を手動でインストールできます。 頒布可能パッケージは、 [2 つのパッケージ](#redistributable-packages)で使用できます。 セットアップ プロセスでは、.NET Framework を探す方法とインストールする方法についてユーザーに指示する必要があります。

<a name="chaining"></a>

## <a name="chaining-the-net-framework-installation-to-your-apps-setup"></a>アプリケーションのセットアップへの .NET Framework のインストールのチェーン

アプリケーション用のカスタム セットアップ プログラムを作成する場合、.NET Framework セットアップ プロセスをアプリケーションのセットアップ プロセスにチェーン (インクルード) することができます。 チェーンは、.NET Framework のインストールに次の 2 種類の UI オプションを提供します。

- .NET Framework のインストーラーによって提供される既定の UI を使用します。

- .NET Framework のインストールのカスタム UI を作成して、アプリケーションのセットアップ プログラムとの一貫性を保ちます。

どちらの方法でも、Web インストーラーまたはオフライン インストーラーを使用できます。 各パッケージには長所があります。

- Web インストーラーを使用した場合、.NET Framework セットアップ プロセスが必要なインストール パッケージを判断し、そのパッケージだけを Web サイトからダウンロードしてインストールします。

- オフライン インストーラーを使用すると、再頒布可能メディアに .NET Framework インストール パッケージの完全なセットを入れることができ、ユーザーがセットアップ中に Web から追加ファイルをダウンロードする必要がなくなります。

<a name="chaining_default"></a>

### <a name="chaining-by-using-the-default-net-framework-ui"></a>既定の .NET Framework の UI を使用したチェーン

.NET Framework インストール プロセスをサイレントにチェーンして .NET Framework のインストーラーに UI を提供させるには、セットアップ プログラムに次のコマンドを追加します。

`<.NET Framework redistributable> /q /norestart /ChainingPackage <PackageName>`

たとえば、実行可能プログラムが Contoso.exe で、.NET Framework 4.5 のオフライン再頒布可能パッケージをサイレント インストールする場合は、次のコマンドを使用します。

`dotNetFx45_Full_x86_x64.exe /q /norestart /ChainingPackage Contoso`

追加のコマンド ライン オプションを使用して、インストールをカスタマイズできます。 次に例を示します。

- システムの再起動を最小限に抑えるために、実行中の .NET Framework アプリケーションを終了する方法をユーザーに提供するには、受動モードを設定して、次のように `/showrmui` オプションを使用します。

    `dotNetFx45_Full_x86_x64.exe /norestart /passive /showrmui /ChainingPackage Contoso`

     このコマンドは、.NET Framework をインストールする前に、.NET Framework アプリを終了する機会をユーザーに与えるメッセージ ボックスを、再起動マネージャーが表示できるようにします。

- Web インストーラーを使用する場合、 `/LCID` オプションを使用して言語パックを指定できます。 たとえば、.NET Framework 4.5 Web インストーラーを Contoso セットアップ プログラムにチェーンして日本語の言語パックをインストールするには、次のコマンドをアプリのセットアップ プロセスに追加します。

    `dotNetFx45_Full_setup.exe /q /norestart /ChainingPackage Contoso /LCID 1041`

     `/LCID` オプションを省略すると、セットアップはユーザーの MUI 設定と一致する言語パックをインストールします。

    > [!NOTE]
    > 言語パックのリリース日は、それぞれ異なっている場合があります。 指定した言語パックがダウンロード センターで入手できない場合、セットアップは言語パックなしで .NET Framework をインストールします。 .NET Framework がユーザーのコンピューターに既にインストールされている場合、セットアップは言語パックだけをインストールします。

オプションの完全なリストについては、「 [コマンド ライン オプション](#command-line-options) 」を参照してください。

共通の戻りコードについては、「 [戻りコード](#return-codes) 」を参照してください。

<a name="chaining_custom"></a>

### <a name="chaining-by-using-a-custom-ui"></a>カスタム UI を使用したチェーン

カスタム セットアップ パッケージがある場合、セットアップの進行状況のビューを独自に表示する一方で、.NET Framework のセットアップをサイレントで起動および追跡できます。 この場合は、コードが次をカバーしていることを確認します。

- [.NET Framework のハードウェア要件とソフトウェア要件](../get-started/system-requirements.md)のチェック。

- .NET Framework の正しいバージョンがユーザーのコンピューターに既にインストールされているかどうかの[検出](#detect_net) 。

    > [!IMPORTANT]
    > 正しいバージョンの .NET Framework が既にインストールされているかどうかを判断するには、ターゲット バージョンがインストールされているかどうかではなく、ターゲット バージョン *または* それ以降のバージョンがインストールされているかどうかを確認する必要があります。 言い換えると、レジストリから取得したリリース キーがターゲット バージョンのリリース キーと *同じかどうかを確認するのではなく* 、ターゲット バージョンのリリース キーと同じか、それ以降になっているかどうかを確認する必要があります。

- 言語パックがユーザーのコンピューターに既にインストールされているかどうかの[検出](#detecting-the-language-packs) 。

- 配置を制御する場合は、.NET Framework セットアップ プロセスをサイレントに起動および追跡 (「[方法:.NET Framework 4.5 インストーラーの進行状況を表示する](how-to-get-progress-from-the-dotnet-installer.md)」をご覧ください)。

- オフライン インストーラーを配置する場合は、 [言語パックを個別にチェーンします](#chain_langpack)。

- [コマンド ライン オプション](#command-line-options)を使用した配置のカスタマイズ。 たとえば、.NET Framework Web インストーラーをチェーンして、既定の言語パックをオーバーライドする場合は、前のセクションで説明したように `/LCID` オプションを使用します。

- [トラブルシューティング](#troubleshooting)。

<a name="detect_net"></a>

### <a name="detecting-the-net-framework"></a>.NET Framework の検出

.NET Framework のインストーラーは、インストールが成功するとレジストリ キーを書き込みます。 .NET Framework 4.5 またはそれ以降がインストールされているかどうかは、`Release` という名前の `DWORD` 値のレジストリで `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\NET Framework Setup\NDP\v4\Full` フォルダーを確認することでテストできます。 ("NET Framework セットアップ" の先頭ががピリオドではないことに注意してください)。このキーがある場合は、.NET Framework 4.5 またはそれ以降のバージョンがそのコンピューターにインストールされていることを示しています。 `Release` の値は、インストールされている .NET Framework のバージョンを示します。

> [!IMPORTANT]
> 特定のバージョンが存在するかどうかを検出するには、Release キーワードの値  **以上** の値があるかどうかをチェックする必要があります。

[!INCLUDE[Release key values note](~/includes/version-keys-note.md)]

|Version|Release DWORD の値|
|-------------|--------------------------------|
|Windows 10 May 2019 Update にインストールされた .NET Framework 4.8|528040|
|Windows 10 May 2019 Update 以外のすべての OS バージョンにインストールされた .NET Framework 4.8|528049|
|Windows 10 April 2018 Update および Windows Server バージョン 1803 にインストールされた .NET Framework 4.7.2|461808|
|Windows 10 April 2018 Update および Windows Server バージョン 1803 以外のすべての OS バージョンにインストールされた .NET Framework 4.7.2。 これには、Windows 10 October 2018 Update が含まれます。 |461814|
|Windows 10 Fall Creators Update および Windows Server バージョン 1709 にインストールされた .NET Framework 4.7.1|461308|
|Windows 10 Fall Creators Update および Windows Server バージョン 1709 以外のすべての OS バージョンにインストールされた .NET Framework 4.7.1|461310|
|Windows 10 Creators Update にインストールされた .NET Framework 4.7|460798|
|Windows 10 Creators Update 以外のすべての OS バージョンにインストールされた .NET Framework 4.7|460805|
|Windows 10 Anniversary Edition および Windows Server 2016 にインストールされた .NET Framework 4.6.2|394802|
|Windows 10 Anniversary Edition および Windows Server 2016 以外のすべての OS バージョンにインストールされた .NET Framework 4.6.2|394806|
|Windows 10 November Update にインストールされた .NET Framework 4.6.1|394254|
|Windows 10 November Update 以外のすべての OS バージョンにインストールされた .NET Framework 4.6.1|394271|
|Windows 10 にインストールされた .NET Framework 4.6|393295|
|Windows 10 以外のすべての OS バージョンにインストールされた .NET Framework 4.6|393297|
|.NET Framework 4.5.2|379893|
|Windows 8.1 または Windows Server 2012 R2 でインストールされた .NET Framework 4.5.1|378675|
|Windows 8 と Windows 7 にインストールされた .NET Framework 4.5.1|378758|
|.NET Framework 4.5|378389|

### <a name="detecting-the-language-packs"></a>言語パックの検出

`Release` という名前の DWORD 値のレジストリで HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\NET Framework Setup\NDP\v4\Full\\*LCID* フォルダーをチェックすることにより、特定の言語パックがインストールされているかどうかをテストできます。 ("NET Framework セットアップ" の先頭ががピリオドではないことに注意してください)。*LCID* はロケール識別子を指定します。これらのリストについては、「[サポートされる言語](#supported-languages)」を参照してください。

たとえば、完全な日本語言語パック (LCID=1041) がインストールされているかどうかを検出するには、レジストリから次の名前付きの値を取得します。

| | |
|-|-|
| キー | HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\NET Framework Setup\NDP\v4\Full\1041 |
| name | 解放 |
| 型 | DWORD |

言語パックの最終リリース バージョンがバージョン 4.5 から 4.7.2 までの特定のバージョンの .NET Framework にインストールされているかどうかを確認するには、前のセクション「[.NET Framework の検出](#detect_net)」で説明した Release キー DWORD の値を確認します。

<a name="chain_langpack"></a>

### <a name="chaining-the-language-packs-to-your-app-setup"></a>アプリケーション セットアップへの言語パックのチェーン

.NET Framework には、特定のカルチャにローカライズされたリソースを含むスタンドアロンの言語パックの実行可能ファイルのセットが用意されています。 言語パックは Microsoft ダウンロード センターから入手できます。

- [.NET Framework 4.8 言語パック](https://go.microsoft.com/fwlink/p/?LinkId=2086170)

- [.NET Framework 4.7.2 の言語パック](https://go.microsoft.com/fwlink/?LinkId=863275)

- [.NET Framework 4.7.1 の言語パック](https://go.microsoft.com/fwlink/p/?LinkId=852090)

- [.NET Framework 4.7 の言語パック](https://go.microsoft.com/fwlink/p/?LinkId=825306)

- [.NET Framework 4.6.2 言語パック](https://go.microsoft.com/fwlink/p/?LinkId=780604)

- [.NET Framework 4.6.1 言語パック](https://go.microsoft.com/fwlink/p/?LinkId=671747)

- [.NET Framework 4.6 言語パック](https://go.microsoft.com/fwlink/p/?LinkId=528314)

- [.NET Framework 4.5.2 言語パック](https://go.microsoft.com/fwlink/p/?LinkId=397701)

- [.NET Framework 4.5.1 言語パック](https://go.microsoft.com/fwlink/p/?LinkId=322101)

- [.NET Framework 4.5 の言語パック](https://go.microsoft.com/fwlink/p/?LinkId=245451)

> [!IMPORTANT]
> 言語パックには、アプリの実行に必要な .NET Framework コンポーネントは含まれていません。言語パックをインストールする前に、Web インストーラーまたはオフラインのインストーラーを使用して .NET Framework をインストールする必要があります。

.NET Framework 4.5.1 以降では、パッケージ名の形式は NDP<`version`>-KB<`number`>-x86-x64-AllOS-<`culture`>.exe になります。`version` は .NET Framework のバージョン番号です。`number` は Microsoft サポート情報記事番号です。`culture` は[国/地域](#supported-languages)です。 これらのパッケージの一例は、 `NDP452-KB2901907-x86-x64-AllOS-JPN.exe`です。 パッケージ名はこの記事の既出の [Redistributable Packages](#redistributable-packages) セクションに記載されています。

.NET Framework のオフライン インストーラーを言語パックと一緒にインストールするには、言語パックをアプリのセットアップにチェーンする必要があります。 たとえば、.NET Framework 4.5.1 のオフライン インストーラーを日本語言語パックと一緒に配置するには、次のコマンドを使用します。

`NDP451-KB2858728-x86-x64-AllOS-JPN.exe /q /norestart /ChainingPackage <ProductName>`

Web インストーラーを使用する場合は、言語パックをチェーンする必要はありません。セットアップはユーザーの MUI 設定と一致する言語パックをインストールします。 異なる言語をインストールするには、 `/LCID` オプションを使用して言語パックを指定します。

コマンド ライン オプションの完全なリストについては、「 [コマンド ライン オプション](#command-line-options) 」を参照してください。

### <a name="troubleshooting"></a>トラブルシューティング

#### <a name="return-codes"></a>戻りコード

次の表は、.NET Framework の再頒布可能インストーラーから返される最も一般的なリターン コードを示しています。 これらのリターン コードは、すべてのバージョンのインストーラーで共通です。 詳細情報へのリンクについては、次のセクションを参照してください。

|リターン コード|説明|
|-----------------|-----------------|
|0|インストールは正常に終了しました。|
|1602|ユーザーがインストールをキャンセルしました。|
|1603|インストール中に致命的なエラーが発生しました。|
|1641|インストールを完了するには再起動する必要があります。 このメッセージが表示された場合、操作は成功しました。|
|3010|インストールを完了するには再起動する必要があります。 このメッセージが表示された場合、操作は成功しました。|
|5100|ユーザーのコンピューターは、システム要件を満たしていません。|

#### <a name="download-error-codes"></a>ダウンロードのエラー コード

次のコンテンツをご覧ください。

- [Background Intelligent Transfer Service (BITS) のエラー コード](https://go.microsoft.com/fwlink/?LinkId=180946)

- [URL モニカーのエラー コード](https://go.microsoft.com/fwlink/?LinkId=180947)

- [WinHttp エラー コード](https://go.microsoft.com/fwlink/?LinkId=180948)

#### <a name="other-error-codes"></a>その他のエラー コード

次のコンテンツをご覧ください。

- [Windows インストーラーのエラー コード](https://go.microsoft.com/fwlink/?LinkId=180949)

- [Windows Update エージェントの結果コード](https://go.microsoft.com/fwlink/?LinkId=180951)

## <a name="uninstalling-the-net-framework"></a>.NET Framework のアンインストール

Windows 8 以降、コントロール パネルの **[Windows の機能の有効化または無効化]** を使用して、.NET Framework 4.5 またはそのポイント リリースの 1 つをアンインストールできます。 Windows の旧バージョンでは、コントロール パネルの **[プログラムの追加と削除]** を使用して .NET Framework 4.5 またはそのポイントリリースの 1 つをアンインストールできます。

> [!IMPORTANT]
> Windows 7 およびそれ以前のオペレーティング システムでは、.NET Framework 4.5.1、4.5.2、4.6、4.6.1、4.6.2、4.7、4.7.1、4.7.2、または 4.8 をアンインストールしても .NET Framework 4.5 のファイルは復元されず、.NET Framework 4.5 をアンインストールしても .NET Framework 4 のファイルは復元されません。 旧バージョンに戻る場合は、更新プログラムと共に再インストールする必要があります。

## <a name="appendix"></a>付録

### <a name="command-line-options"></a>コマンド ライン オプション

次の表では、アプリケーションのセットアップに .NET Framework 4.5 の再頒布可能パッケージをチェーンするときに指定できるオプションを示します。

|オプション|説明|
|------------|-----------------|
|**/CEIPConsent**|既定の動作を上書きし、今後の配置操作を改良するための匿名のフィードバックを Microsoft に送信します。 このオプションは、セットアップ プログラムで同意メッセージが表示され、ユーザーが匿名のフィードバックを Microsoft に送信することを許可した場合のみ使用できます。|
|**/chainingpackage** `packageName`|チェーンを行っている実行可能ファイルの名前を指定します。 この情報は、今後の配置操作を改良するための匿名のフィードバックとして Microsoft に送信されます。<br /><br /> パッケージ名にスペースが含まれている場合は、区切り記号として二重引用符を使用します (例: **/chainingpackage "Lucerne Publishing"** )。 チェーン パッケージの例については、MSDN ライブラリの「 [インストール パッケージからの進行状況に関する情報の取得](https://go.microsoft.com/fwlink/?LinkId=181926) 」をご覧ください。|
|**/LCID**  `LCID`<br /><br /> `LCID` はロケール識別子を指定します (「 [サポートされる言語](#supported-languages)」を参照してください)。|`LCID` によって指定された言語パックをインストールし、クワイエット モードが設定されていない限り表示される UI をその言語で表示します。<br /><br /> Web インストーラーでは、このオプションは、Web から言語パッケージをチェーンしてインストールします。 **注:** このオプションは Web インストーラーだけに使用します。|
|**/log** `file` &#124; `folder`|ログ ファイルの場所を指定します。 既定ではプロセスの一時フォルダーになっており、既定のファイル名はパッケージに基づきます。 ファイル拡張子が .txt の場合、テキスト ログが生成されます。 他の拡張子を指定するか、拡張子がないと、HTML ログが作成されます。|
|**/msioptions**|.msi と .msp の項目に渡されるオプションを指定します。例: `/msioptions "PROPERTY1='Value'"`|
|**/norestart**|セットアップ プログラムが自動的に再起動しないようにします。 このオプションを使用する場合、チェーン アプリがリターン コードをキャプチャし、再起動を処理する必要があります (MSDN ライブラリの「 [インストール パッケージからの進行状況に関する情報の取得](https://go.microsoft.com/fwlink/?LinkId=179606) 」をご覧ください)。|
|**/passive**|受動モードを設定します。 インストールが進行中であることを示す進行状況バーを表示しますが、ユーザーに対してプロンプトやエラー メッセージは表示しません。 このモードでは、セットアップ プログラムによってチェーンされたときに、チェーン パッケージが [リターン コード](#return-codes)を処理する必要があります。|
|**/pipe**|チェーン パッケージが進行状況を取得できるように通信チャネルを作成します。|
|**/promptrestart**|受動モードのみ、セットアップ プログラムの再起動が必要な場合は、ユーザーに対してメッセージが表示されます。 このオプションでは、再起動が必要な場合はユーザーの操作を必要とします。|
|**/q**|クワイエット モードを設定します。|
|**/repair**|修復機能をトリガーします。|
|**/serialdownload**|パッケージをダウンロードした後にのみインストールを強制します。|
|**/showfinalerror**|受動モードを設定します。 インストールが失敗した場合にのみ、エラーを表示します。 このオプションは、インストールが失敗した場合はユーザーの操作を必要とします。|
|**/showrmui**|**/passive** オプションでのみ使用します。 ユーザーに、現在実行されている .NET Framework アプリケーションを閉じるように求めるメッセージ ボックスを表示します。 このメッセージ ボックスの動作は受動モードでも非受動モードでも同じです。|
|**/uninstall**|.NET Framework 再頒布可能パッケージのアンインストール|

### <a name="supported-languages"></a>サポートされる言語

.NET Framework 4.5 とそのポイント リリースで使用可能な .NET Framework 言語パックを次の表に示します。

|LCID|言語 - 国/地域|culture|
|----------|--------------------------------|-------------|
|1025|アラビア語 - サウジアラビア|ar|
|1028|中国語 - 繁体字|zh-Hant|
|1029|チェコ語|cs|
|1030|デンマーク語|da|
|1031|ドイツ語 – ドイツ|de|
|1032|ギリシャ語|el|
|1035|フィンランド語|fi|
|1036|フランス語 - フランス|fr|
|1037|ヘブライ語|he|
|1038|ハンガリー語|hu|
|1040|イタリア語 - イタリア|it|
|1041|日本語|ja|
|1042|韓国語|ko|
|1043|オランダ語 - オランダ|nl|
|1044|ノルウェー語 - ブークモール|Ｘ|
|1045|ポーランド語|pl|
|1046|ポルトガル語 - ブラジル|pt-BR|
|1049|ロシア語|ru|
|1053|スウェーデン語|sv|
|1055|トルコ語|tr|
|2052|中国語 - 簡体字|zh-Hans|
|2070|ポルトガル語 - ポルトガル|pt-PT|
|3082|スペイン語 (スペイン、モダン ソート)|es|

## <a name="see-also"></a>関連項目

- [配置ガイド (管理者向け)](guide-for-administrators.md)
- [システム要件](../get-started/system-requirements.md)
- [開発者向けの .NET Framework のインストール](../install/guide-for-developers.md)
- [.NET Framework のインストールおよびアンインストールのブロックのトラブルシューティング](../install/troubleshoot-blocked-installations-and-uninstallations.md)
- [.NET Framework 4.5 のインストール中のシステム再起動の削減](reducing-system-restarts.md)
- [方法: .NET Framework 4.5 インストーラーの進行状況を表示する](how-to-get-progress-from-the-dotnet-installer.md)
