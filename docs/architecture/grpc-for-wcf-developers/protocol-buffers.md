---
title: プロトコルバッファー-WCF 開発者向け gRPC
description: GRPC ネットワークに使用されるプロトコルバッファーワイヤ形式の概要。
ms.date: 09/09/2019
ms.openlocfilehash: dbe8cb43475cfeec19051daf68452ef86269372f
ms.sourcegitcommit: f348c84443380a1959294cdf12babcb804cfa987
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/12/2019
ms.locfileid: "73967287"
---
# <a name="protocol-buffers"></a>プロトコルバッファー

gRPC サービスは、WCF のデータコントラクトと同様に、データを*プロトコルバッファー (Protobuf) メッセージ*として送受信します。 Protobuf は、XML や JSON などの人間が判読できる形式のオーバーヘッドを発生させることなく、マシン用の構造化データを読み書きするための効率的な方法です。

この章では、Protobuf のしくみと、独自の Protobuf メッセージの定義方法について説明します。

## <a name="how-protobuf-works"></a>Protobuf のしくみ

WCF のデータコントラクトを含むほとんどの .NET オブジェクトのシリアル化手法は、リフレクションを使用して実行時にオブジェクト構造を分析することで機能します。 これに対し、ほとんどの Protobuf ライブラリでは、`.proto` ファイルで専用言語 (*プロトコルバッファー言語*) を使用して、構造を事前に定義する必要があります。 このファイルは、.NET、Java、C/C++、JavaScript など、サポートされているプラットフォームのいずれかのコードを生成するために、コンパイラによって使用されます。 Protobuf コンパイラ (`protoc`) は Google によって管理されますが、代替の実装は使用できます。 生成されたコードは効率的で、データの高速なシリアル化と逆シリアル化のために最適化されています。

Protobuf wire 形式自体はバイナリエンコードです。これは、メッセージを表すために使用されるバイト数を最小限に抑えるために、いくつかの巧妙な手法を使用します。 Protobuf を使用するためにバイナリエンコード形式の知識は必要ありませんが、関心がある場合は[、プロトコルバッファーの web サイト](https://developers.google.com/protocol-buffers/docs/encoding)で詳細を確認できます。

>[!div class="step-by-step"]
>[前へ](why-grpc.md)
>[次へ](protobuf-messages.md)
