---
title: F# をインストールする
description: さまざまな方法で F# をインストールする方法について説明します。
ms.date: 12/20/2019
ms.openlocfilehash: 302e04f7cf3271516dff88d9d5f18f620b6ede80
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/14/2020
ms.locfileid: "79401095"
---
# <a name="install-f"></a>F をインストールする\#

F# は、環境に応じて複数の方法でインストールできます。

## <a name="install-f-with-visual-studio"></a>F# をインストールする

1. 初めて[Visual Studio](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2019)をダウンロードする場合は、最初に Visual Studio インストーラーをインストールします。 インストーラーから適切なエディションの Visual Studio をインストールします。

   Visual Studio が既にインストールされている場合は、F# を追加するエディションの横にある **[変更**] を選択します。

2. [ワークロード] ページで、ASP.NET コア プロジェクトの F# および .NET Core サポートを含む **、ASP.NETと Web 開発**ワークロードを選択します。

3. 右下隅にある [**変更]** を選択して、選択したすべてのものをインストールします。

   その後、Visual Studio インストーラーで**起動**を選択して、F# で Visual Studio を開くことができます。

## <a name="install-f-with-visual-studio-code"></a>F# をインストールする

1. パスに[git](https://git-scm.com/download)がインストールされ、使用可能であることを確認します。 コマンド プロンプトで入力し`git --version`**、Enter**キーを押すと、正しくインストールされていることを確認できます。

2. [.NET コア SDK](https://dotnet.microsoft.com/download)と[Visual Studio コード](https://code.visualstudio.com)をインストールします。

3. 拡張機能アイコンを選択し、「Ionide」を検索します。

   Visual Studio コードで F# のサポートに必要なプラグインは[、Ionide-fsharp](https://marketplace.visualstudio.com/items?itemName=Ionide.Ionide-fsharp)だけです。 しかし, また、[フェイ](https://fake.build/)クサポートを取得するために[Ionide-FAKE](https://marketplace.visualstudio.com/items?itemName=Ionide.Ionide-FAKE)をインストールし[、Paket](https://fsprojects.github.io/Paket/)のサポートを得るために[Ionide-Paket](https://marketplace.visualstudio.com/items?itemName=Ionide.Ionide-Paket)を取得することができます. FAKE と Paket は、プロジェクトをビルドし、依存関係を管理するための追加の F# コミュニティ ツールです。

## <a name="install-f-with-visual-studio-for-mac"></a>Mac 用の Visual Studio で F# をインストールする

F# は、選択した構成に関係なく、[既定では、Visual Studio for Mac](https://visualstudio.microsoft.com/vs/mac/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link)にインストールされます。

インストールが完了したら **、[Visual Studio の起動**] を選択します。 macOS のファインダーを使用して Visual Studio を開くことができます。

## <a name="install-f-on-a-build-server"></a>ビルド サーバーに F# をインストールする

NET SDK を使用して .NET Core または .NET Framework を使用している場合は、ビルド サーバーに .NET SDK をインストールするだけで済みます。 それはあなたが必要とするすべてを持っています。

NET Framework を使用していて、.NET SDK を使用**していない**場合は、Windows サーバーに Visual [Studio ビルド ツール SKU](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=BuildTools&rel=16)をインストールする必要があります。 インストーラーで **、.NET デスクトップ ビルド ツール**を選択し、インストーラー メニューの右側にある**F# コンパイラ**コンポーネントを選択します。
