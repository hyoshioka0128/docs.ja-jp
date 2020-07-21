---
title: WCF での承認
ms.date: 03/30/2017
helpviewer_keywords:
- authorization [WCF]
- security [WCF], authorization
ms.assetid: 8ea0b552-af65-45b0-a157-c6c111b8ce5e
ms.openlocfilehash: d67d64dcf0003de28775ac947f8b5f72d7c2ba2a
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84597632"
---
# <a name="authorization-in-wcf"></a>WCF での承認
承認は、サービスやファイルなどのリソースへのアクセスと権限を制御するプロセスです。 このセクションのトピックでは、さまざまな方法で Windows Communication Foundation (WCF) でこの基本的なタスクを実行する方法について説明します。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [アクセス制御機構](access-control-mechanisms.md)  
 WCF の承認メカニズムの概要と、推奨される使用方法について説明します。  
  
 [方法: PrincipalPermissionAttribute クラスでアクセスを制限する](../how-to-restrict-access-with-the-principalpermissionattribute-class.md)  
 <xref:System.Security.Permissions.PrincipalPermissionAttribute> を使用してサービスへのアクセスを制限するプロセスを示します。  
  
 [方法: ASP.NET のロール プロバイダーとサービスを使用する](how-to-use-the-aspnet-role-provider-with-a-service.md)  
 サービスの構成に従って、ASP.NET のロールプロバイダー機能を使用できるようにします。  
  
 [方法: ASP.NET の承認マネージャー ロール プロバイダーとサービスを使用する](how-to-use-the-aspnet-authorization-manager-role-provider-with-a-service.md)  
 ASP.NET は、承認マネージャーを使用して、Web サイトの承認を管理できます。 WCF では、クライアントの承認に ASP.NET/Authorization Manager の組み合わせを利用することもできます。  
  
 [ID モデルを使用したクレームと承認の管理](managing-claims-and-authorization-with-the-identity-model.md)  
 ID モデル インフラストラクチャをクレーム ベースの承認に使用する際の基本について説明します。  
  
 [委任と偽装](delegation-and-impersonation-with-wcf.md)  
 委任と偽装の違いについて説明します。  
  
## <a name="reference"></a>関連項目  
 <xref:System.ServiceModel.Security>  
  
 <xref:System.ServiceModel.Description.PrincipalPermissionMode>  
  
 <xref:System.ServiceModel.Description.ServiceAuthorizationBehavior>  
  
 <xref:System.Security.Permissions.PrincipalPermissionAttribute>  
  
## <a name="related-sections"></a>関連項目  
 [認証](authentication-in-wcf.md)  
  
## <a name="see-also"></a>関連項目

- [セキュリティの概要](security-overview.md)
- [Windows Server AppFabric のセキュリティ モデル](https://docs.microsoft.com/previous-versions/appfabric/ee677202(v=azure.10))
