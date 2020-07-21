---
title: メッセージ エンコーディング
ms.date: 03/30/2017
ms.assetid: f30ee941-aca9-4c67-82a5-421568496f07
ms.openlocfilehash: 8e5a71095ba62e0e2e6592c8b7b83b67602ef7e7
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "69931591"
---
# <a name="message-encoding"></a>メッセージ エンコーディング
エンコーディングは、Unicode 文字のセットをバイト シーケンスに変換するプロセスです。 デコードは、その逆のプロセスです。 WCF (Windows Communication Foundation) には、SOAP メッセージのエンコードとして、テキスト、バイナリ、および MTOM (Message Transmission Optimization Mechanism) の 3 種類があります。  
  
 `binaryMessageEncoding` 構成セクションでは、バイナリ ベースの XML メッセージに使用される文字エンコーディングおよびメッセージ バージョン管理が指定されます。 バイナリ メッセージ エンコーダーは、ネットワーク上で Windows Communication Foundation (WCF) メッセージをバイナリにエンコードします。 このエンコーディングによりメッセージ転送は非常に高速になりますが、WS-* 標準に基づいた相互運用性は失われます。  
  
 `mtomMessageEncoding` 構成セクションでは、Message Transmission Optimization Mechanism (MTOM) エンコーディングを使用したメッセージの文字エンコーディングおよびメッセージ バージョン管理が指定されます。 (MTOM) は、Windows Communication Foundation (WCF) メッセージでバイナリ データを送信する効率的な技術です。 MTOM エンコーダーは、効率と相互運用性のバランスをとろうとします。 MTOM エンコーディングは、ほとんどの XML をテキスト形式で転送しますが、大きいサイズのバイナリ データ ブロックはテキストに変換せずにそのまま転送することによって最適化します。  
  
 `textMessageEncoding` 構成セクションは、ネットワーク上でテキストベースのメッセージの作成に使用されるテキスト エンコーダーを指定します。 このエンコーダーにより生成されるメッセージは、WS-* ベースの相互運用に適しています。 Web サービスまたは Web サービス クライアントは、一般に、テキスト形式の XML を認識できます。 ただし、バイナリ データの大きいブロックをテキストとして送信することは、XML メッセージをエンコードする最も効率の悪い方法です。  
  
## <a name="see-also"></a>関連項目

- <xref:System.ServiceModel.Channels.CustomBinding>
- <xref:System.ServiceModel.Channels.MessageEncodingBindingElement>
- [バインド](../../../wcf/bindings.md)
- [バインディングの拡張](../../../wcf/extending/extending-bindings.md)
- [カスタム バインディング](../../../wcf/extending/custom-bindings.md)
- [\<customBinding>](custombinding.md)
- [メッセージ エンコーダーを選択する](../../../wcf/feature-details/choosing-a-message-encoder.md)
