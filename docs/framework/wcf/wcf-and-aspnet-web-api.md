---
title: WCF と ASP.NET Web API
description: 各テクノロジの主な機能を比較することにより、WCF または ASP.NET Web API がニーズに適しているかどうかを説明します。
ms.date: 03/30/2017
ms.assetid: 08ceded3-fd9a-4467-9715-c4cbd9c7228e
ms.openlocfilehash: de8d1905866c860da96983c2f3d52599e3342403
ms.sourcegitcommit: 358a28048f36a8dca39a9fe6e6ac1f1913acadd5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85245966"
---
# <a name="wcf-and-aspnet-web-api"></a>WCF と ASP.NET Web API
WCF は、サービス指向のアプリケーションを構築するための Microsoft の統一プログラミング モデルです。 これを使用して開発者は、プラットフォーム間を統合し、既存のコンポーネントと相互運用する、セキュリティで保護された信頼性の高いトランザクション型のソリューションを構築できます。 [ASP.NET Web API](https://www.asp.net/web-api)は、ブラウザーやモバイルデバイスを含む広範なクライアントに接続できる HTTP サービスを簡単に構築できるフレームワークです。 ASP.NET Web API は、.NET Framework に基づいて RESTful アプリケーションを構築するのに最適なプラットフォームです。 このトピックでは、ニーズに最適なテクノロジを決定するのに役立つガイドラインを示します。  
  
## <a name="choosing-which-technology-to-use"></a>使用するテクノロジの選択  
 各テクノロジの主な機能を次の表に示します。  
  
|WCF|ASP.NET Web API|  
|---------|---------------------|  
|複数のトランスポート プロトコル (HTTP、TCP、UDP、およびカスタム トランスポート) をサポートするサービスを構築し、構築したサービスを切り替えることができます。|HTTP のみ。 HTTP のファーストクラスプログラミングモデル。 さまざまなブラウザーやモバイルデバイスなどからのアクセスに適しています。|  
|メッセージの種類が同じ複数のエンコーディング (テキスト、MTOM、およびバイナリ) をサポートするサービスを構築し、構築したサービスを切り替えることができます。|XML や JSON などのさまざまなメディアの種類をサポートする Web API を構築できます。|  
|Reliable Messaging、Transactions、Message Security などの WS-* 標準を使用してサービスを構築できます。|では、HTTP、Websocket、SSL、JSON、XML などの基本プロトコルと形式が使用されます。 Reliable Messaging や Transactions などの高レベルのプロトコルはサポートされません。|  
|要求/応答、一方向、および双方向の各メッセージ交換パターンをサポートしています。|HTTP は要求/応答ですが、 [SignalR](https://github.com/SignalR/SignalR)と websocket の統合を使用して追加のパターンをサポートできます。|  
|WCF SOAP サービスは WSDL で記述でき、スキーマが複雑なサービスの場合でも自動化ツールを使用してクライアント プロキシを生成できます。|スニペットを記述する自動生成された HTML ヘルプ ページから OData で統合された API 用に構造化されたメタデータまで、Web API を記述するためのさまざまな方法があります。|  
|には、.NET Framework が付属しています。|には .NET Framework が付属していますが、オープンソースであり、独立したダウンロードとして帯域外で使用することもできます。|  
  
 WCF を使用して、さまざまなトランスポート経由でアクセスできる信頼性の高いセキュリティで保護された web サービスを作成します。 ASP.NET Web API を使用すると、さまざまなクライアントからアクセスできる HTTP ベースのサービスを作成できます。 ASP.NET Web API は、新しい REST スタイルのサービスを作成および設計する場合に使用します。 WCF では REST スタイルのサービスの作成を一部サポートしていますが、ASP.NET Web API の REST のサポートはより詳細で、以降の REST 機能の強化は ASP.NET Web API で行われる予定です。 既存の WCF サービスがあり、追加の REST エンドポイントを公開する場合は、WCF および <xref:System.ServiceModel.WebHttpBinding> を使用してください。  
  
## <a name="see-also"></a>関連項目

- [Windows Communication Foundation とは](whats-wcf.md)
- [Windows Communication Foundation の基本概念](fundamental-concepts.md)
