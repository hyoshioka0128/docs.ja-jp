---
ms.service: multiple
ms.date: 9/20/2018
ms.topic: include
ms.openlocfilehash: bfa7bcefff45bc325d7bba3aa2b9b3a8f0d439fa
ms.sourcegitcommit: 34dc3c0d0d0a1cc418abff259d9daa8078d00b81
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/19/2020
ms.locfileid: "81433158"
---
`azureauth.json` という名前でテキスト ファイルを作成します。 サービス プリンシパル作成時の JSON 出力を貼り付けます。

このファイルは、コードで読み取ることができるシステム上の安全な場所に保存してください。 PowerShell を使用して、`AZURE_AUTH_LOCATION` という名前の環境変数を設定します。このときに、保存したテキスト ファイルの完全なパスも指定します。次に例を示します。

```powershell
[Environment]::SetEnvironmentVariable("AZURE_AUTH_LOCATION", "C:\src\azureauth.json", "User")
```
