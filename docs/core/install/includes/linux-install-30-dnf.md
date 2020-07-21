---
ms.openlocfilehash: f9ea0ee6402187365cec5cdced1617ee2ae66bed
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84602820"
---

### <a name="install-the-sdk"></a>SDK のインストール

.NET Core SDK を使用すると、.NET Core を使用してアプリを開発できます。 .NET Core SDK をインストールする場合、対応するランタイムをインストールする必要はありません。 .NET Core SDK をインストールするには、次のコマンドを実行します。

```bash
sudo dnf install dotnet-sdk-3.0
```

### <a name="install-the-runtime"></a>ランタイムをインストールする

.NET Core ランタイムを使用すると、ランタイムを含まない .NET Core を使用して作成されたアプリを実行できます。 次のコマンドを実行すると、.NET Core の最も互換性の高いランタイムである ASP.NET Core ランタイムがインストールされます。 ご利用のターミナルで、次のコマンドを実行します。

```bash
sudo dnf install aspnetcore-runtime-3.0
```

ASP.NET Core ランタイムの代替手段として、ASP.NET Core サポートを含まない .NET Core ランタイムをインストールできます。それには、前述のコマンドの `aspnetcore-runtime-3.0` を `dotnet-runtime-3.0` で置き換えます。

```bash
sudo dnf install dotnet-runtime-3.0
```
