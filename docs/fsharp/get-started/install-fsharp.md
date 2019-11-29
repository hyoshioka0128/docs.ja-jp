---
title: F# をインストールする
description: 環境に基づいてF#をインストールする方法について説明します。
ms.date: 09/05/2019
ms.openlocfilehash: 592a4c7763266cee68809fca84f9604d7e96b8f1
ms.sourcegitcommit: 81ad1f09b93f3b3e6706a7f2e4ddf50ef229ea3d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/20/2019
ms.locfileid: "74204874"
---
# <a name="install-f"></a>F\# のインストール

環境に応じて、複数の方法で F# をインストールできます。

## <a name="install-f-with-visual-studio"></a>Visual Studio で F# をインストールする

[Visual studio](https://visualstudio.microsoft.com/vs/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link)を初めてダウンロードする場合は、最初に visual studio インストーラーをインストールします。 インストーラーから適切な SKU の Visual Studio をインストールします。 既にインストールされている場合は、 **[変更]** をクリックします。

次に、ワークロードの一覧が表示されます。 ASP.NET Core プロジェクトのサポートと .NET Core サポートF#をインストールする**ASP.NET と web 開発**を選択します。

次に、右下にある **[変更]** をクリックします。  これにより、選択したすべてのものがインストールされます。 その後、 **[起動]** をクリックF#して、Visual Studio 2017 を言語サポートで開くことができます。

## <a name="install-f-with-visual-studio-code"></a>Visual Studio Code F#と共にインストールする

最初に、git が[インストールされ](https://git-scm.com/download)、パスに使用できることを確認します。 コマンドプロンプトで「`git --version`」と入力し、 **enter**キーを押すと、正しくインストールされていることを確認できます。

次に、 [.NET Core SDK](https://dotnet.microsoft.com/download)をインストールします。

その後、 [Visual Studio Code](https://code.visualstudio.com)インストールする必要があります。

次に、[拡張機能] アイコンをクリックし、"Ionide" を検索します。

Visual Studio Code でのサポートにF#必要なプラグインは、 [Ionide fsharp.core](https://marketplace.visualstudio.com/items?itemName=Ionide.Ionide-fsharp)だけです。 ただし、Ionide をインストールして、[偽](https://fake.build/)[の](https://marketplace.visualstudio.com/items?itemName=Ionide.Ionide-FAKE)サポートと[Ionide](https://marketplace.visualstudio.com/items?itemName=Ionide.Ionide-Paket)を取得し、[パケット](https://fsprojects.github.io/Paket/)のサポートを取得することもできます。 フェイクとパケットは、 F#プロジェクトをビルドし、依存関係を管理するための追加のコミュニティツールです。

## <a name="install-f-with-visual-studio-for-mac"></a>Visual Studio for Macで F# をインストールする

F#は、選択した構成に関係なく[Visual Studio for Mac](https://visualstudio.microsoft.com/vs/mac/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link)に既定でインストールされます。

インストールが完了したら、[Visual Studio の起動] を選択します。 また、macOS で Finder を使用して起動することもできます。

## <a name="install-f-on-a-build-server"></a>ビルドサーバーに F＃ をインストールする

.Net Core または .net SDK を .NET Framework を経由で使用している場合は、.NET SDK をビルドサーバーにインストールするだけです。 必要なものはすべて揃っています。

.NET Framework を使用していて、.NET SDK を使用して**いない**場合は、 [Visual Studio Build Tools SKU](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=BuildTools&rel=16)を Windows Server にインストールする必要があります。 インストーラーで、 **[.net デスクトップビルドツール]** を選択し、インストーラーメニューの右側にある **F#コンパイラ**コンポーネントを選択します。
