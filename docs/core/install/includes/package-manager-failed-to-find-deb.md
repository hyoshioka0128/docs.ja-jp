---
ms.openlocfilehash: 7d398df060c031ae891218b82a2712d74f4c33b7
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84602748"
---

"**パッケージ {netcore-package} が見つかりません**" のようなエラー メッセージが表示される場合は、次のコマンドを実行します。

次の一連のコマンドには、2 つのプレースホルダーがあります。

- `{dotnet-package}`\
これは、`aspnetcore-runtime-3.1` など、インストールする .NET Core パッケージを表します。 これは、次の `sudo apt-get install` コマンドで使用されます。

- `{os-version}`\
これは、使用している Linux のバージョンを表します。 これは、次の `wget` コマンドで使用されます。

パッケージ リストを消去してみてください。

```bash
sudo dpkg --purge packages-microsoft-prod && sudo dpkg -i packages-microsoft-prod.deb
sudo apt-get update
sudo apt-get install {dotnet-package}
```

それでも解決しない場合は、次のコマンドを使用して手動インストールを実行できます。
