---
title: Linux RHEL 7 に .NET Core をインストールする - パッケージ マネージャー - .NET Core
description: パッケージ マネージャーを使用して、.NET Core SDK とランタイムを RHEL 7 にインストールします。
author: thraka
ms.author: adegeo
ms.date: 12/03/2019
ms.openlocfilehash: f17a410ccea1ef4dec32de1d80ef6aac889aa6f3
ms.sourcegitcommit: a4f9b754059f0210e29ae0578363a27b9ba84b64
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/05/2019
ms.locfileid: "74998907"
---
# <a name="rhel-7-package-manager---install-net-core"></a>RHEL 7 パッケージ マネージャー - .NET Core をインストールする

[!INCLUDE [package-manager-switcher](includes/package-manager-switcher.md)]

この記事では、パッケージ マネージャーを使用して RHEL 7 に .NET Core をインストールする方法について説明します。 .NET Core 3.1 は、RHEL 7 ではまだ使用できません。

## <a name="register-your-red-hat-subscription"></a>ご利用の Red Hat サブスクリプションを登録する

Red Hat から RHEL に .NET Core をインストールするには、まず、Red Hat Subscription Manager を使用して登録する必要があります。 ご利用のシステム上でこれがまだ行われていない場合、または不明な場合は、[.NET Core 向け Red Hat 製品ドキュメント](https://access.redhat.com/documentation/net_core/)を参照してください。

## <a name="install-the-net-core-sdk"></a>.NET Core SDK をインストールする

Subscription Manager に登録すると、.NET Core SDK をインストールして有効にする準備が整います。 ご利用のターミナルで、次のコマンドを実行することで、RHEL 7 dotnet チャネルを有効にしてインストールします。

```bash
subscription-manager repos --enable=rhel-7-server-dotnet-rpms
yum install rh-dotnet30 -y
scl enable rh-dotnet30 bash
```

## <a name="install-the-aspnet-core-runtime"></a>ASP.NET Core ランタイムをインストールする

Subscription Manager に登録すると、ASP.NET Core ランタイムをインストールして有効にする準備が整います。 ご利用のターミナルで、次のコマンドを実行します。

<!-- TODO: is this the correct value? Taken from the webpage but it doesn't have aspnet in the name -->
```bash
subscription-manager repos --enable=rhel-7-server-dotnet-rpms
yum install rh-dotnet30-aspnetcore-runtime-3.0 -y
scl enable rh-dotnet30 bash
```

## <a name="install-the-net-core-runtime"></a>.NET Core ランタイムをインストールする

Subscription Manager に登録すると、.NET Core ランタイムをインストールして有効にする準備が整います。 ご利用のターミナルで、次のコマンドを実行します。

```bash
subscription-manager repos --enable=rhel-7-server-dotnet-rpms
yum install rh-dotnet30-dotnet-runtime-3.0 -y
scl enable rh-dotnet30 bash
```

## <a name="see-also"></a>関連項目

- [Red Hat Enterprise Linux 7 での .NET Core 3.0 の使用](https://access.redhat.com/documentation/en-us/net_core/3.0/html/getting_started_guide/gs_install_dotnet)
