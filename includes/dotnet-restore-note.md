---
ms.openlocfilehash: e140b375f4f289df895052aa093f03f381d62488
ms.sourcegitcommit: 73aa9653547a1cd70ee6586221f79cc29b588ebd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "82102744"
---
[`dotnet restore`](~/docs/core/tools/dotnet-restore.md) を実行する必要がなくなりました。復元を必要とするすべてのコマンド (`dotnet new`、`dotnet build`、`dotnet run`、`dotnet test`、`dotnet publish`、`dotnet pack` など) によって暗黙的に実行されるためです。 暗黙的な復元を無効にするには、`--no-restore` オプションを使用します。

[Azure DevOps Services の継続的インテグレーション ビルド](https://docs.microsoft.com/azure/devops/build-release/apps/aspnet/build-aspnet-core)などの、明示的な復元が意味のある一部のシナリオや、復元が行われるタイミングを明示的に制御する必要があるビルド システムでは、`dotnet restore` は引き続き有用なコマンドです。

NuGet フィードの管理方法については、[`dotnet restore` のドキュメント](../docs/core/tools/dotnet-restore.md)をご覧ください。
