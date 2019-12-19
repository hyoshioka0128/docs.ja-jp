---
title: インターネット インフォメーション サービスでのホスティング
ms.date: 03/30/2017
helpviewer_keywords:
- hosting services [WCF], IIS
ms.assetid: ddae14e8-143c-442d-b660-2046809b2d43
ms.openlocfilehash: 8ea7602e82d13425bb678555dde1f44ccbbf5a0f
ms.sourcegitcommit: a4f9b754059f0210e29ae0578363a27b9ba84b64
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/05/2019
ms.locfileid: "74837468"
---
# <a name="hosting-in-internet-information-services"></a>インターネット インフォメーション サービスでのホスティング
Windows Communication Foundation (WCF) サービスをホストするための1つのオプションは、インターネットインフォメーションサービス (IIS) アプリケーションの内部にあります。 このホスティングモデルは、ASP.NET および ASP.NET Web services (ASMX) Web サービスで使用されるモデルに似ています。  
  
## <a name="versions-of-iis"></a>IIS バージョン  
 WCF は、次のオペレーティングシステム上の IIS の次のバージョンでホストできます。  
  
- [!INCLUDE[wxpsp2](../../../../includes/wxpsp2-md.md)] 上で IIS 5.1 を使用。 この環境は、後で [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)] などのサーバー オペレーティング システムに展開される、IIS ホスト型アプリケーションの設計と開発に役立ちます。  
  
- [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)]の IIS 6.0。 IIS 6.0 は、スケーラビリティ、信頼性、およびアプリケーションの分離が強化された高度なプロセス モデルを提供します。 この環境は、HTTP 通信のみを使用する WCF サービスの運用環境へのデプロイに適しています。  
  
- Windows Vista および [!INCLUDE[lserver](../../../../includes/lserver-md.md)]の IIS 7.0。 IIS 7.0 は、IIS 6.0 と同じ高度なプロセスモデルを提供しますが、Windows プロセスアクティブ化サービス (WAS) を使用して、HTTP 以外のプロトコルを介したアクティベーションとネットワーク通信を許可します。 この環境は、WCF でサポートされている任意のネットワークプロトコル (HTTP、net.tcp、net.pipe、および net.tcp を含む) を介して通信する WCF サービスの開発に適しています。 WAS の詳細については、「 [Windows プロセスアクティブ化サービスでのホスト](../../../../docs/framework/wcf/feature-details/hosting-in-windows-process-activation-service.md)」を参照してください。  
  
- [Windows Server AppFabric](https://go.microsoft.com/fwlink/?LinkId=196496)は、IIS 7.0 および Windows プロセスアクティブ化サービス (WAS) と連携して、NET4 WCF および WF サービスのための豊富なアプリケーションホスティング環境を提供します。 この利点には、プロセス ライフサイクル管理、プロセス リサイクル、共有ホスティング、迅速な障害保護、プロセスの孤立化、オンデマンド アクティブ化、状態監視などがあります。 詳細については、「 [appfabric のホスティング機能](https://go.microsoft.com/fwlink/?LinkId=196494)」と「 [appfabric のホスティングの概念](https://go.microsoft.com/fwlink/?LinkId=196495)」を参照してください。  
  
## <a name="benefits-of-iis-hosting"></a>IIS ホスティングの利点  
 IIS で WCF サービスをホストすると、いくつかの利点があります。  
  
- IIS でホストされている WCF サービスは、ASP.NET アプリケーションや ASMX など、他の種類の IIS アプリケーションと同様に展開および管理されます。  
  
- IIS によって、プロセスをアクティブ化する機能、状態管理機能、およびリサイクル機能が提供され、ホストされるアプリケーションの信頼性が向上します。  
  
- ASP.NET と同様に、ASP.NET でホストされる WCF サービスは、サーバーの密度とスケーラビリティを向上させるために、共通のワーカープロセス内に複数のアプリケーションが存在する ASP.NET 共有ホスティングモデルを利用できます。  
  
- IIS でホストされる WCF サービスは、ASP.NET 2.0 と同じ動的コンパイルモデルを使用します。これにより、ホステッドサービスの開発とデプロイが簡単になります。  
  
 IIS で WCF サービスをホストする場合は、IIS 5.1 と IIS 6.0 が HTTP 通信のみに制限されていることに注意することが重要です。 ホスティング環境の選択の詳細については、「[ホスティングサービス](../../../../docs/framework/wcf/hosting-services.md)」を参照してください。  
  
## <a name="deploying-an-iis-hosted-wcf-service"></a>IIS にホストされた WCF サービスの展開  
 IIS でホストされる WCF サービスの開発と展開は、次のタスクで構成されています。  
  
- IIS、ASP.NET、WCF、および WCF HTTP アクティブ化コンポーネントが正しくインストールおよび登録されていることを確認します。  
  
- 新しい IIS アプリケーションを作成するか、既存の ASP.NET アプリケーションを再利用します。  
  
- WCF サービスの .svc ファイルを作成します。  
  
- IIS アプリケーションにサービス実装を展開します。  
  
- WCF サービスを構成します。  
  
 これらの各タスクの詳細については、「[インターネットインフォメーションサービスでホストされる WCF サービスの配置](../../../../docs/framework/wcf/feature-details/deploying-an-internet-information-services-hosted-wcf-service.md)」を参照してください。  
  
## <a name="wcf-services-and-aspnet"></a>WCF サービスと ASP.NET  
 WCF サービスは、ASP.NET とサイドバイサイドでホストすることも、ASP.NET 互換モードでホストすることもできます。このモードでは、ASP.NET Web アプリケーションプラットフォームによって提供される機能をサービスが最大限に活用できます。 これらの機能の詳細については、「 [WCF Services と ASP.NET](../../../../docs/framework/wcf/feature-details/wcf-services-and-aspnet.md)」を参照してください。  
  
## <a name="see-also"></a>参照

- [ServiceHostFactory を使用したホストの拡張](../../../../docs/framework/wcf/extending/extending-hosting-using-servicehostfactory.md)
- [インターネット インフォメーション サービスでホストされる WCF サービスの配置](../../../../docs/framework/wcf/feature-details/deploying-an-internet-information-services-hosted-wcf-service.md)
- [WCF サービスと ASP.NET](../../../../docs/framework/wcf/feature-details/wcf-services-and-aspnet.md)
- [インターネット インフォメーション サービス ホスティングのベスト プラクティス](../../../../docs/framework/wcf/feature-details/internet-information-services-hosting-best-practices.md)
- [Windows Communication Foundation での Internet Information Services 7.0 の構成](../../../../docs/framework/wcf/feature-details/configuring-iis-for-wcf.md)
- [AppFabric のホスティング機能](https://go.microsoft.com/fwlink/?LinkId=201276)
