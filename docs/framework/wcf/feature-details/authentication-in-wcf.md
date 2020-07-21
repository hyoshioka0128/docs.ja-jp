---
title: WCF での認証
description: Windows 認証、x.509 証明書、ユーザー名とパスワードなどの認証を提供する、WCF のいくつかのメカニズムについて説明します。
ms.date: 03/30/2017
helpviewer_keywords:
- authentication [WCF]
- security [WCF], authentication
ms.assetid: 9254d873-843d-4c6e-bea4-8184ac3e44f4
ms.openlocfilehash: 4c3348cfb84b8571dc1f24b774ffcd691aaa5001
ms.sourcegitcommit: 358a28048f36a8dca39a9fe6e6ac1f1913acadd5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85247521"
---
# <a name="authentication-in-wcf"></a>WCF での認証
次のトピックでは、Windows 認証、x.509 証明書、ユーザー名とパスワードなどの認証を提供する Windows Communication Foundation (WCF) のさまざまなメカニズムについて説明します。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [方法: ASP.NET メンバーシップ プロバイダーを使用する](how-to-use-the-aspnet-membership-provider.md)  
 ASP.NET の機能には、メンバーシップとロール プロバイダー、認証のためのユーザー名とパスワードの組み合わせを格納するデータベース、および承認のためのユーザー ロールがあります。 このトピックでは、WCF サービスが同じデータベースを使用してユーザーを認証および承認する方法について説明します。  
  
 [方法: カスタム ユーザー名およびパスワード検証を使用する](how-to-use-a-custom-user-name-and-password-validator.md)  
 カスタム ユーザー名およびパスワード検証を統合する方法を示します。  
  
 [サービス ID と認証](service-identity-and-authentication.md)  
 追加の保護手段として、クライアントはサービスの予期される*id*を指定することによってサービスを認証できます。 予想される ID とサービスから返される ID が一致しない場合、認証は失敗します。  
  
 [セキュリティ ネゴシエーションとタイムアウト](security-negotiation-and-timeouts.md)  
 <xref:System.ServiceModel.Channels.LocalServiceSecuritySettings.NegotiationTimeout%2A> クラスの <xref:System.ServiceModel.Channels.LocalServiceSecuritySettings> プロパティの使用方法について説明します。  
  
 [Windows 認証エラーのデバッグ](debugging-windows-authentication-errors.md)  
 Windows 認証の使用時に発生する一般的な問題について重点的に説明します。  
  
## <a name="reference"></a>関連項目  
 <xref:System.ServiceModel>  
  
## <a name="related-sections"></a>関連項目  
 [一般的なセキュリティ シナリオ](common-security-scenarios.md)  
  
## <a name="see-also"></a>関連項目

- [セキュリティの概要](security-overview.md)
- [Windows Server AppFabric のセキュリティ モデル](https://docs.microsoft.com/previous-versions/appfabric/ee677202(v=azure.10))
