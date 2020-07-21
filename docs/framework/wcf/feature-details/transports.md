---
title: Windows Communication Foundation のトランスポート
ms.date: 03/30/2017
helpviewer_keywords:
- transports [WCF]
- WCF, transports
- Windows Communication Foundation, transports
ms.assetid: 005c894b-af70-48aa-a1c1-c99338083c27
ms.openlocfilehash: 077d63d8038b245a68083611897c1e6c68971071
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84598672"
---
# <a name="transports-in-windows-communication-foundation"></a>Windows Communication Foundation のトランスポート
トランスポート層は、チャネル スタックの最も低いレベルにあります。 Windows Communication Foundation (WCF) で使用される主なトランスポートは、HTTP、HTTPS、TCP、および名前付きパイプです。 このセクションのトピックでは、このようなトランスポートの選択、トランスポートの構成、およびチューニング プロパティの設定について説明します。  
  
 WCF には、追加のトランスポートが含まれています。 メッセージキュー (MSMQ) トランスポートの詳細については、「[キューと信頼できるセッション](queues-and-reliable-sessions.md)」を参照してください。 ピアツーピアトランスポートの詳細については、「[ピアツーピアネットワーク](peer-to-peer-networking.md)」を参照してください。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [トランスポートの選択](choosing-a-transport.md)  
 3 つの主なトランスポートについて説明し、そのうちの 1 つを選択する際の考慮事項を示します。  
  
 [メッセージ エンコーダーを選択する](choosing-a-message-encoder.md)  
 メッセージ エンコーディングのバインド要素を選択する際に考慮する必要のある要因について説明します。  
  
 [メッセージ転送ストリーミング](streaming-message-transfer.md)  
 ストリーミングが行われるようにトランスポート層を構成する方法について説明します。  
  
 [HTTP および HTTPS の構成](configuring-http-and-https.md)  
 HTTP および HTTPS トランスポート バインディング要素の構成方法について説明します。  
  
 [方法: WCF URL 予約を制限付きの予約に置き換える](how-to-replace-the-wcf-url-reservation-with-a-restricted-reservation.md)  
 WCFURL 制限付き予約の使用方法について説明します。  
  
 [トランスポート クォータ](transport-quotas.md)  
 トランスポート層で使用できるクォータを設定する際の考慮事項について説明します。  
  
 [NAT とファイアウォールの使用](working-with-nats-and-firewalls.md)  
 ファイアウォールを介してメッセージを送受信する場合や、ネットワーク アドレス交換 (NAT) が存在する場合にトランスポート層を構成する方法について説明します。  
  
 [Net.TCP ポート共有](net-tcp-port-sharing.md)  
 WCF の Net.tcp ポート共有コンポーネントの使用方法について説明します。  
  
## <a name="reference"></a>関連項目  
 <xref:System.ServiceModel.Channels.HttpTransportBindingElement>  
  
 <xref:System.ServiceModel.Channels.HttpsTransportBindingElement>  
  
 <xref:System.ServiceModel.Channels.TcpTransportBindingElement>  
  
 <xref:System.ServiceModel.Channels.NamedPipeTransportBindingElement>  
  
## <a name="related-sections"></a>関連項目  
 [バインド](bindings.md)  
  
 [バインディングの拡張](../extending/extending-bindings.md)
