---
title: .NET 用 Azure ライブラリの認証を理解する
description: Azure SDK for .NET を利用したさまざまな認証について説明します。
ms.date: 06/19/2020
ms.custom: azure-sdk-dotnet
ms.openlocfilehash: 5ed29d5485dc7f59bcc757c8903116edf6bd5d7d
ms.sourcegitcommit: cb27c01a8b0b4630148374638aff4e2221f90b22
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/09/2020
ms.locfileid: "86174874"
---
# <a name="authenticate-with-the-azure-sdk-for-net"></a>Azure SDK for .NET を使用した認証

## <a name="recommended-azureidentity"></a>推奨:Azure.Identity

Azure SDK for .NET の最新パッケージでは、共通の認証パッケージを使用して認証します。`Azure.Identity` です。 `Azure.Identity` の使用は、このドキュメントの後半で説明する他の認証メカニズムよりも推奨されています。 `Azure.Identity` から提供される資格情報をサポートするパッケージには、*Azure* で始まるパッケージ識別子が与えられています。 [詳細については、Azure SDK for .NET の最新リリースをご覧ください](https://azure.github.io/azure-sdk/releases/latest/index.html#net)。

プロジェクトで `Azure.Identity` を使用する方法の詳細については、[.NET 用 Azure Identity クライアント](/dotnet/api/overview/azure/identity-readme)に関するドキュメントを参照してください。

> [!TIP]
> Azure Identity を使用して Azure リソースにアクセスし、管理する例については、「[Azure Identity、Resource Management、Storage のサンプル](/samples/dotnet/samples/azure-identity-resource-management-storage/)」を参照してください。

Azure.Identity をサポートしないライブラリで認証するには、このトピックの残りを参照してください。

## <a name="access-azure-resources"></a>Azure リソースにアクセスする

Key Vault からシークレットを取得したり、Storage に BLOB を保管したりするなど、Azure リソースの操作には、さまざまな Azure サービス ライブラリで認証のための接続文字列やキーが必要になります。 たとえば、SQL Database では[標準の SQL 接続文字列](https://docs.microsoft.com/azure/azure-sql/database/connect-query-dotnet-core)が使用されます。 [CosmosDB](/azure/cosmos-db/)、[Azure Cache for Redis](/azure/azure-cache-for-redis/cache-dotnet-how-to-use-azure-redis-cache)、および [Service Bus](/azure/service-bus-messaging/service-bus-dotnet-get-started-with-queues) などの他の Azure サービスでは、サービス接続文字列が使用されます。 これらの文字列は、Azure portal、CLI、または PowerShell を使用して取得できます。 また、コード内から .NET 用 Azure 管理ライブラリを使い、リソースを照会することによって接続文字列を作成することもできます。

接続文字列の使用方法は製品によって異なります。 [こちらの Azure 製品ドキュメントをご覧ください](/azure/?product=featured)。

## <a name="manage-azure-resources"></a>Azure のリソースを管理する

[!include[Create service principal](includes/create-sp.md)]

サービス プリンシパルを作成した後は、リソースを作成および管理するサービス プリンシパルの認証に 2 つのオプションを利用できます。

どちらのオプションでも、次の NuGet パッケージをプロジェクトに追加する必要があります。

```powershell
Install-Package Microsoft.Azure.Management.Fluent
Install-Package Microsoft.Azure.Management.ResourceManager.Fluent
```

### <a name="authenticate-with-token-credentials"></a>トークン資格情報で認証を行う

最初の方法では、コードでトークン資格情報オブジェクトを作成します。 構成ファイル、レジストリ、または Azure Key Vault に、資格情報を安全に保存する必要があります。

```csharp
var credentials = SdkContext.AzureCredentialsFactory
    .FromServicePrincipal(clientId,
        clientSecret,
        tenantId,
        AzureEnvironment.AzureGlobalCloud);
```

サービス プリンシパル作成時の JSON 出力の *clientId*、*clientSecret*、および *tenantId* 値を使用します。

その後、API を使うためのエントリ ポイントとなる `Azure` オブジェクトを作成します。

```csharp
var azure = Microsoft.Azure.Management.Fluent.Azure
    .Configure()
    .Authenticate(credentials)
    .WithDefaultSubscription();
```

### <a name="file-based-authentication"></a><a name="mgmt-file"></a>ファイルベースの認証

ファイルベースの認証を使うと、プレーンテキスト ファイルにサービス プリンシパルの資格情報を格納し、ファイル システム内で保護できます。

[!include[File-based authentication](includes/file-based-auth.md)]

ファイルの内容を読み取り、API を使うためのエントリ ポイントとなる `Azure` オブジェクトを作成します。

```csharp
// pull in the location of the authentication properties file from the environment
var credentials = SdkContext.AzureCredentialsFactory
    .FromFile(Environment.GetEnvironmentVariable("AZURE_AUTH_LOCATION"));

var azure = Microsoft.Azure.Management.Fluent.Azure
    .Configure()
    .Authenticate(credentials)
    .WithDefaultSubscription();
```
