---
title: WCF と WebSocket
ms.date: 03/30/2017
ms.assetid: 1e53b49e-022c-49c7-8984-4b21b53c05b3
ms.openlocfilehash: df4a251eb5a570c9fedf19d385a027e23481afed
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84594947"
---
# <a name="wcf-and-websockets"></a>WCF と WebSocket
.NET Framework 4.5 では、Windows Communication Foundation の WebSocket のサポートが導入されています。  Websocket は、標準的な HTTP ポート 80 と 443 を介した双方向通信を有効にする効率的な標準ベース テクノロジです。 標準 HTTP ポートを使用することで、Websocket は中継局を通じて Web 全体で通信できます。  2 つの新しい標準バインディングが WebSocket トランスポート経由の通信をサポートするために追加されました。 <xref:System.ServiceModel.NetHttpBinding> および <xref:System.ServiceModel.NetHttpsBinding>。 Websocket 固有の設定は、プロパティにアクセスすることによってで構成でき <xref:System.ServiceModel.Channels.HttpTransportBindingElement> <xref:System.ServiceModel.Channels.HttpTransportBindingElement.WebSocketSettings%2A> ます。
  
## <a name="in-this-section"></a>このセクションの内容  
 [NetHttpBinding の使用](using-the-nethttpbinding.md)  
 <xref:System.ServiceModel.NetHttpBinding> とその構成方法について説明します。  
  
 [方法: WebSockets 上で通信する WCF サービスを作成する](how-to-create-a-wcf-service-that-communicates-over-websockets.md)  
 Websocket 経由で通信する WCF サービスを作成する方法について説明します。  
  
## <a name="reference"></a>関連項目  
  
## <a name="related-sections"></a>関連項目
