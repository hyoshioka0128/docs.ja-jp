---
title: Windows、Linux、および macOS に .NET Core SDK をインストールする - .NET Core
description: Windows、Linux、および macOS に .NET Core をインストールする方法について説明します。 .NET Core アプリの開発に必要な依存関係を確認します。
author: thraka
ms.author: adegeo
ms.date: 12/04/2019
ms.custom: updateeachrelease
zone_pivot_groups: operating-systems-set-one
ms.openlocfilehash: 1f7efaedaa1a0be90f7b619f954bdf78eecafa07
ms.sourcegitcommit: 42ed59871db1f29a32b3d8e7abeb20e6eceeda7c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/10/2019
ms.locfileid: "74999063"
---
# <a name="install-the-net-core-sdk"></a>.NET Core SDK をインストールする

この記事では、.NET Core SDK をインストールする方法について説明します。 .NET Core SDK は、.NET Core アプリとライブラリの作成に使用されます。 .NET Core ランタイムは、常に SDK と共にインストールされます。

::: zone pivot="os-windows"

## <a name="install-with-an-installer"></a>インストーラーを使用してインストールする

Windows には、.NET Core 3.1 SDK のインストールに使用できるスタンドアロン インストーラーが用意されています。

- [x64 (64 ビット) CPU](https://dotnet.microsoft.com/download/dotnet-core/3.1)
- [x86 (32 ビット) CPU](https://dotnet.microsoft.com/download/dotnet-core/3.1)

::: zone-end

::: zone pivot="os-macos"

## <a name="install-with-an-installer"></a>インストーラーを使用してインストールする

macOS には、.NET Core 3.1 SDK のインストールに使用できるスタンドアロン インストーラーが用意されています。

- [x64 (64 ビット) CPU](https://dotnet.microsoft.com/download/dotnet-core/3.1)

::: zone-end

::: zone pivot="os-linux"

## <a name="install-with-a-package-manager"></a>パッケージ マネージャーを使用してインストールする

多くの一般的な Linux パッケージ マネージャーを使用して、.NET Core SDK をインストールできます。 詳細については、[Linux パッケージ マネージャー - .NET Core のインストール](linux-package-managers.md)に関するページを参照してください。

## <a name="download-and-manually-install"></a>手動でダウンロードしてインストールする

SDK を抽出し、コマンドをターミナルで使用できるようにするには、最初に .NET Core のバイナリ リリースを[ダウンロード](#all-net-core-downloads)します。 次に、ターミナルを開き、以下のコマンドを実行します。

```bash
mkdir -p $HOME/dotnet && tar zxf dotnet-sdk-3.1.100-linux-x64.tar.gz -C $HOME/dotnet
export DOTNET_ROOT=$HOME/dotnet
export PATH=$PATH:$HOME/dotnet
```

> [!TIP]
> 上記のコマンドでは、それを実行したターミナル セッションでのみ、.NET SDK コマンドを使用できるようになります。
>
> シェル プロファイルを編集して、コマンドを永続的に追加することができます。 Linux ではさまざまなシェルを使用でき、それぞれに異なるプロファイルがあります。 次に例を示します。
>
> - **Bash シェル**: *~/.bash_profile*、 *~/.bashrc*
> - **Korn シェル**: *~/.kshrc* または *.profile*
> - **Z シェル**: *~/.zshrc* または *.zprofile*
> 
> シェルの適切なソース ファイルを編集し、既存の `PATH` ステートメントの末尾に `:$HOME/dotnet` を追加します。 `PATH` ステートメントが含まれていない場合は、`export PATH=$PATH:$HOME/dotnet` を含む新しい行を追加します。
>
> また、ファイルの末尾に `export DOTNET_ROOT=$HOME/dotnet` を追加します。

::: zone-end

::: zone pivot="os-windows"

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

Visual Studio をインストールまたは変更するときは、ビルドするアプリケーションの種類に応じて、次のいずれかのワークロードを選択します。

- **[他のツールセット]** セクションの **[.NET Core クロスプラットフォームの開発]** ワークロード。
- **[Web クラウド]** セクションの **[ASP.NET と Web 開発]** ワークロード。
- **[Web クラウド]** セクションの **[Azure の開発]** ワークロード。
- **[デスクトップとモバイル]** セクションの **[.NET デスクトップ開発]** ワークロード。

[![Windows Visual Studio 2019 と .NET Core ワークロード](media/install-sdk/windows-install-visual-studio-2019.png)](media/install-sdk/windows-install-visual-studio-2019.png#lightbox)

::: zone-end

::: zone pivot="os-macos"

## <a name="install-with-visual-studio-for-mac"></a>Visual Studio for Mac を使用してインストールする

Visual Studio for Mac では、 **[.NET Core]** ワークロードを選択すると、.NET Core SDK がインストールされます。 macOS で .NET Core の開発を始めるには、「[Visual Studio 2019 for Mac をインストールする](/visualstudio/mac/installation)」を参照してください。 最新リリースである .NET Core 3.1 の場合は、Visual Studio for Mac 8.4 Preview を使用する必要があります。

[![macOS Visual Studio 2019 for Mac と .NET Core ワークロード機能](media/install-sdk/mac-install-selection.png)](media/install-sdk/mac-install-selection.png#lightbox)

::: zone-end

## <a name="install-alongside-visual-studio-code"></a>Visual Studio Code と共にインストールする

Visual Studio Code は、デスクトップ上で動作する強力で軽量なソース コード エディターです。 Visual Studio Code は、Windows、macOS、Linux で利用できます。

Visual Studio Code には、Visual Studio のような自動化された .NET Core インストーラーは付属していませんが、.NET Core のサポートを簡単に追加できます。

01. [Visual Studio Code をダウンロードしてインストールします](https://code.visualstudio.com/Download)。
01. [.NET Core SDK をダウンロードしてインストールします](https://dotnet.microsoft.com/download/dotnet-core)。
01. [Visual Studio Code マーケットプレースから C# 拡張機能をインストールします](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp)。

::: zone pivot="os-windows"

## <a name="install-with-powershell-automation"></a>PowerShell オートメーションを使用してインストールする

[dotnet-install スクリプト](../tools/dotnet-install-script.md)は、SDK のインストールの自動化および管理者以外によるインストールに使用されます。 スクリプトは、[dotnet-install スクリプト参照ページ](../tools/dotnet-install-script.md)からダウンロードできます。

スクリプトでは、最新の[長期サポート (LTS)](https://dotnet.microsoft.com/platform/support/policy/dotnet-core) バージョン (.NET Core 2.1) が既定でインストールされます。 NET Core の最新リリースをインストールするには、次のスイッチを使用してスクリプトを実行します。

```powershell
dotnet-install.ps1 -Channel Current
```

::: zone-end

::: zone pivot="os-linux,os-macos"

## <a name="install-with-bash-automation"></a>bash オートメーションを使用してインストールする

[dotnet-install スクリプト](../tools/dotnet-install-script.md)は、SDK のインストールの自動化および管理者以外によるインストールに使用されます。 スクリプトは、[dotnet-install スクリプト参照ページ](../tools/dotnet-install-script.md)からダウンロードできます。

スクリプトでは、最新の[長期サポート (LTS)](https://dotnet.microsoft.com/platform/support/policy/dotnet-core) バージョン (.NET Core 2.1) が既定でインストールされます。 NET Core の最新リリースをインストールするには、次のスイッチを使用してスクリプトを実行します。

```bash
./dotnet-install.sh -c Current
```

::: zone-end

## <a name="all-net-core-downloads"></a>すべての .NET Core のダウンロード

次のいずれかのリンクを使用して、.NET Core を直接ダウンロードしてインストールすることができます。

- [.NET Core 3.1 のダウンロード](https://dotnet.microsoft.com/download/dotnet-core/3.1)
- [.NET Core 3.0 のダウンロード](https://dotnet.microsoft.com/download/dotnet-core/3.0)
- [.NET Core 2.2 のダウンロード](https://dotnet.microsoft.com/download/dotnet-core/2.2)
- [.NET Core 2.1 のダウンロード](https://dotnet.microsoft.com/download/dotnet-core/2.1)

## <a name="docker"></a>Docker

コンテナーを使用すると、アプリケーションをホスト システムの他の部分から簡単に分離できます。 同じコンピューター上のコンテナーでは、カーネルだけが共有され、アプリケーションに提供されたリソースが使用されます。

.NET Core は Docker コンテナー内で実行できます。 公式の .NET Core Docker イメージは Microsoft Container Registry (MCR) に公開され、[Microsoft .NET Core の Docker Hub リポジトリ](https://hub.docker.com/_/microsoft-dotnet-core/)で見つけられます。 各リポジトリには、.NET (SDK またはランタイム) と自分が使用できる OS のさまざまな組み合わせのイメージが含まれています。

Microsoft は、特定のシナリオに対応したイメージを用意しています。 たとえば、[ASP.NET Core リポジトリ](https://hub.docker.com/_/microsoft-dotnet-core-aspnet/)には、運用環境での ASP.NET Core アプリの実行用にビルドされたイメージが用意されています。

Docker コンテナー内で .NET Core を使用する方法の詳細については、「[.NET および Docker の概要](../docker/introduction.md)」と[サンプル](https://github.com/dotnet/dotnet-docker/blob/master/samples/README.md)に関するページを参照してください。

## <a name="next-steps"></a>次の手順

::: zone pivot="os-windows"

- [チュートリアル: C# Hello World チュートリアル](../tutorials/with-visual-studio.md).
- [チュートリアル: Visual Basic Hello World チュートリアル](../tutorials/vb-with-visual-studio.md).
- [チュートリアル: Visual Studio Code を使用して新しいアプリを作成する](../tutorials/with-visual-studio-code.md)。
- [チュートリアル: NET Core アプリをコンテナー化する](../docker/build-container.md)。

::: zone-end

::: zone pivot="os-macos"

- [チュートリアル: macOS での作業を始める](../tutorials/using-on-mac-vs.md).
- [チュートリアル: Visual Studio Code を使用して新しいアプリを作成する](../tutorials/with-visual-studio-code.md)。
- [チュートリアル: NET Core アプリをコンテナー化する](../docker/build-container.md)。

::: zone-end

::: zone pivot="os-linux"

- [チュートリアル: Visual Studio Code を使用して新しいアプリを作成する](../tutorials/with-visual-studio-code.md)。
- [チュートリアル: NET Core アプリをコンテナー化する](../docker/build-container.md)。

::: zone-end
