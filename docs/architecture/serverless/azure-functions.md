---
title: Azure Functions - サーバーレス アプリ
description: Azure Functions には、イベント ドリブンのインスタント スケール コードを提供する、複数の言語 (C#、JavaScript、Java) とプラットフォーム向けのサーバーレス機能が用意されています。
author: JEREMYLIKNESS
ms.author: jeliknes
ms.date: 04/06/2020
ms.openlocfilehash: 2dee60e3635be94a55ee26a7f04942bc59cb8dec
ms.sourcegitcommit: 8b02d42f93adda304246a47f49f6449fc74a3af4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/24/2020
ms.locfileid: "82135725"
---
# <a name="azure-functions"></a>Azure Functions 

Azure Functions によってサーバーレスのコンピューティング エクスペリエンスが提供されます。 *トリガー* (HTTP エンドポイントへのアクセスやタイマーなど) によって呼び出される関数によって、コードまたはビジネス ロジックのブロックが実行されます。 ストレージやキューなどのリソースに接続する特別な "*バインド*" も Functions でサポートされています。

![Azure Functions のロゴ](./media/azure-functions-logo.png)

現在のランタイム バージョン3.0 では、クロスプラットフォームの .NET Core 3.1 アプリケーションがサポートされています。 C# 以外に、JavaScript、F#、Java などのその他の言語がサポートされています。 ポータルで作成する関数には、豊富なスクリプト構文が用意されています。 スタンドアロン プロジェクトとして作成した関数を、完全なプラットフォームのサポートと機能を使用して展開できます。

詳細については、「[Azure Functions のドキュメント](https://docs.microsoft.com/azure/azure-functions)」を参照してください。

## <a name="programming-language-support"></a>プログラミング言語のサポート

一般提供 (GA) では、以下の言語がすべてサポートされています。

|言語      |サポートされているランタイム|
|--------------|------------------|
|**C#**        |.NET Core 3.1     |
|**JavaScript**|Node 10、12      |
|**F#**        |.NET Core 3.1     |
|**Java**      |Java 8            |
|**Python**    |Python 3.6、3.7、3.8|
|**TypeScript**|Node 10、12 (JavaScript を使用)|
|**PowerShell**|PowerShell Core 6|

詳細については、[サポートされている言語](https://docs.microsoft.com/azure/azure-functions/supported-languages)に関するページを参照してください。

## <a name="app-service-plans"></a>App Service プラン

Functions は "*App Service プラン*" によってサポートされています。 このプランでは、関数アプリによって使用されるリソースを定義します。 プランをリージョンに割り当て、使用される仮想マシンのサイズと数を決定し、価格レベルを選択することができます。 真のサーバーレス アプローチとして、関数アプリで**従量課金**プランを使用することができます。 従量課金プランでは、負荷に基づいてバックエンドが自動的にスケーリングされます。

関数アプリのもう 1 つのホスティング オプションは、[Premium プラン](https://docs.microsoft.com/azure/azure-functions/functions-premium-plan)です。 このプランでは、コールド スタートの必要がない "常時接続" インスタンスが提供され、VNet 接続などの高度な機能がサポートされて、Premium ハードウェアで実行されます。

詳細については、[App Service プラン](https://docs.microsoft.com/azure/app-service/azure-web-sites-web-hosting-plans-in-depth-overview)に関するページを参照してください。

## <a name="create-your-first-function"></a>最初の関数を作成する

関数アプリを作成するには、3 つの一般的な方法があります。

- ポータルで関数をスクリプト化します。
- Azure CLI を使用して必要なリソースを作成します。
- お気に入りの IDE を使用してローカルで関数をビルドし、Azure に発行します。

スクリプト化された関数をポータル上で作成する方法の詳細については、「[Azure portal で初めての関数を作成する](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function)」を参照してください。

Azure CLI からビルドするには、[Azure CLI を使用して初めての関数を作成する](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function-azure-cli)方法に関するページを参照してください。

Visual Studio で関数を作成するには、「[Visual Studio を使用して初めての関数を作成する](https://docs.microsoft.com/azure/azure-functions/functions-create-your-first-function-visual-studio)」を参照してください。

## <a name="understand-triggers-and-bindings"></a>トリガーとバインドについて

関数は "*トリガー*" によって呼び出されます。関数に設定できるトリガーは 1 つだけです。 関数を呼び出すだけでなく、特定のトリガーにはバインドとしての機能もあります。 トリガーに加えて、複数のバインドを定義することもできます。 "*バインド*" は、宣言によってデータをコードに接続する方法です。 渡される場合 (入力) と、データを受け取る場合 (出力) があります。 トリガーとバインドを使用すると、関数を使用した作業が簡単になります。 バインドによって、データベースまたはファイル システムの接続を手動で作成するオーバーヘッドが解消されます。 バインドに必要なすべての情報は、*functions.json* というスクリプト用の特別なファイル内に格納されます。または、コード内で属性を使用して宣言します。

次のような一般的なトリガーがあります。

- Blob Storage: ストレージ内でファイルまたはフォルダーがアップロードまたは変更されたときに、関数を呼び出します。
- HTTP: REST API のように関数を呼び出します。
- キュー: キューに項目が存在する場合に関数を呼び出します。
- タイマー: 関数を定期的に呼び出します。

バインドの例を次に示します。

- CosmosDB: データベースに簡単に接続して、ファイルを読み込んだり保存したりできます。
- Table Storage: 関数アプリからキー/値のストレージを操作します。
- Queue Storage: キューからの項目の取得、または新しい項目のキューへの配置を簡単に行うことができます。

次の *functions.json* ファイルの例では、トリガーとバインドを定義しています。

```json
{
  "bindings": [
    {
      "name": "myBlob",
      "type": "blobTrigger",
      "direction": "in",
      "path": "images/{name}",
      "connection": "AzureWebJobsStorage"
    },
    {
      "name": "$return",
      "type": "queue",
      "direction": "out",
      "queueName": "images",
      "connection": "AzureWebJobsStorage"
    }
  ],
  "disabled": false
}
```

この例では、`images` コンテナー内での BLOB ストレージに対する変更によって関数がトリガーされます。 ファイルの情報が渡され、トリガーはバインドとしても機能します。 `images` という名前のキューに情報を格納するための別のバインドが存在します。

関数の C# スクリプトを次に示します。

```csharp
public static string Run(Stream myBlob, string name, TraceWriter log)
{
    log.Info($"C# Blob trigger function Processed blob\n Name:{name} \n Size: {myBlob.Length} Bytes");
    return name;
}
```

この例は、BLOB ストレージ内の変更またはアップロードされたファイルの名前を取得し、後で処理するためにキューに配置する単純な関数です。

トリガーとバインドの完全な一覧については、「[Azure Functions でのトリガーとバインドの概念](https://docs.microsoft.com/azure/azure-functions/functions-triggers-bindings)」を参照してください。

>[!div class="step-by-step"]
>[前へ](azure-serverless-platform.md)
>[次へ](application-insights.md)
