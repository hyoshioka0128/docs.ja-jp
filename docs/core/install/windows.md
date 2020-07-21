---
title: Windows に .NET Core をインストールする
description: .NET Core をインストールできる Windows のバージョンについて説明します。
author: adegeo
ms.author: adegeo
ms.date: 06/22/2020
ms.openlocfilehash: e26494de7e9246b241cb965d8d735a781aab5478
ms.sourcegitcommit: c23d9666ec75b91741da43ee3d91c317d68c7327
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85804456"
---
# <a name="install-net-core-on-windows"></a>Windows に .NET Core をインストールする

> [!div class="op_single_selector"]
>
> - [Windows へのインストール](windows.md)
> - [macOS へのインストール](macos.md)
> - [Linux へのインストール](linux.md)

この記事では、Windows に .NET Core をインストールする方法について説明します。 .NET Core は、ランタイムと SDK で構成されています。 ランタイムは .NET Core アプリを実行するために使用され、アプリに含まれている場合と含まれていない場合があります。 SDK は、.NET Core アプリとライブラリの作成に使用されます。 .NET Core ランタイムは、常に SDK と共にインストールされます。

.NET Core の最新バージョンは 3.1 です。

[.NET Core をダウンロードする。](https://dotnet.microsoft.com/download/dotnet-core)

## <a name="supported-releases"></a>サポートされているリリース

次の表に、現在サポートされている .NET Core リリースと、それらがサポートされている Windows のバージョンの一覧を示します。 これらのバージョンは、[.NET Core のバージョンがサポート終了](https://dotnet.microsoft.com/platform/support/policy/dotnet-core)するか、[Windows のバージョンの有効期限が切れるまで](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet)サポートされます。

Windows 10 のバージョンのサービス終了日は、エディションごとに分かれています。 次の表では、**Home**、**Pro**、**Pro Education**、**Pro for Workstations** の各エディションだけが考慮されています。 具体的な詳細については、「[Windows ライフサイクルのファクト シート](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet)」を確認してください。

- ✔️ は、Windows または .NET Core のバージョンがまだサポートされていることを示します。
- ❌ は、Windows または .NET Core のバージョンがその Windows のリリースではサポートされていないことを示しています。
- Windows のバージョンと .NET Core のバージョンの両方に ✔️ が付いている場合、その OS と .NET の組み合わせはサポートされています。

| オペレーティング システム                      | .NET Core 2.1 | .NET Core 3.1 | .NET 5 Preview |
|-----------------------------|---------------|---------------|----------------|
| ✔️ Windows 10 バージョン 2004 | ✔️ 2.1        | ✔️ 3.1        | ✔️ 5.0 Preview |
| ✔️ Windows 10 バージョン 1909 | ✔️ 2.1        | ✔️ 3.1        | ✔️ 5.0 Preview |
| ✔️ Windows 10 バージョン 1903 | ✔️ 2.1        | ✔️ 3.1        | ✔️ 5.0 Preview |
| ✔️ Windows 10 バージョン 1809 | ✔️ 2.1        | ✔️ 3.1        | ✔️ 5.0 Preview |
| ❌ Windows 10 バージョン 1803 | ✔️ 2.1        | ❌ 3.1        | ❌ 5.0 Preview |
| ❌ Windows 10 バージョン 1709 | ❌ 2.1        | ❌ 3.1        | ❌ 5.0 Preview |
| ❌ Windows 10 バージョン 1703 | ❌ 2.1        | ❌ 3.1        | ❌ 5.0 Preview |
| ❌ Windows 10 バージョン 1607 | ❌ 2.1        | ❌ 3.1        | ❌ 5.0 Preview |
| ❌ Windows 10 バージョン 1511 | ❌ 2.1        | ❌ 3.1        | ❌ 5.0 Preview |
| ❌ Windows 10 バージョン 1507 | ❌ 2.1        | ❌ 3.1        | ❌ 5.0 Preview |

## <a name="unsupported-releases"></a>サポートされていないリリース

次のバージョンの .NET Core は ❌ サポート対象外となりました。 これらのダウンロードは、まだ公開されています。

- 3.0
- 2.2
- 2.0

## <a name="runtime-information"></a>ランタイムに関する情報

ランタイムは、.NET Core で作成されたアプリを実行するために使用されます。 アプリの作成者は、アプリを公開するとき、アプリにランタイムを含めることができます。 ランタイムが含まれていない場合は、ユーザーがランタイムをインストールする必要があります。

Windows には、3 つの異なるランタイムをインストールできます。

*ASP.NET Core ランタイム*\
ASP.NET Core アプリを実行します。 .NET Core ランタイムが含まれます。

*Desktop ランタイム*\
Windows 用の .NET Core WPF デスクトップ アプリおよび .NET Core Windows フォーム デスクトップ アプリを実行します。 .NET Core ランタイムが含まれます。

*.NET Core ランタイム*\
このランタイムは最も単純なランタイムであり、他のランタイムは含まれていません。 .NET Core アプリとの互換性を最善にするには、"*ASP.NET Core ランタイム*" と "*Desktop ランタイム*" の両方をインストールすることを強くお勧めします。

[.NET Core ランタイムをダウンロードする。](https://dotnet.microsoft.com/download/dotnet-core)

## <a name="sdk-information"></a>SDK に関する情報

SDK は、.NET Core アプリとライブラリを作成して公開するために使用されます。 SDK のインストールには、次の 3 つの[ランタイム](#runtime-information)が含まれます: ASP.NET Core、Desktop、.NET Core。

[.NET Core SDK をダウンロードする。](https://dotnet.microsoft.com/download/dotnet-core)

## <a name="dependencies"></a>依存関係

<!-- markdownlint-disable MD025 -->
<!-- markdownlint-disable MD024 -->

# <a name="net-core-31"></a>[.NET Core 3.1](#tab/netcore31)

.NET Core 3.1 では以下の Windows のバージョンがサポートされます。

> [!NOTE]
> `+` 記号は、最小バージョンを表します。

| OS                            | バージョン                        | アーキテクチャ   |
| ----------------------------- | ------------------------------ | --------------- |
| Windows クライアント                | 8.1                            | x64、x86        |
| Windows 10 クライアント             | バージョン 1609+                  | x64、x86        |
| Windows Server                | 2012 R2+                       | x64、x86        |
| Nano Server                   | バージョン 1803+                  | x64、ARM32      |

.NET Core 3.1 でサポートされているオペレーティング システム、ディストリビューション、ライフサイクル ポリシーの詳細については、「[.NET Core 3.1 Supported OS Versions](https://github.com/dotnet/core/blob/master/release-notes/3.1/3.1-supported-os.md)」(.NET Core 3.1 でサポートされている OS バージョン) を参照してください。

# <a name="net-core-30"></a>[.NET Core 3.0](#tab/netcore30)

" *.NET Core 3.0 は現在サポートされていません。詳細については、「[.NET Core のサポート ポリシー](https://dotnet.microsoft.com/platform/support/policy/dotnet-core)」をご覧ください。* "

.NET Core 3.0 では以下の Windows のバージョンがサポートされます。

> [!NOTE]
> `+` 記号は、最小バージョンを表します。

| OS                            | バージョン                        | アーキテクチャ   |
| ----------------------------- | ------------------------------ | --------------- |
| Windows クライアント                | 7 SP1+、8.1                    | x64、x86        |
| Windows 10 クライアント             | バージョン 1607+                  | x64、x86        |
| Windows Server                | 2012 R2+                       | x64、x86        |
| Nano Server                   | バージョン 1803+                  | x64、ARM32      |

.NET Core 3.0 でサポートされているオペレーティング システム、ディストリビューション、ライフサイクル ポリシーの詳細については、「[.NET Core 3.0 Supported OS Versions](https://github.com/dotnet/core/blob/master/release-notes/3.0/3.0-supported-os.md)」(.NET Core 3.0 でサポートされている OS バージョン) を参照してください。

# <a name="net-core-22"></a>[.NET Core 2.2](#tab/netcore22)

" *.NET Core 2.2 は現在サポートされていません。詳細については、「[.NET Core のサポート ポリシー](https://dotnet.microsoft.com/platform/support/policy/dotnet-core)」をご覧ください。* "

.NET Core 2.2 では以下の Windows のバージョンがサポートされます。

> [!NOTE]
> `+` 記号は、最小バージョンを表します。

| OS                            | バージョン                        | アーキテクチャ   |
| ----------------------------- | ------------------------------ | --------------- |
| Windows クライアント                | 7 SP1+、8.1                    | x64、x86        |
| Windows 10 クライアント             | バージョン 1607+                  | x64、x86        |
| Windows Server                | 2008 R2 SP1+                   | x64、x86        |
| Nano Server                   | バージョン 1803+                   | x64、ARM32      |

.NET Core 2.2 でサポートされているオペレーティング システム、ディストリビューション、ライフサイクル ポリシーの詳細については、「[.NET Core 2.2 Supported OS Versions](https://github.com/dotnet/core/blob/master/release-notes/2.2/2.2-supported-os.md)」(.NET Core 2.2 でサポートされている OS バージョン) を参照してください。

# <a name="net-core-21"></a>[.NET Core 2.1](#tab/netcore21)

.NET Core 2.1 では以下の Windows のバージョンがサポートされます。

> [!NOTE]
> `+` 記号は、最小バージョンを表します。

| OS                            | バージョン                        | アーキテクチャ   |
| ----------------------------- | ------------------------------ | --------------- |
| Windows クライアント                | 7 SP1+、8.1                    | x64、x86        |
| Windows 10 クライアント             | バージョン 1607+                  | x64、x86        |
| Windows Server                | 2008 R2 SP1+                   | x64、x86        |
| Nano Server                   | バージョン 1803+                  | x64、            |

.NET Core 2.1 でサポートされているオペレーティング システム、ディストリビューション、ライフサイクル ポリシーの詳細については、「[.NET Core 2.1 Supported OS Versions](https://github.com/dotnet/core/blob/master/release-notes/2.1/2.1-supported-os.md)」(.NET Core 2.1 でサポートされている OS バージョン) を参照してください。

---

<!-- markdownlint-disable MD001 -->

### <a name="windows-7--vista--81--server-2008-r2--server-2012-r2"></a><a name="additional-deps"></a> Windows 7 / Vista / 8.1 / Server 2008 R2 / Server 2012 R2

次の Windows のバージョンに .NET SDK またはランタイムをインストールする場合は、追加の依存関係が必要です。

- ❌ Windows 7 SP1
- ❌ Windows Vista SP 2
- ✔️ Windows 8.1
- ✔️ Windows Server 2008 R2
- ✔️ Windows Server 2012 R2

以下をインストールします。

- [Microsoft Visual C++ 2015 再頒布可能パッケージ Update 3](https://www.microsoft.com/download/details.aspx?id=52685)。
- [KB2533623](https://support.microsoft.com/help/2533623/microsoft-security-advisory-insecure-library-loading-could-allow-remot)

上記の要件は、次のいずれかのエラーが発生した場合にも必要です。

> お使いのコンピューターに *api-ms-win-crt-runtime-l1-1-0.dll* が見つからず、プログラムを開始できない。 この問題を解決するには、プログラムを再インストールしてください。
>
> \- または
>
> お使いのコンピューターに *api-ms-win-cor-timezone-l1-1-0.dll* が見つからず、プログラムを開始できない。 この問題を解決するには、プログラムを再インストールしてください。
>
> \- または
>
> ライブラリ *hostfxr.dll* は見つかったが、その *C:\\\<path_to_app>\\hostfxr.dll* からの読み込みに失敗した。

## <a name="install-with-powershell-automation"></a>PowerShell オートメーションを使用してインストールする

[dotnet-install スクリプト](../tools/dotnet-install-script.md)は、ランタイムの CI 自動化および管理者以外によるインストールに使用されます。 スクリプトは、[dotnet-install スクリプト参照ページ](../tools/dotnet-install-script.md)からダウンロードできます。

スクリプトでは、既定で最新の [長期サポート (LTS)](https://dotnet.microsoft.com/platform/support/policy/dotnet-core) バージョン (.NET Core 3.1) がインストールされます。 `Channel` スイッチを指定することで、特定のリリースを選択できます。 ランタイムをインストールするには、`Runtime` スイッチを含めます。 それ以外の場合は、スクリプトによって [SDK](sdk.md) がインストールされます。

```powershell
dotnet-install.ps1 -Channel 3.1 -Runtime aspnetcore
```

`-Runtime` スイッチを省略して SDK をインストールします。 この例では、`-Channel` スイッチが `Current` に設定されているため、サポートされている最新バージョンがインストールされます。

```powershell
dotnet-install.ps1 -Channel Current
```

## <a name="install-with-visual-studio"></a>Visual Studio を使用してインストールする

次の表では、Visual Studio を使用して .NET Core アプリを開発している場合に、ターゲットの .NET Core SDK バージョンに基づいて最低限必要な Visual Studio のバージョンを説明します。

| .NET Core SDK のバージョン | Visual Studio のバージョン                      |
| --------------------- | ------------------------------------------ |
| 3.1                   | Visual Studio 2019 バージョン 16.4 以降。 |
| 3.0                   | Visual Studio 2019 バージョン 16.3 以降。 |
| 2.2                   | Visual Studio 2017 バージョン 15.9 以降。 |
| 2.1                   | Visual Studio 2017 バージョン 15.7 以降。 |

Visual Studio を既にインストールしてある場合は、次の手順でバージョンを確認できます。

01. Visual Studio を開きます。
01. **[ヘルプ]**  >  **[Microsoft Visual Studio のバージョン情報]** を選択します。
01. **[バージョン情報]** ダイアログで、バージョン番号を確認します。

Visual Studio では、最新の .NET Core SDK とランタイムをインストールできます。

- [Visual Studio をダウンロードします](https://www.visualstudio.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2019)。

### <a name="select-a-workload"></a>ワークロードを選択する

Visual Studio をインストールまたは変更するときは、ビルドするアプリケーションの種類に応じて、次の 1 つ以上のワークロードを選択します。

- **[他のツールセット]** セクションの **[.NET Core クロスプラットフォームの開発]** ワークロード。
- **[Web クラウド]** セクションの **[ASP.NET と Web 開発]** ワークロード。
- **[Web クラウド]** セクションの **[Azure の開発]** ワークロード。
- **[デスクトップとモバイル]** セクションの **[.NET デスクトップ開発]** ワークロード。

[![Windows Visual Studio 2019 と .NET Core ワークロード](media/install-sdk/windows-install-visual-studio-2019.png)](media/install-sdk/windows-install-visual-studio-2019.png#lightbox)

## <a name="install-alongside-visual-studio-code"></a>Visual Studio Code と共にインストールする

Visual Studio Code は、デスクトップ上で動作する強力で軽量なソース コード エディターです。 Visual Studio Code は、Windows、macOS、Linux で利用できます。

Visual Studio Code には、Visual Studio のような自動化された .NET Core インストーラーは付属していませんが、.NET Core のサポートを簡単に追加できます。

01. [Visual Studio Code をダウンロードしてインストールします](https://code.visualstudio.com/Download)。
01. [.NET Core SDK をダウンロードしてインストールします](https://dotnet.microsoft.com/download/dotnet-core)。
01. [Visual Studio Code マーケットプレースから C# 拡張機能をインストールします](https://marketplace.visualstudio.com/items?itemName=ms-dotnettools.csharp)。

## <a name="download-and-manually-install"></a>手動でダウンロードしてインストールする

.NET Core 用 Windows インストーラーの代わりに、SDK またはランタイムをダウンロードして手動でインストールすることもできます。 手動インストールは、通常、継続的インテグレーション テストの一環として実行されます。 開発者またはユーザーの場合、通常は[インストーラー](https://dotnet.microsoft.com/download/dotnet-core)を使用することをお勧めします。

.NET Core SDK と .NET Core ランタイムはどちらも、ダウンロード後に手動でインストールできます。 .NET Core SDK をインストールする場合、対応するランタイムをインストールする必要はありません。 まず、次のいずれかのサイトから SDK またはランタイムのバイナリ リリースをダウンロードします。

- ✔️ [.NET 5.0 preview のダウンロード](https://dotnet.microsoft.com/download/dotnet/5.0)
- ✔️ [.NET Core 3.1 のダウンロード](https://dotnet.microsoft.com/download/dotnet-core/3.1)
- ✔️ [.NET Core 2.1 のダウンロード](https://dotnet.microsoft.com/download/dotnet-core/2.1)
- [すべての .NET Core のダウンロード](https://dotnet.microsoft.com/download/dotnet-core)

.NET を抽出するためのディレクトリを作成します (`%USERPROFILE%\dotnet` など)。 次に、ダウンロードした zip ファイルをそのディレクトリに抽出します。

既定では、.NET Core CLI コマンドおよびアプリでは、この方法でインストールされた .NET Core は使用されません。使用することを明示的に選択する必要があります。 これを行うには、アプリケーションの起動に使用する環境変数を変更します。

```console
set DOTNET_ROOT=%USERPROFILE%\dotnet
set PATH=%USERPROFILE%\dotnet;%PATH%
set DOTNET_MULTILEVEL_LOOKUP=0
```

この方法では、複数のバージョンを別々の場所にインストールして、その場所を参照する環境変数を使ってアプリケーションを実行することで、アプリケーションによって使用されるインストール場所を明示的に選択できます。

`DOTNET_MULTILEVEL_LOOKUP` が `0` に設定されている場合、.NET Core ではグローバルにインストールされている .NET Core のバージョンは無視されます。 .NET Core で、アプリケーションを実行するための最適なフレームワークを選択するときに、既定のグローバル インストールの場所が考慮されるようにするには、その環境設定を削除します。 通常、既定値は `C:\Program Files\dotnet` です。これは、インストーラーによって .NET Core がインストールされる場所です。

## <a name="docker"></a>Docker

コンテナーを使用すると、アプリケーションをホスト システムの他の部分から簡単に分離できます。 同じコンピューター上のコンテナーでは、カーネルだけが共有され、アプリケーションに提供されたリソースが使用されます。

.NET Core は Docker コンテナー内で実行できます。 公式の .NET Core Docker イメージは Microsoft Container Registry (MCR) に公開され、[Microsoft .NET Core の Docker Hub リポジトリ](https://hub.docker.com/_/microsoft-dotnet-core/)で見つけられます。 各リポジトリには、.NET (SDK またはランタイム) と自分が使用できる OS のさまざまな組み合わせのイメージが含まれています。

Microsoft は、特定のシナリオに対応したイメージを用意しています。 たとえば、[ASP.NET Core リポジトリ](https://hub.docker.com/_/microsoft-dotnet-core-aspnet/)には、運用環境での ASP.NET Core アプリの実行用にビルドされたイメージが用意されています。

Docker コンテナー内で .NET Core を使用する方法の詳細については、「[.NET および Docker の概要](../docker/introduction.md)」と[サンプル](https://github.com/dotnet/dotnet-docker/blob/master/samples/README.md)に関するページを参照してください。

## <a name="next-steps"></a>次の手順

- [.NET Core が既にインストールされているかどうかを確認する方法](how-to-detect-installed-versions.md?pivots=os-windows)。
- [チュートリアル: Hello World チュートリアル](../tutorials/with-visual-studio.md)。
- [チュートリアル: Visual Studio Code を使用して新しいアプリを作成する](../tutorials/with-visual-studio-code.md)。
- [チュートリアル: NET Core アプリをコンテナー化する](../docker/build-container.md)。
