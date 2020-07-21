---
ms.openlocfilehash: 7723892a33bf7dd8e475b2f696db5d9ab287e182
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84602754"
---

パッケージ マネージャーのフィードに追加されるパッケージは、変更可能な `{product}-{type}-{version}` の形式で名前が付けられます。

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

  - 3.1
  - 3.0
  - 2.1

  ダウンロードしようとしている SDK/ランタイムが Linux ディストリビューションで使用できない可能性があります。 サポートされているディストリビューションの一覧については、「[.NET Core の依存関係と要件](../linux.md)」を参照してください。

### <a name="examples"></a>使用例

- ASP.NET Core 3.1 ランタイムをインストールする: `aspnetcore-runtime-3.1`
- .NET Core 2.1 ランタイムをインストールする: `dotnet-runtime-2.1`
- .NET Core 3.1 SDK をインストールする: `dotnet-sdk-3.1`

### <a name="package-missing"></a>パッケージがない

パッケージ バージョンの組み合わせが正しくない場合は、使用できません。 たとえば、ASP.NET Core SDK がない場合、SDK コンポーネントは .NET Core SDK に含まれています。 値 `aspnetcore-sdk-2.2` は正しくありません。`dotnet-sdk-2.2` にする必要があります .NET Core によってサポートされている Linux ディストリビューションの一覧については、「[.NET Core の依存関係と要件](../linux.md)」を参照してください。
