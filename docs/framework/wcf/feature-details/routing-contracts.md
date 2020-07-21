---
title: ルーティング コントラクト
ms.date: 03/30/2017
ms.assetid: 9ceea7ae-ea19-4cf9-ba4f-d071e236546d
ms.openlocfilehash: 69dff2c82f67a16d51e11a92052c59672a054e04
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84601076"
---
# <a name="routing-contracts"></a>ルーティング コントラクト
ルーティング コントラクトは、ルーティング サービスが処理できるメッセージ パターンを定義します。  各コントラクトは型指定されておらず、サービスは、メッセージ スキーマやアクションを認識していない場合でもメッセージを受信できます。 このため、ルーティング サービスは、ルーティングされる基盤のメッセージの詳細構成を追加することなく、メッセージをジェネリックにルーティングできます。  
  
## <a name="routing-contracts"></a>ルーティング コントラクト  
 ルーティング サービスには汎用 WCF メッセージ オブジェクトを使用できるため、コントラクトを選ぶ場合の最大の検討事項は、クライアントとサービスとの通信時に使用されるチャネルの形状です。 ルーティング サービスは、メッセージを処理するときに対象型メッセージ ポンプを使用するため、通常、受信コントラクトの形状は、送信コントラクトの形状と一致します。 ただし、ディスパッチャーが双方向チャネルを要求/応答チャネルに変換するときなど、サービスモデルのディスパッチャーが図形を変更できる場合もあります。また、必要ではなく、使用されていない場合 (つまり、 **IInputSessionChannel**を**IInputChannel**に変換する**場合)** は、チャネルからセッションのサポートを削除することもできます。  
  
 これらのメッセージ ポンプをサポートするために、ルーティング サービスでは、<xref:System.ServiceModel.Routing> 名前空間にコントラクトを用意しています。これらのコントラクトは、ルーティング サービスが使用するサービス エンドポイントを定義するときに、使用される必要があります。 これらのコントラクトは型指定されていないため、どのようなメッセージの種類やアクションでも受信でき、ルーティング サービスは、特定のメッセージ スキーマを認識しない場合でもメッセージを処理できます。 ルーティングサービスで使用されるコントラクトの詳細については、「[ルーティングコントラクト](routing-contracts.md)」を参照してください。  
  
 ルーティング サービスによって提供されるコントラクトは、<xref:System.ServiceModel.Routing> 名前空間に含まれています。これらのコントラクトは、次の表のとおりです。  
  
|コントラクト|図形|チャネル形状|  
|--------------|-----------|-------------------|  
|<xref:System.ServiceModel.Routing.ISimplexDatagramRouter>|SessionMode = SessionMode.Allowed<br /><br /> AsyncPattern = true<br /><br /> IsOneWay = true|IInputChannel-> IOutputChannel|  
|<xref:System.ServiceModel.Routing.ISimplexSessionRouter>|SessionMode = SessionMode.Required<br /><br /> AsyncPattern = true<br /><br /> IsOneWay = true|IInputSessionChannel-> IOutputSessionChannel|  
|<xref:System.ServiceModel.Routing.IRequestReplyRouter>|SessionMode = SessionMode.Allowed<br /><br /> AsyncPattern = true|IReplyChannel-> IRequestChannel|  
|<xref:System.ServiceModel.Routing.IDuplexSessionRouter>|SessionMode=SessionMode.Required<br /><br /> CallbackContract=typeof(ISimplexSession)<br /><br /> AsyncPattern = true<br /><br /> IsOneWay = true<br /><br /> TransactionFlow(TransactionFlowOption.Allowed)|IDuplexSessionChannel-> IDuplexSessionChannel|  
  
## <a name="see-also"></a>関連項目

- [ルーティング サービス](routing-service.md)
- [ルーティングの概要](routing-introduction.md)
