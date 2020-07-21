---
title: Alpine に .NET Core をインストールする - .NET Core
description: Alpine に .NET Core SDK と .NET Core ランタイムをインストールするさまざまな方法を示します。
author: adegeo
ms.author: adegeo
ms.date: 06/04/2020
ms.openlocfilehash: 0efe3bbacbe573b77eae8818ea29b5a3867e4570
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85619521"
---
# <a name="install-net-core-sdk-or-net-core-runtime-on-alpine"></a>Alpine に .NET Core SDK または .NET Core ランタイムをインストールする

この記事では、Alpine に .NET Core をインストール方法について説明します。 Alpine のバージョンがサポート対象外である場合、.NET Core もそのバージョンでサポート対象外となります。 ただし、サポート対象外のバージョンで .NET Core を実行するのに、ここで説明する手順が役立つ場合があります。

[!INCLUDE [linux-intro-sdk-vs-runtime](includes/linux-intro-sdk-vs-runtime.md)]

Alpine には、インストーラーはありません。 [インストール スクリプト](#scripted-install)を使用するか、[手動でのインストール](#manual-install)手順に従う必要があります。

## <a name="supported-distributions"></a>サポートされているディストリビューション

次の表に、現在サポートされている .NET Core リリースと、それらがサポートされている Alpine のバージョンの一覧を示します。 これらのバージョンは、[.NET Core のバージョンがサポート終了](https://dotnet.microsoft.com/platform/support/policy/dotnet-core)するか、[Alpine のバージョンの有効期限が切れるまで](https://wiki.alpinelinux.org/wiki/Alpine_Linux:Releases)サポートされます。

- ✔️ は、Alpine または .NET Core のバージョンがまだサポートされていることを示します。
- ❌ は、Alpine または .NET Core のバージョンがその Alpine のリリースではサポートされないことを示します。
- Alpine のバージョンと .NET Core のバージョンの両方に ✔️ がある場合、その OS と .NET の組み合わせはサポートされます。

| Alpine                   | .NET Core 2.1 | .NET Core 3.1 | .NET 5 Preview |
|--------------------------|---------------|---------------|----------------|
| ✔️ 3.12  | ✔️ 2.1        | ✔️ 3.1        | ✔️ 5.0 Preview |
| ✔️ 3.11  | ✔️ 2.1        | ✔️ 3.1        | ✔️ 5.0 Preview |
| ✔️ 3.10  | ✔️ 2.1        | ✔️ 3.1        | ✔️ 5.0 Preview |
| ✔️ 3.9   | ✔️ 2.1        | ✔️ 3.1        | ✔️ 5.0 Preview |
| ❌ 3.8   | ✔️ 2.1        | ❌ 3.1        | ❌ 5.0 Preview |

次のバージョンの .NET Core は、サポート対象外となりました。 これらのダウンロードは、まだ公開されています。

- 3.0
- 2.2
- 2.0

## <a name="dependencies"></a>依存関係

Alpine Linux 上の .NET Core には、次の依存関係がインストールされている必要があります。

- icu-libs
- krb5-libs
- libgcc
- libintl
- libssl1.1 (Alpine v3.9 以上)
- libssl1.0 (Alpine v3.8 以下)
- libstdc++
- zlib

## <a name="scripted-install"></a>スクリプトでのインストール

[!INCLUDE [linux-install-scripted](includes/linux-install-scripted.md)]

## <a name="manual-install"></a>手動インストール

[!INCLUDE [linux-install-manual](includes/linux-install-manual.md)]

## <a name="next-steps"></a>次の手順

- [チュートリアル: Visual Studio Code を使用して .NET Core SDK でコンソール アプリケーションを作成する](../tutorials/with-visual-studio-code.md)
