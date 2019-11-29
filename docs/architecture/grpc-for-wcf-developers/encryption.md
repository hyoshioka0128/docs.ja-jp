---
title: 暗号化とネットワークセキュリティ-WCF 開発者向けの gRPC
description: GRPC でのネットワークセキュリティと暗号化に関する注意事項
ms.date: 09/02/2019
ms.openlocfilehash: fd993a2d75e97011c6c92cee02c24c5358a211ad
ms.sourcegitcommit: f348c84443380a1959294cdf12babcb804cfa987
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/12/2019
ms.locfileid: "73967774"
---
# <a name="encryption-and-network-security"></a>暗号化とネットワークセキュリティ

WCF のネットワークセキュリティモデルは、HTTPS または TLS over TCP を使用したトランスポートレベルのセキュリティ、および WS-SECURITY 仕様を使用して個々のメッセージを暗号化するメッセージレベルのセキュリティなど、広範で複雑なものです。

gRPC は、通常の TLS 証明書を使用してセキュリティで保護できる、基になる HTTP/2 プロトコルに安全なネットワークを残します。

Web ブラウザーは、HTTP/2 の TLS 接続を使用することを主張していますが、を含むほとんどのプログラム用クライアントです。NET の `HttpClient`では、暗号化されていない接続を介して HTTP/2 を使用できます。 `HttpClient` に*は*既定で暗号化が必要ですが、<xref:System.AppContext> スイッチを使用して上書きできます。

```csharp
AppContext.SetSwitch("System.Net.Http.SocketsHttpHandler.Http2UnencryptedSupport", true);
```

パブリック Api の場合、TLS 接続を常に使用し、適切な SSL 機関からサービスに有効な証明書を提供する必要があります。 現在、最新の自動 SSL 証明書を提供し、ほとんどのホスティングインフラストラクチャでは、一般的なプラグインまたは拡張機能[によって](https://letsencrypt.org)、標準のプラグインまたは拡張機能をサポートしています。

企業ネットワーク全体の内部サービスについても、TLS を使用して、gRPC サービスとの間のネットワークトラフィックをセキュリティで保護することを検討する必要があります。

Kubernetes や Docker の群れなど、クラスター内のマイクロサービス間の通信は、通常、コンテナーネットワークレイヤーによって自動的に暗号化されます。そのため、このようなクラスターでのみ実行されるサービスに TLS を実装する必要はありません。 詳細については、次の章の「サービスメッシュ」セクションを参照してください。

Kubernetes で実行されているサービス間で明示的な TLS を使用する必要がある場合は、クラスター内の証明機関と、証明[書マネージャーのような](https://docs.cert-manager.io/en/latest/)証明書マネージャーコントローラーを使用して、展開時にサービスに自動的に証明書を割り当てることを検討してください。

>[!div class="step-by-step"]
>[前へ](channel-credentials.md)
>[次へ](grpc-in-production.md)
