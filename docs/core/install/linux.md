---
title: .NET Core と Linux ディストリビューションをインストールする
description: Linux への .NET Core のインストールをサポートしている Linux ディストリビューションについて説明します。
author: adegeo
ms.author: adegeo
ms.date: 06/01/2020
ms.openlocfilehash: 06a90d7fecfe9f25d26caccb2fe3aedec0176f64
ms.sourcegitcommit: c23d9666ec75b91741da43ee3d91c317d68c7327
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85803093"
---
# <a name="install-net-core-on-linux"></a>Linux に .NET Core をインストールする

> [!div class="op_single_selector"]
>
> - [Windows へのインストール](windows.md)
> - [macOS へのインストール](macos.md)
> - [Linux へのインストール](linux.md)

.NET Core は、さまざまな Linux ディストリビューションで使用できます。 ほとんどの Linux プラットフォームおよびディストリビューションには毎年メジャー リリースがあり、そのほとんどでは .NET Core のインストールに使用されるパッケージ マネージャーが提供されます。 この記事では、現在何がサポートされているかと、どのパッケージ マネージャーが使用されるかについて説明します。

この記事の残りの部分では、.NET Core でサポートされている主要な各 Linux ディストリビューションの詳細について説明します。 すべての .NET Core リリースは、[.NET Core のバージョンがサポート終了になる](https://dotnet.microsoft.com/platform/support/policy/dotnet-core)か、Linux ディストリビューションのバージョンがサポート終了になるまでサポートされます。

互換性を最大限に高めるために、長期的なリリース (LTS) のバージョンを選択してください。

## <a name="unsupported-releases"></a>サポートされていないリリース

次のバージョンの .NET Core は ❌ サポート対象外となりました。 これらのダウンロードは、まだ公開されています。

- 3.0
- 2.2
- 2.0

これらのサポートされていないバージョンについては、以下のセクションでは詳しく説明しません。これらをインストールしようとする場合、実現できることが変動する可能性があります。

## <a name="alpine"></a>Alpine

Alpine には、インストーラーはありません。 [インストール スクリプト](linux-alpine.md#scripted-install)を使用するか、[手動でのインストール](linux-alpine.md#manual-install)手順に従う必要があります。

次の表に、現在サポートされている .NET Core リリースと、それらがサポートされている Alpine のバージョンの一覧を示します。 これらのバージョンは、[.NET Core のバージョンがサポート終了](https://dotnet.microsoft.com/platform/support/policy/dotnet-core)するか、[Alpine のバージョンの有効期限が切れるまで](https://wiki.alpinelinux.org/wiki/Alpine_Linux:Releases)サポートされます。

- ✔️ は、Alpine または .NET Core のバージョンがまだサポートされていることを示します。
- ❌ は、Alpine または .NET Core のバージョンがその Alpine のリリースではサポートされないことを示します。
- Alpine のバージョンと .NET Core のバージョンの両方に ✔️ がある場合、その OS と .NET の組み合わせはサポートされます。

| Alpine                      | .NET Core 2.1 | .NET Core 3.1 | .NET 5 Preview |
|-----------------------------|---------------|---------------|----------------|
| ✔️ [3.12](linux-alpine.md)  | ✔️ 2.1        | ✔️ 3.1        | ✔️ 5.0 Preview |
| ✔️ [3.11](linux-alpine.md)  | ✔️ 2.1        | ✔️ 3.1        | ✔️ 5.0 Preview |
| ✔️ [3.10](linux-alpine.md)  | ✔️ 2.1        | ✔️ 3.1        | ✔️ 5.0 Preview |
| ✔️ [3.9](linux-alpine.md)   | ✔️ 2.1        | ✔️ 3.1        | ✔️ 5.0 Preview |
| ❌ [3.8](linux-alpine.md)   | ✔️ 2.1        | ❌ 3.1        | ❌ 5.0 Preview |

詳細については、[Alpine での .NET Core のインストール](linux-alpine.md)に関する記事をご覧ください。

## <a name="centos"></a>CentOS

CentOS 7 ではパッケージ マネージャーとして Yum が使用され、CentOS 8 では DNF が使用されます。

次の表は、CentOS 7 と CentOS 8 の両方で現在サポートされている .NET Core リリースの一覧です。 これらのバージョンは、[.NET Core のバージョンがサポート終了になる](https://dotnet.microsoft.com/platform/support/policy/dotnet-core)か、CentOS のバージョンがサポート終了になるまでサポートされます。

| CentOS                   | .NET Core 2.1 | .NET Core 3.1 | .NET 5 Preview (手動インストールのみ) |
|--------------------------|---------------|---------------|----------------|
| ✔️ [8](linux-centos.md#centos-8-) | ✔️ 2.1        | ✔️ 3.1        | ✔️ 5.0 Preview |
| ✔️ [7](linux-centos.md#centos-7-) | ✔️ 2.1        | ✔️ 3.1        | ✔️ 5.0 Preview |

詳細については、[CentOS での .NET Core のインストール](linux-centos.md)に関する記事をご覧ください。

## <a name="debian"></a>Debian

Debian では、パッケージ マネージャーとして APT (Advanced Package Tool) が使用されます。

次の表は、現在サポートされている .NET Core リリースと、それらがサポートされている Debian のバージョンの一覧です。 これらのバージョンは、[.NET Core のバージョンがサポート終了になる](https://dotnet.microsoft.com/platform/support/policy/dotnet-core)か、[Debian のバージョンがサポート終了になる](https://wiki.debian.org/DebianReleases)までサポートされます。

- ✔️ は、Debian または .NET Core のバージョンがまだサポートされていることを示します。
- ❌ は、Debian または .NET Core のバージョンがその Debian のリリースではサポートされていないことを示しています。
- Debian のバージョンと .NET Core のバージョンの両方に ✔️ が付いている場合、その OS と .NET の組み合わせはサポートされています。

| Debian                   | .NET Core 2.1 | .NET Core 3.1 | .NET 5 Preview (手動インストールのみ) |
|--------------------------|---------------|---------------|----------------|
| ✔️ [10](linux-debian.md#debian-10-)     | ✔️ 2.1        | ✔️ 3.1        | ✔️ 5.0 Preview |
| ✔️ [9](linux-debian.md#debian-9-)       | ✔️ 2.1        | ✔️ 3.1        | ✔️ 5.0 Preview |
| ❌ [8](linux-debian.md#debian-8-)       | ✔️ 2.1        | ❌ 3.1        | ❌ 5.0 Preview |

詳細については、[Debian での .NET Core のインストール](linux-debian.md)に関する記事をご覧ください。

## <a name="fedora"></a>Fedora

Fedora では、パッケージ マネージャーとして DNF が使用されます。

次の表は、現在サポートされている .NET Core リリースと、それらがサポートされている Fedora のバージョンの一覧です。 これらのバージョンは、[.NET Core のバージョンがサポート終了になる](https://dotnet.microsoft.com/platform/support/policy/dotnet-core)か、[Fedora のバージョンがサポート終了になる](https://fedoraproject.org/wiki/End_of_life)までサポートされます。

- ✔️ は、Fedora または .NET Core のバージョンがまだサポートされていることを示します。
- ❌ は、Fedora または .NET Core のバージョンがその Fedora のリリースではサポートされていないことを示しています。
- Fedora のバージョンと .NET Core のバージョンの両方に ✔️ が付いている場合、その OS と .NET の組み合わせはサポートされています。

| Fedora                   | .NET Core 2.1 | .NET Core 3.1 | .NET 5 Preview (手動インストールのみ) |
|--------------------------|---------------|---------------|----------------|
| ✔️ [32](linux-fedora.md#fedora-32-) | ✔️ 2.1        | ✔️ 3.1        | ✔️ 5.0 Preview |
| ✔️ [31](linux-fedora.md#fedora-31-) | ✔️ 2.1        | ✔️ 3.1        | ✔️ 5.0 Preview |
| ❌ [30](linux-fedora.md#fedora-30-) | ✔️ 2.1        | ✔️ 3.1        | ❌ 5.0 Preview |
| ❌ [29](linux-fedora.md#fedora-29-) | ✔️ 2.1        | ✔️ 3.1        | ❌ 5.0 Preview |
| ❌ [28](linux-fedora.md#fedora-28-) | ✔️ 2.1        | ❌ 3.1        | ❌ 5.0 Preview |
| ❌ [27](linux-fedora.md#fedora-27-) | ✔️ 2.1        | ❌ 3.1        | ❌ 5.0 Preview |

詳細については、[Fedora での .NET Core のインストール](linux-fedora.md)に関する記事をご覧ください。

## <a name="opensuse"></a>openSUSE

openSUSE では、パッケージ マネージャーとして zypper が使用されます。

次の表は、openSUSE 15 で現在サポートされている .NET Core リリースの一覧です。 これらのバージョンは、[.NET Core のバージョンがサポート終了になる](https://dotnet.microsoft.com/platform/support/policy/dotnet-core)か、openSUSE のバージョンがサポート終了になるまでサポートされます。

- ✔️ は、openSUSE または .NET Core のバージョンがまだサポートされていることを示します。
- ❌ は、openSUSE または .NET Core のバージョンがその openSUSE のリリースではサポートされていないことを示しています。
- openSUSE のバージョンと .NET Core のバージョンの両方に ✔️ が付いている場合、その OS と .NET の組み合わせはサポートされています。

| openSUSE                   | .NET Core 2.1 | .NET Core 3.1 | .NET 5 Preview (手動インストールのみ) |
|----------------------------|---------------|---------------|----------------|
| ✔️ [15](linux-opensuse.md#opensuse-15-)     | ✔️ 2.1        | ✔️ 3.1        | ✔️ 5.0 Preview |

詳細については、[openSUSE での .NET Core のインストール](linux-opensuse.md)に関する記事をご覧ください。

## <a name="red-hat"></a>Red Hat

Red Hat Enterprise Linux (RHEL) では、パッケージ マネージャーとして yum (RHEL 7) と DNF (RHEL 8) が使用されます。

次の表は、RHEL 7 と RHEL 8 の両方で現在サポートされている .NET Core リリースの一覧です。 これらのバージョンは、[.NET Core のバージョンがサポート終了になる](https://dotnet.microsoft.com/platform/support/policy/dotnet-core)か、RHEL のバージョンがサポート終了になるまでサポートされます。

- ✔️ は、RHEL または .NET Core のバージョンがまだサポートされていることを示します。
- ❌ は、RHEL または .NET Core のバージョンがその RHEL のリリースではサポートされていないことを示しています。
- RHEL のバージョンと .NET Core のバージョンの両方に ✔️ が付いている場合、その OS と .NET の組み合わせはサポートされています。

| RHEL                   | .NET Core 2.1 | .NET Core 3.1 | .NET 5 Preview (手動インストールのみ) |
|--------------------------|---------------|---------------|----------------|
| ✔️ [8](linux-rhel.md#rhel-8-) | ✔️ 2.1        | ✔️ 3.1        | ✔️ 5.0 Preview |
| ✔️ [7](linux-rhel.md#rhel-7-) | ✔️ 2.1        | ✔️ 3.1        | ✔️ 5.0 Preview |

詳細については、[RHEL での .NET Core のインストール](linux-rhel.md)に関する記事をご覧ください。

## <a name="sles"></a>SLES

SLES では、パッケージ マネージャーとして zypper が使用されます。

次の表は、SLES 12 SP2 と SLES 15 の両方で現在サポートされている .NET Core リリースの一覧です。 これらのバージョンは、[.NET Core のバージョンがサポート終了になる](https://dotnet.microsoft.com/platform/support/policy/dotnet-core)か、SLES のバージョンがサポート終了になるまでサポートされます。

- ✔️ は、SLES または .NET Core のバージョンがまだサポートされていることを示します。
- ❌ は、SLES または .NET Core のバージョンがその SLES のリリースではサポートされていないことを示しています。
- SLES のバージョンと .NET Core のバージョンの両方に ✔️ が付いている場合、その OS と .NET の組み合わせはサポートされています。

| SLES                   | .NET Core 2.1 | .NET Core 3.1 | .NET 5 Preview (手動インストールのみ) |
|------------------------|---------------|---------------|----------------|
| ✔️ [15](linux-sles.md#sles-15-)     | ✔️ 2.1        | ✔️ 3.1        | ✔️ 5.0 Preview |
| ✔️ [12 SP2](linux-sles.md#sles-12-) | ✔️ 2.1        | ✔️ 3.1        | ✔️ 5.0 Preview |

詳細については、[SLES での .NET Core のインストール](linux-sles.md)に関する記事をご覧ください。

## <a name="ubuntu"></a>Ubuntu

Ubuntu では、パッケージ マネージャーとして APT (Advanced Package Tool) が使用されます。

次の表は、Ubuntu と .NET Core のサポート状態を示しています。

- ✔️ は、Ubuntu または .NET Core のバージョンがまだサポートされていることを示します。
- ❌ は、Ubuntu または .NET Core のバージョンがその Ubuntu のリリースではサポートされていないことを示しています。
- Ubuntu のバージョンと .NET Core のバージョンの両方に ✔️ が付いている場合、その OS と .NET の組み合わせはサポートされています。

| Ubuntu                   | .NET Core 2.1 | .NET Core 3.1 | .NET 5 Preview (手動インストールのみ) |
|--------------------------|---------------|---------------|----------------|
| ✔️ [20.04 (LTS)](linux-ubuntu.md#2004-) | ✔️ 2.1        | ✔️ 3.1        | ✔️ 5.0 Preview |
| ✔️ [19.10](linux-ubuntu.md#1910-)       | ✔️ 2.1        | ✔️ 3.1        | ✔️ 5.0 Preview |
| ❌ [19.04](linux-ubuntu.md#1904-)       | ✔️ 2.1        | ✔️ 3.1        | ❌ 5.0 Preview |
| ❌ [18.10](linux-ubuntu.md#1810-)       | ✔️ 2.1        | ❌ 3.1        | ❌ 5.0 Preview |
| ✔️ [18.04 (LTS)](linux-ubuntu.md#1804-) | ✔️ 2.1        | ✔️ 3.1        | ✔️ 5.0 Preview |
| ❌ [17.10](linux-ubuntu.md#1710-)       | ✔️ 2.1        | ❌ 3.1        | ❌ 5.0 Preview |
| ❌ [17.04](linux-ubuntu.md#1704-)       | ✔️ 2.1        | ❌ 3.1        | ❌ 5.0 Preview |
| ❌ [16.10](linux-ubuntu.md#1610-)       | ❌ 2.1        | ❌ 3.1        | ❌ 5.0 Preview |
| ✔️ [16.04 (LTS)](linux-ubuntu.md#1604-) | ✔️ 2.1        | ✔️ 3.1        | ✔️ 5.0 Preview |

詳細については、[Ubuntu での .NET Core のインストール](linux-ubuntu.md)に関する記事をご覧ください。

## <a name="next-steps"></a>次の手順

- [.NET Core が既にインストールされているかどうかを確認する方法](how-to-detect-installed-versions.md?pivots=os-linux)。
- [チュートリアル: Visual Studio Code を使用して新しいアプリを作成する](../tutorials/with-visual-studio-code.md)。
- [チュートリアル: NET Core アプリをコンテナー化する](../docker/build-container.md)。
