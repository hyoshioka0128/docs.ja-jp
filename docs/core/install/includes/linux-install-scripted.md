---
ms.openlocfilehash: fb78e1439a680a8dbb9fc0eb8afdeee3efef7ead
ms.sourcegitcommit: 5fd4696a3e5791b2a8c449ccffda87f2cc2d4894
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2020
ms.locfileid: "84768399"
---

[dotnet-install スクリプト](../../tools/dotnet-install-script.md)は、**SDK** および**ランタイム**のインストールの自動化および管理者以外によるインストールのために使用されます。 このスクリプトは <https://dot.net/v1/dotnet-install.sh> からダウンロードできます。

スクリプトでは、最新の SDK の[長期サポート (LTS)](https://dotnet.microsoft.com/platform/support/policy/dotnet-core) バージョン (.NET Core 3.1) が既定でインストールされます。 (LTS) バージョンではない場合がある現在のリリースをインストールするには、`-c Current` パラメーターを使用します。

```bash
./dotnet-install.sh -c Current
```

SDK の代わりに .NET Core ランタイムをインストールするには、`--runtime` パラメーターを使用します。

```bash
./dotnet-install.sh -c Current --runtime aspnetcore
```

特定のバージョンをインストールするには、`-c` パラメーターを変更して特定のバージョンを指定します。 次のコマンドでは、.NET Core SDK 3.1 がインストールされます。

```bash
./dotnet-install.sh -c 3.1
```

詳細については、「[dotnet-install スクリプト リファレンス](../../tools/dotnet-install-script.md)」をご覧ください。
