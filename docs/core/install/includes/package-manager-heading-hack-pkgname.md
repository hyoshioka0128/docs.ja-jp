---
ms.openlocfilehash: 7a55641b3673dc4d8d9b328f0de99b7247ca51d4
ms.sourcegitcommit: 9a39f2a06f110c9c7ca54ba216900d038aa14ef3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/23/2019
ms.locfileid: "74998799"
---

パッケージ マネージャーのフィードに追加されたパッケージは、`{product}-{type}-{version}` のハック可能な形式で名前が付けられます。

- **product**\
インストールする .NET 製品の種類。 有効なオプションは次のとおりです。

  - dotnet
  - aspnetcore

- **type**\
SDK またはランタイムを選択します。 有効なオプションは次のとおりです。

  - SDK
  - ランタイム

- **version**\
インストールする SDK またはランタイムのバージョン。 この記事では常に、サポートされている最新バージョンの手順について説明します。 有効なオプションは、次のようなリリース バージョンです。

  - 3.0
  - 2.2
  - 2.1

### <a name="examples"></a>使用例

- .NET Core 2.2 SDK をインストールする: `dotnet-sdk-2.2`
- ASP.NET Core 3.0 ランタイムをインストールする: `aspnetcore-runtime-3.0`
- .NET Core 2.1 ランタイムをインストールする: `dotnet-runtime-2.1`

### <a name="troubleshoot"></a>トラブルシューティング

パッケージの組み合わせが機能しない場合は、使用できません。 たとえば、ASP.NET Core SDK がない場合、SDK コンポーネントは .NET Core SDK に含まれています。 値 `aspnetcore-sdk-2.2` は正しくありません。これは、`dotnet-sdk-2.2` である必要があります
