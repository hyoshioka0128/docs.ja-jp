---
title: RHEL に .NET Core をインストールする - .NET Core
description: RHEL に .NET Core SDK と .NET Core ランタイムをインストールするさまざまな方法を示します。
author: adegeo
ms.author: adegeo
ms.date: 06/04/2020
ms.openlocfilehash: 9e4d0ab86355329b898a82f135b9eeb839eab1cb
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85619450"
---
# <a name="install-net-core-sdk-or-net-core-runtime-on-rhel"></a>RHEL に .NET Core SDK または .NET Core ランタイムをインストールする

.NET Core は RHEL でサポートされています。 この記事では、RHEL に .NET Core をインストールする方法について説明します。

[!INCLUDE [linux-intro-sdk-vs-runtime](includes/linux-intro-sdk-vs-runtime.md)]

## <a name="register-your-red-hat-subscription"></a>ご利用の Red Hat サブスクリプションを登録する

Red Hat から RHEL に .NET Core をインストールするには、まず、Red Hat Subscription Manager を使用して登録する必要があります。 ご利用のシステム上でこれがまだ行われていない場合、または不明な場合は、[.NET Core 向け Red Hat 製品ドキュメント](https://access.redhat.com/documentation/net_core/)を参照してください。

## <a name="supported-distributions"></a>サポートされているディストリビューション

次の表は、RHEL 7 と RHEL 8 の両方で現在サポートされている .NET Core リリースの一覧です。 これらのバージョンは、[.NET Core のバージョンがサポート終了になる](https://dotnet.microsoft.com/platform/support/policy/dotnet-core)か、RHEL のバージョンがサポート終了になるまでサポートされます。

- ✔️ は、RHEL または .NET Core のバージョンがまだサポートされていることを示します。
- ❌ は、RHEL または .NET Core のバージョンがその RHEL のリリースではサポートされていないことを示しています。
- RHEL のバージョンと .NET Core のバージョンの両方に ✔️ が付いている場合、その OS と .NET の組み合わせはサポートされています。

| RHEL                   | .NET Core 2.1 | .NET Core 3.1 | .NET 5 Preview (手動インストールのみ) |
|--------------------------|---------------|---------------|----------------|
| ✔️ [8](#rhel-8-) | ✔️ 2.1        | ✔️ 3.1        | ✔️ 5.0 Preview |
| ✔️ [7](#rhel-7-) | ✔️ 2.1        | ✔️ 3.1        | ✔️ 5.0 Preview |

次のバージョンの .NET Core は、サポート対象外となりました。 これらのダウンロードは、まだ公開されています。

- 3.0
- 2.2
- 2.0

## <a name="how-to-install-other-versions"></a>その他のバージョンをインストールする方法

.NET Core の他のリリースをインストールするために必要な手順については、[.NET Core に関する Red Hat のドキュメント](https://access.redhat.com/documentation/net_core/)を参照してください。

## <a name="rhel-8-"></a>RHEL 8 ✔️

.NET Core は、RHEL 8 用の AppStream リポジトリに含まれています。

[!INCLUDE [linux-dnf-install-31](includes/linux-install-31-dnf.md)]

## <a name="rhel-7-"></a>RHEL 7 ✔️

[!INCLUDE [linux-prep-intro-generic](includes/linux-prep-intro-generic.md)]

次のコマンドでは、`scl-utils` パッケージがインストールされます。

```bash
sudo yum install scl-utils
```

### <a name="install-the-sdk"></a>SDK のインストール

.NET Core SDK を使用すると、.NET Core を使用してアプリを開発できます。 .NET Core SDK をインストールする場合、対応するランタイムをインストールする必要はありません。 .NET Core SDK をインストールするには、次のコマンドを実行します。

```bash
subscription-manager repos --enable=rhel-7-server-dotnet-rpms
yum install rh-dotnet31 -y
scl enable rh-dotnet31 bash
```

Red Hat では、`rh-dotnet31` を永続的に有効にすることは推奨されません。他のプログラムに影響を与える可能性があるためです。 たとえば、`rh-dotnet31` には、ベースとなる RHEL のバージョンとは異なるバージョンの `libcurl` が含まれています。 これにより、異なるバージョンの `libcurl` を想定していないプログラムで問題が発生する可能性があります。 `rh-dotnet` を永続的に有効にする場合は、 _~/.bashrc_ ファイルに次の行を追加します。

```bash
source scl_source enable rh-dotnet31
```

### <a name="install-the-runtime"></a>ランタイムをインストールする

.NET Core ランタイムを使用すると、ランタイムを含まない .NET Core を使用して作成されたアプリを実行できます。 次のコマンドを実行すると、.NET Core の最も互換性の高いランタイムである ASP.NET Core ランタイムがインストールされます。 ご利用のターミナルで、次のコマンドを実行します。

```bash
subscription-manager repos --enable=rhel-7-server-dotnet-rpms
yum install rh-dotnet31-aspnetcore-runtime-3.1 -y
scl enable rh-dotnet31-aspnetcore-runtime-3.1 bash
```

Red Hat では、`rh-dotnet31-aspnetcore-runtime-3.1` を永続的に有効にすることは推奨されません。他のプログラムに影響を与える可能性があるためです。 たとえば、`rh-dotnet31-aspnetcore-runtime-3.1` には、ベースとなる RHEL のバージョンとは異なるバージョンの `libcurl` が含まれています。 これにより、異なるバージョンの `libcurl` を想定していないプログラムで問題が発生する可能性があります。 `rh-dotnet31-aspnetcore-runtime-3.1` を永続的に有効にする場合は、 _~/.bashrc_ ファイルに次の行を追加します。

```bash
source scl_source enable rh-dotnet31-aspnetcore-runtime-3.1
```

ASP.NET Core ランタイムの代替手段として、ASP.NET Core サポートを含まない .NET Core ランタイムをインストールできます。それには、前述のコマンドの `rh-dotnet31-aspnetcore-runtime-3.1` を `rh-dotnet31-dotnet-runtime-3.1` で置き換えます。

## <a name="snap"></a>Snap

[!INCLUDE [linux-install-snap](includes/linux-install-snap.md)]

## <a name="dependencies"></a>依存関係

[!INCLUDE [linux-rpm-install-dependencies](includes/linux-rpm-install-dependencies.md)]

## <a name="scripted-install"></a>スクリプトでのインストール

[!INCLUDE [linux-install-scripted](includes/linux-install-scripted.md)]

## <a name="manual-install"></a>手動インストール

[!INCLUDE [linux-install-manual](includes/linux-install-manual.md)]

## <a name="next-steps"></a>次の手順

- [チュートリアル: Visual Studio Code を使用して .NET Core SDK でコンソール アプリケーションを作成する](../tutorials/with-visual-studio-code.md)
