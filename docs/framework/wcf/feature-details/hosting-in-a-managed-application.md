---
title: マネージド アプリケーションのホスト
ms.date: 03/30/2017
ms.assetid: af70132d-e9e1-4f32-b20f-f0014629758a
ms.openlocfilehash: 759257edf89d1af5c453bb98f41361b54cf113ae
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84597346"
---
# <a name="hosting-in-a-managed-application"></a>マネージド アプリケーションのホスト
Windows Communication Foundation (WCF) サービスは、任意の .NET Framework アプリケーションでホストできます。 自己ホスト型サービスは、展開を要するインフラストラクチャが最も少ないので、最も柔軟なホスト オプションです。 ただし、マネージアプリケーションは、インターネットインフォメーションサービス (IIS) や Windows サービスなど、WCF の他のホストオプションの高度なホスト機能や管理機能を提供しないため、最も信頼性の低いホストオプションでもあります。  
  
 自己ホスト型サービスを作成するには、メッセージをリッスンするサービスを開始する <xref:System.ServiceModel.ServiceHost>のインスタンスを作成して開きます。 詳細については、「[方法: マネージアプリケーションで WCF サービスをホスト](../how-to-host-a-wcf-service-in-a-managed-application.md)する」を参照してください。  
  
 コントラクトを定義する方法、コントラクトを実装する方法、およびマネージアプリケーション内でサービスをホストする方法の完全な例については、[はじめにチュートリアル](../getting-started-tutorial.md)と[自己ホスト](../samples/self-host.md)を参照してください。  
  
 以下に、このホスト オプションを使用する一般的なシナリオについて説明します。  
  
## <a name="console-applications"></a>コンソール アプリケーション  
 自己ホストによって可能になる一般的なシナリオは、コンソールアプリケーション内で実行される WCF サービスです。 通常、コンソールアプリケーション内で WCF サービスをホストすることは、サービスの開発フェーズで役に立ちます。 コンソール アプリケーションにより、アプリケーション内部で起こっている状況を見極めるための情報のデバッグやトレースが容易になり、新しい場所にアプリケーションをコピーして移動することも簡単に行うことができます。  
  
## <a name="rich-client-applications"></a>リッチ クライアント アプリケーション  
 自己ホストによって有効になるその他の一般的なシナリオとしては、Windows Presentation Foundation (WPF) または Windows フォーム (WinForms) に基づいたクライアントアプリケーションなどがあります。 また、このホストオプションを使用すると、WPF や WinForms アプリケーションなどのリッチクライアントアプリケーションで外部との通信を容易に行うことができます。 たとえば、ユーザーインターフェイスに WPF を使用し、他のクライアントがそれに接続して情報を共有できるようにする WCF サービスもホストするピアツーピアコラボレーションクライアントなどです。  
  
## <a name="see-also"></a>関連項目

- [ホスティング サービス](../hosting-services.md)
- [はじめにチュートリアル](../getting-started-tutorial.md)
