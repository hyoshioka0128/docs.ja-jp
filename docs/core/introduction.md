---
title: .NET Core の紹介と概要
description: .NET Core は、Windows、Linux、macOS アプリを作成するための .NET のモジュール型の高性能な実装です。 ここでは、.NET Core の概要について説明します。
author: richlander
ms.date: 03/26/2020
ms.custom: updateeachrelease
ms.openlocfilehash: b28ad965e54680e2e1134c389266741ade28084f
ms.sourcegitcommit: 67cf756b033c6173a1bbd1cbd5aef1fccac99e34
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/10/2020
ms.locfileid: "86226583"
---
# <a name="introduction-to-net-core"></a>.NET Core の概要

[.NET Core](about.md) は、[オープンソース](https://github.com/dotnet/runtime/blob/master/LICENSE.TXT)の汎用開発プラットフォームです。 複数のプログラミング言語を使用して、x64、x86、ARM32、および ARM64 の各プロセッサ用に Windows、macOS、および Linux 用 .NET Core アプリを作成できます。 フレームワークと API は、[クラウド](/aspnet/core/)、[IoT](/archive/msdn-magazine/2019/august/net-core-cross-platform-iot-programming-with-net-core-3-0)、[クライアント UI](../desktop-wpf/overview/index.md)、[機械学習](/dotnet/machine-learning/)用に提供されています。

[.NET Core SDK をダウンロード](https://dotnet.microsoft.com/download)して、お使いのマシンで .NET Core を試してください。 最新バージョンは [.NET Core 3.1](https://devblogs.microsoft.com/dotnet/announcing-net-core-3-1/) です。

## <a name="download-net-core"></a>.NET Core のダウンロード

.NET Core は、次の方法で入手できます。

* [Windows および macOS 用のインストーラー](https://dotnet.microsoft.com/download)
* [Linux パッケージ](https://docs.microsoft.com/dotnet/core/install/linux-package-managers)
* [Docker コンテナー](https://hub.docker.com/_/microsoft-dotnet-core/)
* [zip と tar ボール](https://dotnet.microsoft.com/download/dotnet-core/3.1)
* [スクリプトのインストール](https://dotnet.microsoft.com/download/dotnet-core/scripts)
* [リリース ノート](https://github.com/dotnet/core/tree/master/release-notes)

## <a name="create-your-first-application"></a>最初のアプリケーションの作成

.NET Core SDK をインストールしたらコマンド プロンプトを開きます。 次のコマンドを使用し、アプリケーションを作成して実行します。

```dotnetcli
dotnet new console
dotnet run
```

次の出力が表示されます。

```output
Hello World!
```

## <a name="contribute"></a>投稿

.NET Core はオープン プラットフォームです。 どなたでも参加できます。

* [開発者コミュニティ](https://developercommunity.visualstudio.com/spaces/61/index.html)で製品に関する問題と質問をお寄せください。
* 製品の投稿は、[dotnet/runtime](https://github.com/dotnet/runtime)、[dotnet/sdk](https://github.com/dotnet/sdk)、[dotnet/rosyln](https://github.com/dotnet/roslyn)、[aspnetcore](https://github.com/dotnet/aspnetcore) などのプロジェクト リポジトリのいずれかで行う必要があります。 詳細については、[.NET Core リポジトリ](https://github.com/dotnet/core/blob/master/Documentation/core-repos.md)に関するページを参照してください。

## <a name="support"></a>サポート

.NET Core は、Windows、macOS、および Linux 上の Microsoft と、Red Hat Enterprise Linux 上の Red Hat でサポートされています。

## <a name="next-steps"></a>次の手順

> [!div class="nextstepaction"]
> [.NET Core チュートリアル](tutorials/index.md)

> [!div class="nextstepaction"]
> [ブラウザーで .NET Core を試す](../csharp/tutorials/intro-to-csharp/numbers-in-csharp.yml)
