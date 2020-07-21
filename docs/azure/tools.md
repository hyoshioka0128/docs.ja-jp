---
title: Azure .NET 開発者向けツール
description: Windows、Linux、Mac 環境から Azure .NET ライブラリを使い始めるためのツールを入手します。
ms.date: 06/19/2020
ms.custom: azure-sdk-dotnet
ms.openlocfilehash: fa645b152f15550b25a3542ba0cdbb43799536b9
ms.sourcegitcommit: cb27c01a8b0b4630148374638aff4e2221f90b22
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/09/2020
ms.locfileid: "86174835"
---
# <a name="azure-tools-for-developing-with-net"></a>.NET で開発するための Azure ツール

## <a name="sdk-downloads"></a>SDK のダウンロード

.NET 用 Azure ライブラリは [NuGet パッケージ](https://www.nuget.org/packages?q=windowsazureofficial)として実装されています。 Azure サービス別に整理されているリファレンス ドキュメントが必要であれば、[API リファレンス](/dotnet/api/overview/azure/?view=azure-dotnet)に関する記事を参照してください。

## <a name="development-tools"></a>開発ツール

Visual Studio には、Azure サービス向けの多くのツールが組み込まれています。 一部の Azure サービスでは、[Azure Storage Explorer](https://azure.microsoft.com/features/storage-explorer/) などの追加のツールやエミュレーターが提供されています。 必要に応じて、その他のツールについては、Azure サービスのドキュメントを参照してください。

希望の開発環境を以下から選択します。

## <a name="visual-studio-on-windows"></a>[Windows 上の Visual Studio](#tab/vs)

Visual Studio バージョン 2017 以降には、Azure 開発の組み込みサポートがあります。 以下の手順では、Visual Studio での Azure 開発サポートの有効化について説明します。

Visual Studio 2015 以前の場合は、<a href="vs2015-install.md">これらの手順</a>に従います。

### <a name="step-1-download-visual-studio-2019"></a>手順 1: Visual Studio 2019 のダウンロード

Visual Studio 2019 を既にインストールしてある場合は省略できます。

> [!div class="nextstepaction"]
> [Visual Studio 2019 のダウンロード](https://www.visualstudio.com/downloads/)

### <a name="step-2-install-the-two-azure-workloads"></a>手順 2: 2 つの Azure ワークロードをインストールする

Visual Studio インストーラーで、Visual Studio をインストールします (または既存のインストールを変更します)。 *Azure 開発*および *ASP.NET と Web 開発*ワークロードが選択されていることを確認します。

### <a name="step-3-develop-with-net-on-azure"></a>手順 3: Azure で .NET を使って開発する

まず、[最初の ASP.NET Core Web アプリを Azure App Service にデプロイ](/azure/app-service-web/app-service-web-get-started-dotnet)します。

## <a name="visual-studio-code-cross-platform"></a>[Visual Studio Code (クロスプラットフォーム)](#tab/vscode)

Visual Studio Code には、クロスプラットフォーム Azure での開発に必要なすべてのものが揃っています。

### <a name="step-1-download-the-net-core-sdk"></a>手順 1: .NET Core SDK をダウンロードする

.NET Core アプリ用の SDK とコマンド ライン ツールです。

> [!div class="nextstepaction"]
> [.NET Core SDK をダウンロードする](https://dotnet.microsoft.com/download)

### <a name="step-2-visual-studio-code"></a>手順 2: Visual Studio Code

任意のオペレーティング システム上で .NET Core アプリを編集し、デバッグします (Windows、Mac、Linux)。

> [!div class="nextstepaction"]
> [Visual Studio Code をダウンロードする](https://code.visualstudio.com)

### <a name="step-3-azure-tools-extension"></a>手順 3: Azure Tools 拡張機能

Visual Studio Code で Azure Tools 拡張機能をインストールします。

> [!div class="nextstepaction"]
> [Azure Tools 拡張機能のインストール](https://marketplace.visualstudio.com/items?itemName=ms-vscode.vscode-node-azure-pack)

### <a name="step-4-develop-with-net-on-azure"></a>手順 4: Azure で .NET を使って開発する

まず、[最初の ASP.NET Core Web アプリを Azure App Service on Linux にデプロイ](/azure/app-service/containers/quickstart-dotnetcore)します。

---
