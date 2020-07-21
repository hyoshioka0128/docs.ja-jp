---
title: エラー処理 - WCF 開発者用 gRPC
description: gRPC でのエラー処理に関するトピック。 最も一般的に使用されるステータスコードの表が含まれています。
ms.date: 09/02/2019
ms.openlocfilehash: 64a2355a8bd608c074f9bc420312b23aba0c1fb2
ms.sourcegitcommit: e3cbf26d67f7e9286c7108a2752804050762d02d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/09/2020
ms.locfileid: "80988948"
---
# <a name="error-handling"></a>エラー処理

Windows 通信ファウンデーション<xref:System.ServiceModel.FaultException%601>(WCF) は、SOAP フォールト標準のサポートを含む詳細なエラー情報を提供するために使用および[FaultContract](xref:System.ServiceModel.FaultContractAttribute)を使用します。

残念ながら、現在のバージョンの gRPC には WCF で見られる高度な機能が欠けており、単純な状態コードとメタデータに基づく組み込みのエラー処理のみが制限されています。 次の表は、最も一般的に使用されるステータスコードのクイックガイドです。

| status code | 問題 |
| ----------- | ------- |
| `GRPC_STATUS_UNIMPLEMENTED` | メソッドが書かれていません。 |
| `GRPC_STATUS_UNAVAILABLE` | サービス全体に問題があります。 |
| `GRPC_STATUS_UNKNOWN` | 無効な応答です。 |
| `GRPC_STATUS_INTERNAL` | エンコード/デコードに問題があります。 |
| `GRPC_STATUS_UNAUTHENTICATED` | 認証に失敗しました。 |
| `GRPC_STATUS_PERMISSION_DENIED` | 承認に失敗しました。 |
| `GRPC_STATUS_CANCELLED` | 呼び出しは、通常、呼び出し元によって取り消されました。 |

## <a name="raise-errors-in-aspnet-core-grpc"></a>ASP.NETコア gRPC でエラーを発生させる

ASP.NET Core gRPC サービスは`RpcException`、同じプロセスにあるかのようにクライアントがキャッチできる をスローすることでエラー応答を送信できます。 には`RpcException`、ステータス コードと説明を含める必要があり、オプションでメタデータと長い例外メッセージを含めることができます。 メタデータを使用すると、WCF エラーに対する追加データを`FaultContract`オブジェクトが伝送する方法と同様に、サポート データを送信できます。

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

## <a name="catch-errors-in-grpc-clients"></a>gRPC クライアントでエラーをキャッチする

WCF クライアントがエラーを<xref:System.ServiceModel.FaultException%601>キャッチできるのと同様に、gRPC`RpcException`クライアントはエラーを処理するをキャッチできます。 ジェネリック`RpcException`型ではないため、異なるブロックで異なるエラータイプをキャッチすることはできません。 ただし、C# の*例外フィルター*機能を使用して、次`catch`の例に示すように、さまざまな状態コードに対して個別のブロックを宣言できます。

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
> エラーの追加メタデータを提供する場合は、API ドキュメントまたはファイル内のコメントに関連するキーと値を必ず文書化`.proto`してください。

## <a name="grpc-richer-error-model"></a>gRPC リッチ エラー モデル

Google は WCF の[FaultContract](xref:System.ServiceModel.FaultContractAttribute)に似た[より豊富なエラー モデル](https://cloud.google.com/apis/design/errors#error_model)を開発しましたが、このモデルはまだ C# ではサポートされていません。 現在のところ、Go、Java、Python、および C++ でのみ使用できます。

>[!div class="step-by-step"]
>[前へ](metadata.md)
>[次へ](ws-protocols.md)
