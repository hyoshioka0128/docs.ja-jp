---
title: Windows、Linux、および macOS に .NET Core ランタイムをインストールする - .NET Core
description: Windows、Linux、および macOS に .NET Core をインストールする方法について説明します。 .NET Core アプリの実行に必要な依存関係を確認します。
author: thraka
ms.author: adegeo
ms.date: 12/04/2019
ms.custom: updateeachrelease
zone_pivot_groups: operating-systems-set-one
ms.openlocfilehash: 8f4a895ad66dea3063a32f785e4c521196266978
ms.sourcegitcommit: a4f9b754059f0210e29ae0578363a27b9ba84b64
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/05/2019
ms.locfileid: "74998889"
---
# <a name="install-the-net-core-runtime"></a>.NET Core ランタイムのインストール

この記事では、.NET Core ランタイムをダウンロードしてインストールする方法について説明します。 .Net Core ランタイムは、.NET Core で作成されたアプリを実行するために使用されます。

::: zone pivot="os-windows"

## <a name="install-with-an-installer"></a>インストーラーを使用したインストール

Windows には、.NET Core 3.1 ランタイムのインストールに使用できるスタンドアロン インストーラーが用意されています。

- [x64 (64 ビット) CPU](https://dotnet.microsoft.com/download/dotnet-core/3.1)
- [x86 (32 ビット) CPU](https://dotnet.microsoft.com/download/dotnet-core/3.1)

::: zone-end

::: zone pivot="os-macos"

## <a name="install-with-an-installer"></a>インストーラーを使用したインストール

macOS には、.NET Core 3.1 ランタイムのインストールに使用できるスタンドアロン インストーラーが用意されています。

- [x64 (64 ビット) CPU](https://dotnet.microsoft.com/download/dotnet-core/3.1)

::: zone-end

::: zone pivot="os-linux"

## <a name="install-with-a-package-manager"></a>パッケージ マネージャーを使用したインストール

多くの一般的な Linux パッケージ マネージャーを使用して .NET Core ランタイムをインストールできます。 詳細については、[Linux パッケージ マネージャー - .NET Core のインストール](linux-package-manager-rhel7.md)に関するページを参照してください。

::: zone-end

::: zone pivot="os-windows"

## <a name="install-with-powershell-automation"></a>PowerShell オートメーションを使用したインストール

[dotnet-install スクリプト](../tools/dotnet-install-script.md)は、ランタイムの自動化および管理者以外によるインストールに使用されます。 スクリプトは、[dotnet-install スクリプト参照ページ](../tools/dotnet-install-script.md)からダウンロードできます。

スクリプトでは、既定で最新の [長期サポート (LTS)](https://dotnet.microsoft.com/platform/support/policy/dotnet-core) バージョン (.NET Core 3.1) がインストールされます。 `Channel` スイッチを指定することで、特定のリリースを選択できます。 ランタイムをインストールするには、`Runtime` スイッチを含めます。 それ以外の場合は、スクリプトによって [SDK](sdk.md) がインストールされます。

```powershell
dotnet-install.ps1 -Channel 3.1 -Runtime aspnetcore
```

> [!NOTE]
> 上のコマンドでは、互換性を最大限に高めるために ASP.NET Core ランタイムをインストールします。 ASP.NET Core ランタイムには、標準の .NET Core ランタイムも含まれています。

::: zone-end

::: zone pivot="os-linux,os-macos"

## <a name="install-with-bash-automation"></a>bash オートメーションを使用したインストール

[dotnet-install スクリプト](../tools/dotnet-install-script.md)は、ランタイムの自動化および管理者以外によるインストールに使用されます。 スクリプトは、[dotnet-install スクリプト参照ページ](../tools/dotnet-install-script.md)からダウンロードできます。

スクリプトでは、既定で最新の [長期サポート (LTS)](https://dotnet.microsoft.com/platform/support/policy/dotnet-core) バージョン (.NET Core 3.1) がインストールされます。 `current` スイッチを指定することで、特定のリリースを選択できます。 ランタイムをインストールするには、`runtime` スイッチを含めます。 それ以外の場合は、スクリプトによって [SDK](sdk.md) がインストールされます。

```bash
./dotnet-install.sh --current 3.1 --runtime aspnetcore
```

> [!NOTE]
> 上のコマンドでは、互換性を最大限に高めるために ASP.NET Core ランタイムをインストールします。 ASP.NET Core ランタイムには、標準の .NET Core ランタイムも含まれています。

::: zone-end

## <a name="all-net-core-downloads"></a>すべての .NET Core のダウンロード

次のいずれかのリンクを使用して、.NET Core を直接ダウンロードしてインストールすることができます。

- [.NET Core 3.1 のダウンロード](https://dotnet.microsoft.com/download/dotnet-core/3.1)
- [.NET Core 3.0 のダウンロード](https://dotnet.microsoft.com/download/dotnet-core/3.0)
- [.NET Core 2.2 のダウンロード](https://dotnet.microsoft.com/download/dotnet-core/2.2)
- [.NET Core 2.1 のダウンロード](https://dotnet.microsoft.com/download/dotnet-core/2.1)

## <a name="docker"></a>Docker

コンテナーを使用すると、アプリケーションをホスト システムの他の部分から簡単に分離できます。 同じコンピューター上のコンテナーでは、カーネルだけが共有され、アプリケーションに提供されたリソースが使用されます。

.NET Core は Docker コンテナー内で実行できます。 公式の .NET Core Docker イメージは Microsoft Container Registry (MCR) に公開され、[Microsoft .NET Core の Docker Hub リポジトリ](https://hub.docker.com/_/microsoft-dotnet-core/)で見つけられます。 各リポジトリには、.NET (SDK またはランタイム) と自分が使用できる OS のさまざまな組み合わせのイメージが含まれています。

Microsoft は、特定のシナリオに対応したイメージを用意しています。 たとえば、[ASP.NET Core リポジトリ](https://hub.docker.com/_/microsoft-dotnet-core-aspnet/)には、運用環境での ASP.NET Core アプリの実行用にビルドされたイメージが用意されています。

Docker コンテナー内で .NET Core を使用する方法の詳細については、「[.NET および Docker の概要](../docker/introduction.md)」と[サンプル](https://github.com/dotnet/dotnet-docker/blob/master/samples/README.md)に関するページを参照してください。

## <a name="next-steps"></a>次の手順

- [.NET Core が既にインストールされているかどうかを確認する方法](how-to-detect-installed-versions.md)。
