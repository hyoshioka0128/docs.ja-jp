---
title: Windows における .NET Core の前提条件
description: Windows コンピューターで .NET Core アプリケーションを開発および実行する場合に必要な依存関係について説明します。
f1_keywords:
- NETSDK1045
ms.custom: updateeachvsrelease
ms.date: 09/20/2019
ms.openlocfilehash: b1557e6910cb6d0b6d7e2b3ce2aec97d3715fec7
ms.sourcegitcommit: 35da8fb45b4cca4e59cc99a5c56262c356977159
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/28/2019
ms.locfileid: "71591669"
---
# <a name="prerequisites-for-net-core-on-windows"></a>Windows における .NET Core の前提条件

この記事では、Windows 上で .NET Core アプリケーションを実行するためにサポートされる OS のバージョンについて説明します。 後述のサポート対象 OS のバージョンと依存関係は、Windows で .NET Core アプリを開発する次の 3 つの方法に適用されます。

* [コマンド ライン](./tutorials/using-with-xplat-cli.md)
* [Visual Studio](https://www.visualstudio.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2019)
* [Visual Studio Code](https://code.visualstudio.com/)

また、Visual Studio を使用して Windows 上で開発している場合、.NET Core 開発でサポートされている最小バージョンの詳細については、「[Visual Studio で .NET Core アプリを開発するための前提条件](#prerequisites-to-develop-net-core-apps-with-visual-studio)」セクションを参照してください。

## <a name="net-core-supported-operating-systems"></a>.NET Core がサポートされたオペレーティング システム

次の記事では、.NET Core がサポートされたオペレーティング システム (バージョンごと) の完全な一覧を示します。

* [.NET Core 3.0](https://github.com/dotnet/core/blob/master/release-notes/3.0/3.0-supported-os.md)
* [.NET Core 2.2](https://github.com/dotnet/core/blob/master/release-notes/2.2/2.2-supported-os.md)
* [.NET Core 2.1](https://github.com/dotnet/core/blob/master/release-notes/2.1/2.1-supported-os.md)

ダウンロード リンクと詳細については、最新バージョンをダウンロードするには [.NET ダウンロード](https://dotnet.microsoft.com/download)、以前のバージョンについて [.NET ダウンロードのアーカイブ](https://dotnet.microsoft.com/download/archives#dotnet-core)に関するページを参照してください。

## <a name="net-core-dependencies"></a>.NET Core の依存関係

次の場合には、[Microsoft Visual C++ 2015 再頒布可能パッケージ Update 3](https://www.microsoft.com/download/details.aspx?id=52685) を手動でインストールする必要があります。

* [インストーラー スクリプト](./tools/dotnet-install-script.md)を使用して .NET Core をインストールする。
* 自己完結型の .NET Core アプリケーションを展開する。
* ソースから製品をビルドする。
* *.zip* ファイルを使用して .NET Core をインストールする。 これにはビルド/CI/CD サーバーを含めることができます。

> [!NOTE]
> **Windows 8.1 以前のバージョン、または Windows Server 2012 R2 以前のバージョンの場合:**
>
> Windows のインストールが最新であり、Windows Update から修正プログラム [KB2999226](https://support.microsoft.com/help/2999226/update-for-universal-c-runtime-in-windows) をインストールしていることを確認してください。 この更新プログラムがインストールされていない場合は、.NET Core アプリケーションを起動するときに、次のようなエラーが表示されます。`The program can't start because api-ms-win-crt-runtime-l1-1-0.dll is missing from your computer. Try reinstalling the program to fix this problem.`
>
> **Windows 7 または Windows Server 2008 R2 の場合:**
>
> KB2999226 に加え、[KB2533623](https://support.microsoft.com/help/2533623/microsoft-security-advisory-insecure-library-loading-could-allow-remot) もインストールされていることを確認します。 この更新プログラムがインストールされていない場合は、.NET Core アプリケーションを起動するときに、次のようなエラーが表示されます。`The library hostfxr.dll was found, but loading it from C:\<path_to_app>\hostfxr.dll failed`

## <a name="prerequisites-to-develop-net-core-apps-with-visual-studio"></a>Visual Studio で .NET Core アプリを開発するための前提条件
    
.NET Core SDK を使用して .NET Core アプリケーションを開発するには任意のエディターを使用できますが、Visual Studio 2017 以降のバージョンでは、Windows での .NET Core アプリ用の統合開発環境が提供されています。

<a name="vs-mapping"></a>

.NET Core の各バージョンには、最低限必要な Visual Studio のバージョンがあります。 お使いの Visual Studio バージョンを確認するには、次の手順を実行します。

* **[ヘルプ]** メニューの **[About Microsoft Visual Studio]** (Microsoft Visual Studio のバージョン情報) を選択します。
* **[Microsoft Visual Studio のバージョン情報]** ダイアログで、バージョン番号を確認します。

次の表では、各 SDK の最小バージョンを示します。

| .NET Core SDK のバージョン | Visual Studio のバージョン                      |
| --------------------- | ------------------------------------------ |
| 3.0                   | Visual Studio 2019 バージョン 16.3 以降。 |
| 2.2                   | Visual Studio 2017 バージョン 15.9 以降。 |
| 2.1                   | Visual Studio 2017 バージョン 15.7 以降。 |
| 1.x                   | Visual Studio 2017 バージョン 15.0 以降。 |

<!-- markdownlint-disable MD025 -->

# <a name="net-core-30tabnetcore30"></a>[.NET Core 3.0](#tab/netcore30)

Visual Studio 2019 で .NET Core 3.0 SDK を使用して .NET Core アプリを開発するには:

* [Visual Studio 2019 バージョン 16.3 以降をダウンロードしてインストール](/visualstudio/install/install-visual-studio)し、ビルドしているアプリケーションの種類に応じて、.NET Core SDK が含まれる次のいずれかのワークロードを選択します。

  * **[他のツールセット]** セクションの **[.NET Core クロスプラットフォームの開発]** ワークロード。
  * **[Web クラウド]** セクションの **[ASP.NET と Web 開発]** ワークロード。
  * **[Windows]** セクションの **[.NET デスクトップ開発]** ワークロード。

次の図では、Visual Studio UI で **[.NET Core クロスプラットフォームの開発]** ワークロードが選択されています。

![".NET Core クロスプラットフォームの開発" ワークロードが選択された状態の Visual Studio 2019 インストールのスクリーンショット](./media/windows-prerequisites/vs-2019-workloads.jpg)

これらのいずれかのワークロードをインストールした後は、Visual Studio 2019 16.3 では .NET Core 3.0 SDK が既定で使用されます。

既存のプロジェクトで最新の .NET Core ランタイムを使用する場合は、次の手順を使用して、既存の各 .NET Core プロジェクトのターゲットを .NET Core 3.0 に再設定します。

* **[プロジェクト]** メニューの **[プロパティ]** をクリックします。
* **[ターゲット フレームワーク]** 選択メニューで、値を **[.NET Core 3.0]** に設定します。

![ターゲット フレームワーク メニュー項目で [.NET Core 3.0] が選択された Visual Studio 2019 のアプリケーション プロジェクト プロパティのスクリーンショット](./media/windows-prerequisites/target-dotnet-core-3-0.jpg)

Visual Studio が .NET Core 3.0 SDK で構成されている場合は、次の操作を行うことができます。

* 既存の .NET Core 1.x および 2.x プロジェクトを開き、ビルドし、実行する。
* .NET Core 1.x および 2.x プロジェクトのターゲットを .NET Core 3.0 に再設定し、ビルドし、実行する。
* .NET Core 3.0 の新しいプロジェクトを作成する。

# <a name="net-core-2xtabnetcore2x"></a>[.NET Core 2.x](#tab/netcore2x)

Visual Studio 2017 で .NET Core 2.2 SDK を使用して .NET Core アプリを開発するには:

* ( **[他のツールセット]** セクションで) **[.NET Core クロスプラットフォームの開発]** ワークロードを選択して、[Visual Studio 2019 バージョン 16.3 以降をダウンロードしてインストール](/visualstudio/install/install-visual-studio)します。
* ( **[その他のツールセット]** セクションで) **[.NET Core クロスプラットフォームの開発]** ワークロードを選択して、[Visual Studio 2017 バージョン 15.9.0 以降をダウンロードしてインストール](/visualstudio/install/install-visual-studio)します。

![".NET Core クロスプラットフォームの開発" ワークロードが選択された状態の Visual Studio 2017 インストールのスクリーン ショット](./media/windows-prerequisites/vs-2017-workloads.jpg)

**.NET Core クロスプラットフォーム開発**ツールセットをインストールすると、通常、Visual Studio には以前のバージョンの .NET Core SDK がインストールされます。
たとえば、ワークロードをインストールすると、Visual Studio 2017 15.9 には既定で .NET Core 2.1 SDK が使用されます。

.NET Core 2.2 SDK を使用するように Visual Studio を更新するには:

 1. [.NET Core 2.2 SDK](https://dotnet.microsoft.com/download) をインストールします。

 1. プロジェクトで最新の .NET Core ランタイムを使用する場合は、次の手順を使用して、既存または新規の各 .NET Core プロジェクトのターゲットを .NET Core 2.2 に再設定します。

    * **[プロジェクト]** メニューの **[プロパティ]** をクリックします。
    * **[ターゲット フレームワーク]** 選択メニューで、値を **[.NET Core 2.2]** に設定します。

![ターゲット フレームワーク メニュー項目で [.NET Core 2.2] が選択された Visual Studio 2017 のアプリケーション プロジェクト プロパティのスクリーンショット](./media/windows-prerequisites/targeting-dotnet-core.jpg)

Visual Studio が .NET Core 2.2 SDK で構成されている場合は、次の操作を行うことができます。

* 既存の .NET Core 1.x および 2.x プロジェクトを開き、ビルドし、実行する。
* .NET Core 1.x および 2.x プロジェクトを .NET Core 2.2 に再ターゲットし、ビルドし、実行する。
* .NET Core 2.2 の新しいプロジェクトを作成する。

---
