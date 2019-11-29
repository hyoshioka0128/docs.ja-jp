---
title: Wcf のバインディングとトランスポート-WCF 開発者向け gRPC
description: さまざまな WCF バインドとトランスポートが gRPC とどのように比較されるかについて説明します。
ms.date: 09/02/2019
ms.openlocfilehash: 233e3d030bc1f4450bd5cd6a7d7770486ca9e95a
ms.sourcegitcommit: f348c84443380a1959294cdf12babcb804cfa987
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/12/2019
ms.locfileid: "73966900"
---
# <a name="wcf-bindings-and-transports"></a>WCF のバインドとトランスポート

WCF には、さまざまなネットワークプロトコル、ワイヤ形式、およびその他の実装の詳細を指定するさまざまな組み込み*バインド*があります。 gRPC には、ネットワークプロトコルとワイヤ形式が1つだけあります (技術的には、ワイヤ形式は*カスタマイズできます*が、このブックの範囲を超えています)。 GRPC はほとんどの場合、最適なソリューションを提供していることがよくわかります。 ここでは、最も関連性の高い WCF バインドについて簡単に説明し、gRPC で同等のバインドと比較する方法を示します。

## <a name="nettcp"></a>Wcf-nettcp

WCF の NetTCP バインドでは、永続的な接続、小さいメッセージ、双方向メッセージングが可能ですが、.NET クライアントとサーバーの間でのみ機能します。 gRPC では同じ機能を使用できますが、複数のプログラミング言語とプラットフォームでサポートされています。 gRPC には WCF NetTCP バインディングの多くの機能がありますが、常に同じ方法で実装されるわけではありません。 たとえば、WCF では、暗号化は構成によって制御され、フレームワークで処理されます。 GRPC では、TLS 経由の HTTP/2 を使用して接続レベルで暗号化が行われます。

## <a name="http"></a>HTTP

WCF の BasicHttpBinding は通常、ワイヤ形式の SOAP を使用したテキストベースであり、NetTCP バインドと比較すると低速です。 一般に、クロスプラットフォームの相互運用性、またはインターネットインフラストラクチャ経由の接続を提供するために使用されます。 GRPC の場合と同等です。これは、メッセージのバイナリ Protobuf ワイヤ形式で、基になるトランスポート層として HTTP/2 が使用されるため、NetTCP サービスレベルのパフォーマンスを提供できますが、すべての最新のプログラミング言語とフレームワークと完全なクロスプラットフォームの相互運用性を備えています。

## <a name="named-pipes"></a>名前付きパイプ

WCF は、同じ物理マシン上のプロセス間の通信に使用する名前付きパイプのバインドを提供しました。 名前付きパイプは ASP.NET Core gRPC の最初のリリースではサポートされていません。 名前付きパイプ (および Unix ドメインソケット) のクライアントとサーバーのサポートを追加することは、将来のリリースの目的です。

## <a name="msmq"></a>MSMQ

MSMQ は専用の Windows メッセージキューです。 WCF による MSMQ へのバインドを使用すると、後でいつでも処理できるクライアントからの "火災および忘れる" 要求を行うことができます。 gRPC では、メッセージキュー機能はネイティブには提供されません。 最適な方法は、Azure Service Bus、RabbitMQ、Kafka などのメッセージングシステムを直接使用することです。 これは、メッセージをキューに直接配置するクライアント、またはメッセージをキューに入れる gRPC クライアントストリーミングサービスと共に実装できます。

## <a name="webhttpbinding"></a>WebHttpBinding

`WebGet` 属性と `WebInvoke` 属性を持つ WebHttpBinding (WCF ReST とも呼ばれます) は、現時点では、これがあまり一般的ではないときに JSON を話す可能性のある ReSTful Api を開発することを可能にしています。 そのため、WCF REST でビルドされた RESTful API を使用している場合は、通常の ASP.NET Core MVC Web API アプリケーションに移行することを検討してください。これは、gRPC に変換するのではなく、同等の機能を提供します。

>[!div class="step-by-step"]
>[前へ](wcf-endpoints-grpc-methods.md)
>[次へ](rpc-types.md)
