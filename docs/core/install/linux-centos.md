---
title: CentOS に .NET Core をインストールする - .NET Core
description: CentOS に .NET Core SDK と .NET Core ランタイムをインストールするさまざまな方法を示します。
author: adegeo
ms.author: adegeo
ms.date: 06/04/2020
ms.openlocfilehash: 6b1bad3a6c967483bb683866de84c9e5077a336f
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85619508"
---
# <a name="install-net-core-sdk-or-net-core-runtime-on-centos"></a>CentOS に .NET Core SDK または .NET Core ランタイムをインストールする

.NET Core は CentOS でサポートされています。 この記事では、CentOS に .NET Core をインストールする方法について説明します。

[!INCLUDE [linux-intro-sdk-vs-runtime](includes/linux-intro-sdk-vs-runtime.md)]

[!INCLUDE [linux-install-package-manager-x64-vs-arm](includes/linux-install-package-manager-x64-vs-arm.md)]

## <a name="supported-distributions"></a>サポートされているディストリビューション

次の表は、CentOS 7 と CentOS 8 の両方で現在サポートされている .NET Core リリースの一覧です。 これらのバージョンは、[.NET Core のバージョンがサポート終了になる](https://dotnet.microsoft.com/platform/support/policy/dotnet-core)か、CentOS のバージョンがサポート終了になるまでサポートされます。

- ✔️ は、CentOS または .NET Core のバージョンがまだサポートされていることを示します。
- ❌ は、CentOS または .NET Core のバージョンがその CentOS のリリースではサポートされていないことを示しています。
- CentOS のバージョンと .NET Core のバージョンの両方に ✔️ が付いている場合、その OS と .NET の組み合わせはサポートされています。

| CentOS                   | .NET Core 2.1 | .NET Core 3.1 | .NET 5 Preview (手動インストールのみ) |
|--------------------------|---------------|---------------|----------------|
| ✔️ [8](#centos-8-) | ✔️ 2.1        | ✔️ 3.1        | ✔️ 5.0 Preview |
| ✔️ [7](#centos-7-) | ✔️ 2.1        | ✔️ 3.1        | ✔️ 5.0 Preview |

次のバージョンの .NET Core は、サポート対象外となりました。 これらのダウンロードは、まだ公開されています。

- 3.0
- 2.2
- 2.0

[!INCLUDE [linux-install-package-manager-x64-vs-arm](includes/linux-install-package-manager-x64-vs-arm.md)]

## <a name="how-to-install-other-versions"></a>その他のバージョンをインストールする方法

[!INCLUDE [package-manager-switcher](./includes/package-manager-heading-hack-pkgname.md)]

## <a name="centos-8-"></a>CentOS 8 ✔️

.NET Core 3.1 は CentOS 8 の既定のパッケージ リポジトリで利用できます。

[!INCLUDE [linux-dnf-install-31](includes/linux-install-31-dnf.md)]

## <a name="centos-7-"></a>CentOS 7 ✔️

[!INCLUDE [linux-prep-intro-generic](includes/linux-prep-intro-generic.md)]

```bash
sudo rpm -Uvh https://packages.microsoft.com/config/centos/7/packages-microsoft-prod.rpm
```

[!INCLUDE [linux-yum-install-31](includes/linux-install-31-yum.md)]

## <a name="troubleshoot-the-package-manager"></a>パッケージ マネージャーのトラブルシューティング

このセクションでは、パッケージ マネージャーを使用して .NET Core をインストールするときに発生する可能性のある一般的なエラーについて説明します。

### <a name="failed-to-fetch"></a>フェッチできない

[!INCLUDE [package-manager-failed-to-fetch-rpm](includes/package-manager-failed-to-fetch-rpm.md)]

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
