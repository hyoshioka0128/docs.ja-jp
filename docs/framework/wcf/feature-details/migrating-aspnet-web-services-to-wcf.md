---
title: ASP.NET Web サービスを WCF に移行する
ms.date: 03/30/2017
ms.assetid: 1adbb931-f0b1-47f3-9caf-169e4edc9907
ms.openlocfilehash: fa707a4246d5bc9940417072c098b2973140f878
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84598802"
---
# <a name="migrating-aspnet-web-services-to-wcf"></a>ASP.NET Web サービスを WCF に移行する
ASP.NET には Web サービスを構築するための .NET Framework クラス ライブラリとツールが用意されています。また、インターネット インフォメーション サービス (IIS) 内でサービスをホストする機能も用意されています。 Windows Communication Foundation (WCF) には、ソフトウェアエンティティが任意のプロトコル (Web サービスで使用されるプロトコルを含む) を使用して通信できるようにするための、.NET Framework クラスライブラリ、ツール、およびホスト機能が用意されています。  ASP.NET Web サービスを WCF に移行することで、アプリケーションは WCF に固有の新機能と機能強化を利用できます。  
  
 WCF には、ASP.NET ウェブサービスに関連する重要な利点がいくつかあります。 ASP.NET Web services ツールは Web サービスの構築専用ですが、WCF には、ソフトウェアエンティティを相互に通信する必要がある場合に使用できるツールが用意されています。 これにより、さまざまなソフトウェア通信シナリオを実現するために開発者が知っておく必要があるテクノロジの数が少なくて済むため、ソフトウェア開発プロジェクトが完了するまでの時間だけでなく、ソフトウェア開発リソースのコストが削減されます。  
  
 Web サービス開発プロジェクトの場合でも、WCF は ASP.NET ウェブサービスサポートよりも多くの Web サービスプロトコルをサポートします。 これらの追加プロトコルにより、特に信頼できるセッションとトランザクションという点で、より洗練されたソリューションが実現されます。  
  
 WCF では、ASP.NET ウェブサービスよりも多くのプロトコルをサポートしています。 ASP.NET Web サービスでは、HTTP (ハイパーテキスト転送プロトコル) を使用したメッセージの送信しかサポートしていません。 WCF では、HTTP、伝送制御プロトコル (TCP)、名前付きパイプ、および Microsoft Message Queuing (MSMQ) を使用したメッセージの送信をサポートしています。 さらに重要なのは、追加のトランスポートプロトコルをサポートするように WCF を拡張できることです。 そのため、WCF を使用して開発されたソフトウェアは、他のさまざまなソフトウェアと連携して動作するように調整できるため、投資収益率を高めることができます。  
  
 WCF では、ASP.NET Web サービスで提供されるアプリケーションを展開および管理するための豊富な機能が提供されます。 ASP.NET にも含まれる構成システムに加えて、WCF では、構成エディター、送信者から受信者へのアクティビティトレース、任意の数の中継局、トレースビューアー、メッセージログ、膨大な数のパフォーマンスカウンター、Windows Management Instrumentation のサポートが提供されています。  
  
 ASP.NET ウェブサービスに関連する WCF の潜在的な利点を考えて、を使用している場合、または ASP.NET Web サービスの使用を検討している場合は、いくつかのオプションがあります。  
  
- 引き続き ASP.NET ウェブサービスを使用し、WCF による特典を proffered ます。  
  
- 今後、WCF を導入することを目的として、ASP.NET ウェブサービスの使用を継続します。 このセクションのトピックでは、新しい ASP.NET Web サービスアプリケーションを将来の WCF アプリケーションと共に使用できるようにするための見込顧客を最大化する方法について説明します。 このセクションのトピックでは、WCF への移行を容易にするために、新しい ASP.NET Web サービスを構築する方法についても説明します。 ただし、サービスをセキュリティで保護することが重要な場合、信頼性やトランザクションの保証が必要な場合、またはカスタムの管理機能を構築する必要がある場合は、WCF を導入することをお勧めします。 WCF は、このようなシナリオ向けに設計されています。  
  
- 既存の ASP.NET Web サービスアプリケーションを引き続き維持しながら、新しい開発用に WCF を導入します。 おそらくこれが最適な選択です。 WCF の利点が得られますが、既存のアプリケーションを変更して使用するためのコストが発生します。 このシナリオでは、新しい WCF アプリケーションを既存の ASP.NET アプリケーションと共存させることができます。 新しい WCF アプリケーションは、既存の ASP.NET Web サービスを使用できるようになります。また、wcf ASP.NET 互換モードを利用することで、WCF を使用して、新しい運用機能を既存の ASP.NET アプリケーションにプログラムすることができます。  
  
- WCF を導入し、既存の ASP.NET Web サービスアプリケーションを WCF に移行します。 このオプションを選択すると、WCF によって提供される機能を使用して既存のアプリケーションを拡張したり、新しいより強力な WCF アプリケーション内の既存の ASP.NET Web サービスの機能を再現したりすることができます。  
  
> [!NOTE]
> WCF サービスが IIS 5.x によってホストされ、ASP.NET がアンインストールされている場合は、注意が必要です。 WCF サービスが IIS 5.x によってホストされている場合、ASP.NET がアンインストールされると、サービスのコードが要求される可能性があります。 IIS 5.x が実行されているオペレーティングシステムで ASP.NET がアンインストールされ、WCF がアンインストールされると、.svc 拡張子の付いたファイルがテキストファイルと見なされ、ソースコードを含む内容が要求元に返されます。  
  
 このセクションでは、これらのオプションについて詳しく説明し、ASP.NET Web サービスを WCF と比較し、ASP.NET Web サービスコードを WCF に移行する方法について説明します。  
  
## <a name="see-also"></a>関連項目

- [Windows Communication Foundation 導入の準備:将来の移行の簡略化](anticipating-adopting-wcf-migration.md)
- [Windows Communication Foundation 導入の準備:将来的な統合の容易化](anticipating-adopting-the-wcf-easing-future-integration.md)
- [Windows Communication Foundation の採用](adopting-wcf.md)
- [使用目的と使用標準に基づく ASP.NET Web サービスと WCF との比較](comparing-aspnet-web-services-to-wcf-based-on-purpose-and-standards-used.md)
- [開発者の視点から見た ASP.NET Web サービスと WCF との比較](comparing-aspnet-web-services-to-wcf-based-on-development.md)
