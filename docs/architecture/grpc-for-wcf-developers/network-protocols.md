---
title: ネットワークプロトコル-WCF 開発者向け gRPC
description: GRPC ネットワークプロトコルの概要について説明します。
ms.date: 09/02/2019
ms.openlocfilehash: 5e837738bd345608ca7119d04c9221acb220c276
ms.sourcegitcommit: f348c84443380a1959294cdf12babcb804cfa987
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/12/2019
ms.locfileid: "73971702"
---
# <a name="network-protocols"></a>ネットワーク プロトコル

WCF とは異なり、gRPC はネットワークのベースとして HTTP/2 を使用します。 これは、HTTP/1.1 でのみ動作する WCF および SOAP よりも大きな利点を提供します。 GRPC の使用を検討している開発者にとって、HTTP/2 の代替手段がない場合は、HTTP/2 の詳細を確認し、gRPC を使用するためのその他のメリットを特定することが理想的です。

2015の Internet Engineering Task Force によってリリースされた HTTP/2 は、既に Google によって使用されていた実験的な SPDY プロトコルから派生しました。 これは、HTTP/1.1 よりも効率的で高速かつ安全になるように設計されています。

## <a name="key-features-of-http2"></a>HTTP/2 の主な機能

次の一覧は、HTTP/2 の主な機能と利点の一部を示しています。

### <a name="binary-protocol"></a>バイナリプロトコル

要求/応答サイクルでは、テキストコマンドが不要になりました。 これにより、コマンドの実装が簡略化され、高速化されます。 具体的には、データの解析が高速で、使用するメモリが少なくなるため、ネットワーク待機時間が短縮されます。

### <a name="streams"></a>ストリーム

ストリームを使用すると、送信側と受信側の間の有効期間の長い接続を作成できます。これにより、複数のメッセージやフレームを非同期に送信できます。 複数のストリームは、1つの HTTP/2 接続で個別に操作できます。

### <a name="request-multiplexing-over-a-single-tcp-connection"></a>1つの TCP 接続で多重化を要求する

この機能は、HTTP/2 の最も重要なイノベーションの1つです。 データに対して複数の並列要求を許可することにより、1台のサーバーから web ファイルを同時にダウンロードできるようになりました。 Web サイトの読み込みが速くなり、最適化の必要性が軽減されます。 先行 (ホル) ブロック。前の要求が完了するまで送信されるのを待機する必要があります (ただし、TCP トランスポートレベルでは、ホルブロックが引き続き発生する可能性があります)。

### <a name="nettcp-like-performance-cross-platform"></a>NetTCP に似たパフォーマンス、クロスプラットフォーム

基本的に、gRPC と HTTP/2 の組み合わせにより、開発者は少なくとも WCF 用の NetTCP バインディングの同等の速度と効率を実現します。また、場合によっては、速度と効率が向上します。 ただし、NetTCP とは異なり、gRPC over HTTP/2 は .NET アプリケーションに制限されていません。

>[!div class="step-by-step"]
>[前へ](interface-definition-language.md)
>[次へ](why-grpc.md)
