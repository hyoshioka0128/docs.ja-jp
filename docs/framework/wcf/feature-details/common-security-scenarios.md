---
title: 一般的なセキュリティ シナリオ
ms.date: 03/30/2017
helpviewer_keywords:
- security [WCF], scenarios
ms.assetid: 201923b5-5162-4a8a-8d4c-e7bd242748d5
ms.openlocfilehash: f36ebdb5ea248ec8134c688f89eb5d0be38dfe38
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84579737"
---
# <a name="common-security-scenarios"></a>一般的なセキュリティ シナリオ
ここでは、考えられるさまざまなクライアントおよびサービスのセキュリティ構成の一覧を示します。 構成はさまざまな要因により異なります。 たとえば、サービスやクライアントがイントラネット上にあるかどうか、また、セキュリティが Windows とトランスポート (HTTPS など) のどちらで提供されるかなどが考えられます。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [セキュリティで保護されていないインターネット環境のクライアントとサービス](internet-unsecured-client-and-service.md)  
 セキュリティで保護されていないパブリックなクライアントとサービスの例です。  
  
 [セキュリティで保護されていないイントラネットのクライアントとサービス](intranet-unsecured-client-and-service.md)  
 セキュリティで保護されたプライベートネットワークに関する情報を WCF アプリケーションに提供するために開発された基本的な Windows Communication Foundation (WCF) サービス。  
  
 [基本認証でのトランスポート セキュリティ](transport-security-with-basic-authentication.md)  
 アプリケーションは、カスタム認証を使用して、クライアントにログオンを許可します。  
  
 [トランスポート セキュリティと Windows 認証](transport-security-with-windows-authentication.md)  
 Windows セキュリティによってセキュリティ保護されたクライアントとサービスを示します。  
  
 [トランスポート セキュリティと匿名クライアント](transport-security-with-an-anonymous-client.md)  
 このシナリオでは HTTPS などのようなトランスポート セキュリティを使用して、機密性と整合性を強化します。  
  
 [トランスポート セキュリティと証明書認証](transport-security-with-certificate-authentication.md)  
 証明書によってセキュリティ保護されたクライアントとサービスを示します。  
  
 [メッセージ セキュリティと匿名クライアント](message-security-with-an-anonymous-client.md)  
 WCF メッセージセキュリティによってセキュリティ保護されたクライアントとサービスを示します。  
  
 [ユーザー名クライアントを使用したメッセージ セキュリティ](message-security-with-a-user-name-client.md)  
 クライアントは、ドメイン ユーザー名とパスワードを使用してクライアントのログオンを許可する Windows フォーム アプリケーションです。  
  
 [メッセージ セキュリティと証明書クライアント](message-security-with-a-certificate-client.md)  
 サーバー側の証明書は複数あり、クライアント側の証明書はそれぞれ 1 つです。 セキュリティのコンテキストは、トランスポート層セキュリティ (TLS: Transport Layer Security) ネゴシエーションを介して確立されます。  
  
 [Windows クライアントとのメッセージ セキュリティ](message-security-with-a-windows-client.md)  
 証明書クライアントのバリエーションの 1 つです。 サーバー側の証明書は複数あり、クライアント側の証明書はそれぞれ 1 つです。 セキュリティのコンテキストは TLS ネゴシエーションを介して確立されます。  
  
 [資格情報ネゴシエーションを使用しない Windows クライアントを使用するメッセージ セキュリティ](message-security-with-a-windows-client-without-credential-negotiation.md)  
 Kerberos ドメインによってセキュリティ保護されたクライアントとサービスを示します。  
  
 [メッセージ セキュリティと相互の証明書](message-security-with-mutual-certificates.md)  
 サーバー側の証明書は複数あり、クライアント側の証明書はそれぞれ 1 つです。 サーバーの証明書はアプリケーションと共に配布され、帯域外でも使用可能です。  
  
 [発行済みトークンを使用したメッセージ セキュリティ](message-security-with-issued-tokens.md)  
 フェデレーション セキュリティにより独立したドメイン間で信頼を確立できます。  
  
 [信頼できるサブシステム](trusted-subsystem.md)  
 クライアントは、ネットワーク全体に分散している 1 つ以上の Web サービスにアクセスします。 Web サービスは、セキュリティで保護する必要がある追加のリソース (データベースや他の Web サービスなど) にアクセスします。  
  
## <a name="reference"></a>関連項目  
 <xref:System.ServiceModel>  
  
## <a name="related-sections"></a>関連項目  
 [承認](authorization-in-wcf.md)  
  
 [セキュリティの概要](security-overview.md)  
  
 [Security](security.md)  
  
 [バインディングとセキュリティ](bindings-and-security.md)  
  
 [サービスおよびクライアントのセキュリティ保護](securing-services-and-clients.md)  
  
 [認証](authentication-in-wcf.md)  
  
 [承認](authorization-in-wcf.md)  
  
 [フェデレーションと発行済みトークン](federation-and-issued-tokens.md)  
  
 [監査](auditing-security-events.md)  
  
## <a name="see-also"></a>関連項目

- [セキュリティ ガイドラインとベスト プラクティス](security-guidance-and-best-practices.md)
- [Windows Server AppFabric のセキュリティ モデル](https://docs.microsoft.com/previous-versions/appfabric/ee677202(v=azure.10))
