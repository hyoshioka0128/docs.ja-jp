---
ms.openlocfilehash: d8506893f5b3eefa6f46dc9f773e43b125ee5210
ms.sourcegitcommit: e48a54ebe62e874500a7043f6ee0b77a744d55b4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/26/2020
ms.locfileid: "80291667"
---
### <a name="azure-microsoft-prefixed-azure-integration-packages-removed"></a>Azure: Microsoft というプレフィックスが付いた Azure 統合パッケージが削除された

ASP.NET Core と Azure SDK の統合を提供する次の `Microsoft.*` パッケージは、ASP.NET Core 5.0 に含まれていません。

* [Microsoft.Extensions.Configuration.AzureKeyVault](https://www.nuget.org/packages/Microsoft.Extensions.Configuration.AzureKeyVault/)。[Azure Key Vault](/azure/key-vault/) を[構成システム](/aspnet/core/fundamentals/configuration/)に統合します。
* [Microsoft.AspNetCore.DataProtection.AzureKeyVault](https://www.nuget.org/packages/Microsoft.AspNetCore.DataProtection.AzureKeyVault/)。Azure Key Vault を [ASP.NET Core データ保護システム](/aspnet/core/security/data-protection/introduction)に統合します。
* [Microsoft.AspNetCore.DataProtection.AzureStorage](https://www.nuget.org/packages/Microsoft.AspNetCore.DataProtection.AzureStorage/)。[Azure Blob Storage](/azure/storage/blobs/) を ASP.NET Core データ保護システムに統合します。

この問題に関するディスカッションについては、[dotnet/aspnetcore#19570](https://github.com/dotnet/aspnetcore/issues/19570) を参照してください。

#### <a name="version-introduced"></a>導入されたバージョン

5.0 Preview 1

#### <a name="old-behavior"></a>以前の動作

`Microsoft.*` パッケージにより、Azure サービスと構成 API およびデータ保護 API が統合されていました。

#### <a name="new-behavior"></a>新しい動作

新しい `Azure.*` パッケージにより、Azure サービスと構成 API およびデータ保護 API が統合されます。

#### <a name="reason-for-change"></a>変更理由

この変更は、`Microsoft.*` パッケージが以下であるために行われました。

* 古いバージョンの Azure SDK を使用していました。 新しいバージョンの Azure SDK には破壊的変更が含まれていたため、単純な更新はできませんでした。
* .NET Core のリリース スケジュールに拘束されていました。 パッケージの所有権を Azure SDK チームに譲渡すると、Azure SDK が更新されるときにパッケージを更新できます。

#### <a name="recommended-action"></a>推奨アクション

ASP.NET Core 2.1 以降のプロジェクトでは、古い `Microsoft.*` パッケージを新しい `Azure.*` パッケージに置き換えます。

| 旧 | 新規作成 |
|--|--|
| `Microsoft.AspNetCore.DataProtection.AzureKeyVault` | [Azure.AspNetCore.DataProtection.Keys](https://www.nuget.org/packages/Azure.AspNetCore.DataProtection.Keys) |
| `Microsoft.AspNetCore.DataProtection.AzureStorage` | [Azure.AspNetCore.DataProtection.Blobs](https://www.nuget.org/packages/Azure.AspNetCore.DataProtection.Blobs) |
| `Microsoft.Extensions.Configuration.AzureKeyVault` | [Azure.Extensions.Configuration.Secrets](https://www.nuget.org/packages/Azure.Extensions.Configuration.Secrets) |

新しいパッケージでは、破壊的変更が含まれる新しいバージョンの Azure SDK が使用されています。 一般的な使用パターンは変更されません。 基になっている Azure SDK API での変更に対応するため、一部のオーバーロードとオプションが異なる場合があります。

古いパッケージは次のようになります。

* .NET Core 2.1 および 3.1 の有効期間中は、ASP.NET Core チームによってサポートされます。
* .NET 5 には含まれません。

プロジェクトを .NET 5 にアップグレードするときは、サポートを維持するため `Azure.*` パッケージに切り替えてください。

#### <a name="category"></a>カテゴリ

ASP.NET Core

#### <a name="affected-apis"></a>影響を受ける API

- <xref:Microsoft.Extensions.Configuration.AzureKeyVaultConfigurationExtensions.AddAzureKeyVault%2A?displayProperty=nameWithType>
- <xref:Microsoft.AspNetCore.DataProtection.AzureDataProtectionBuilderExtensions.ProtectKeysWithAzureKeyVault%2A?displayProperty=nameWithType>
- <xref:Microsoft.AspNetCore.DataProtection.AzureDataProtectionBuilderExtensions.PersistKeysToAzureBlobStorage%2A?displayProperty=nameWithType>

<!--

#### Affected APIs

- `Overload:Microsoft.Extensions.Configuration.AzureKeyVaultConfigurationExtensions.AddAzureKeyVault`
- `Overload:Microsoft.AspNetCore.DataProtection.AzureDataProtectionBuilderExtensions.ProtectKeysWithAzureKeyVault`
- `Overload:Microsoft.AspNetCore.DataProtection.AzureDataProtectionBuilderExtensions.PersistKeysToAzureBlobStorage`

-->
