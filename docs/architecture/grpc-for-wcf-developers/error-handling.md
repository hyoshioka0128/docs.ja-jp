---
title: エラー処理-WCF 開発者向け gRPC
description: 記述予定
ms.date: 09/02/2019
ms.openlocfilehash: 2c44bd9264c877a7c7a86c115b6da9f759006016
ms.sourcegitcommit: f348c84443380a1959294cdf12babcb804cfa987
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/12/2019
ms.locfileid: "73967793"
---
# <a name="error-handling"></a>エラー処理

WCF は `FaultException<T>` と `FaultContract` を使用して、SOAP Fault standard のサポートなど、詳細なエラー情報を提供します。

残念ながら、現在のバージョンの gRPC では、WCF での洗練された機能が不足しており、単純なステータスコードとメタデータに基づいて組み込まれたエラー処理は限られています。 次の表に、最も一般的に使用されるステータスコードの簡単なガイドを示します。

| 状態コード | Problem |
| ----------- | ------- |
| `GRPC_STATUS_UNIMPLEMENTED` | メソッドが書き込まれていません。 |
| `GRPC_STATUS_UNAVAILABLE` | サービス全体に問題があります。 |
| `GRPC_STATUS_UNKNOWN` | 無効な応答です。 |
| `GRPC_STATUS_INTERNAL` | エンコード/デコードに問題があります。 |
| `GRPC_STATUS_UNAUTHENTICATED` | 認証に失敗しました。 |
| `GRPC_STATUS_PERMISSION_DENIED` | 承認に失敗しました。 |
| `GRPC_STATUS_CANCELLED` | 呼び出しはキャンセルされました。通常は呼び出し元によって行われます。 |

## <a name="raising-errors-in-aspnet-core-grpc"></a>ASP.NET Core gRPC でエラーが発生する

ASP.NET Core gRPC サービスは、`RpcException`をスローすることによってエラー応答を送信することができます。これは、同じプロセスにあるかのようにクライアントからキャッチできます。 `RpcException` には、状態コードと説明を含める必要があります。また、必要に応じて、メタデータと長い例外メッセージを含めることができます。 メタデータを使用して、サポートデータを送信することができます。これは、`FaultContract` オブジェクトが WCF エラーに対して追加データを伝達する方法と似ています。

```csharp
public async Task<GetPortfolioResponse> GetPortfolio(GetPortfolioRequest request, ServerCallContext context)
{
    var user = context.GetHttpContext().User;
    if (!ValidateUser(user))
    {
        var metadata = new Metadata
        {
            { "User", user.Identity.Name }
        };
        throw new RpcException(new Status(StatusCode.PermissionDenied, "Permission denied"), metadata);
    }
}
```

## <a name="catching-errors-in-grpc-clients"></a>GRPC クライアントでのエラーのキャッチ

WCF クライアントが <xref:System.ServiceModel.FaultException%601> エラーをキャッチできるのと同様に、gRPC クライアントは、エラーを処理するための `RpcException` をキャッチできます。 `RpcException` はジェネリック型ではないため、異なるブロックでさまざまなエラーの種類をキャッチすることC#はできませんが、次の例に示すように、の*例外フィルター*機能を使用して、さまざまな状態コードに対して個別の `catch` ブロックを宣言することができます。

```csharp
try
{
    var portfolio = await client.GetPortfolioAsync(new GetPortfolioRequest { Id = id });
}
catch (RpcException ex) when (ex.StatusCode == StatusCode.PermissionDenied)
{
    var userEntry = ex.Trailers.FirstOrDefault(e => e.Key == "User");
    Console.WriteLine($"User '{userEntry.Value}' does not have permission to view this portfolio.");
}
catch (RpcException)
{
    // Handle any other error type ...
}
```

> [!IMPORTANT]
> エラーのために追加のメタデータを指定する場合は、API のドキュメント、または `.proto` ファイルのコメントで、関連するキーと値を必ず文書化してください。

## <a name="grpc-richer-error-model"></a>gRPC の豊富なエラーモデル

今後、Google は、WCF の[Faultcontract](xref:System.ServiceModel.FaultContractAttribute)のようなより[豊富なエラーモデル](https://cloud.google.com/apis/design/errors#error_model)を開発しましたがC# 、ではまだサポートされていません。 現在は、ゴー、Java、Python およびC++でのみ使用できますが、のC#サポートは来年に予定されています。

>[!div class="step-by-step"]
>[前へ](metadata.md)
>[次へ](ws-protocols.md)
