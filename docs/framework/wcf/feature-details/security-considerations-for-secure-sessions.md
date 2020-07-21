---
title: セキュリティで保護されたセッションに関するセキュリティの検討
ms.date: 03/30/2017
ms.assetid: 0d5be591-9a7b-4a6f-a906-95d3abafe8db
ms.openlocfilehash: 587897cc296523e0bfd5a4d4fa50b1e145cb69fb
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84601050"
---
# <a name="security-considerations-for-secure-sessions"></a>セキュリティで保護されたセッションに関するセキュリティの検討
セキュリティで保護されたセッションを実装する場合に、セキュリティに影響を及ぼす次の項目について考慮する必要があります。 セキュリティに関する考慮事項の詳細については、「セキュリティの[考慮事項](security-considerations-in-wcf.md)とセキュリティ[に関するベストプラクティス](best-practices-for-security-in-wcf.md)」を参照してください。  
  
## <a name="secure-sessions-and-metadata"></a>セキュリティで保護されたセッションとメタデータ  
 セキュリティで保護されたセッションが確立され、 <xref:System.ServiceModel.Security.Tokens.SecureConversationSecurityTokenParameters.RequireCancellation%2A> プロパティがに設定されている場合 `false` 、WINDOWS COMMUNICATION FOUNDATION (WCF) は、 `mssp:MustNotSendCancel` サービスエンドポイントの Web サービス記述言語 (WSDL) ドキュメントのメタデータの一部としてアサーションを送信します。 `mssp:MustNotSendCancel` アサーションは、クライアントに対してセキュリティで保護されたセッションのキャンセル要求にサービスが応答しないことを通知します。 <xref:System.ServiceModel.Security.Tokens.SecureConversationSecurityTokenParameters.RequireCancellation%2A>プロパティがに設定されている場合 `true` 、WCF は `mssp:MustNotSendCancel` WSDL ドキュメントにアサーションを生成しません。 セキュリティで保護されたセッションが必要でなくなった場合、クライアントはサービスに対してキャンセル要求を送る必要があります。 [ServiceModel メタデータユーティリティツール (svcutil.exe)](../servicemodel-metadata-utility-tool-svcutil-exe.md)を使用してクライアントが生成されると、クライアントコードはアサーションの有無に応じて適切に反応し `mssp:MustNotSendCancel` ます。  
  
## <a name="secure-conversations-and-custom-tokens"></a>セキュリティ保護されたメッセージ交換とカスタム トークン  
 WS-SecureConversation 仕様での定義方法に起因する、カスタム トークンと派生キーの混在に関する問題があります。 この仕様では、は、派生トークンを参照する省略可能な要素であることを示してい `wsse:SecurityTokenReference` ます。 " `/wsc:DerivedKeyToken/wsse:SecurityTokenReference` この省略可能な要素は、派生に使用されるセキュリティコンテキストトークン、セキュリティトークン、または共有キー/シークレットを指定するために使用されます。 指定されていない場合、受信者はメッセージのコンテキストから共有キーを判断できると想定されます。 コンテキストを特定できない場合は、などのエラーを `wsc:UnknownDerivationSource` 発生させる必要があります。 "  
  
 つまり、カスタム トークンを派生させるには、`SecurityTokenReference` 要素にその句型をラップする必要があります。 派生をオフにするオプションもありますが、キーを派生させるオプションが既定となっています。 キーをラップしなかった場合、派生キー トークンのシリアル化は実行されますが、その逆シリアル化を試みると例外がスローされます。  
  
## <a name="see-also"></a>関連項目

- [方法: WSFederationHttpBinding のセキュリティで保護されたセッションを無効にする](how-to-disable-secure-sessions-on-a-wsfederationhttpbinding.md)
- [セキュリティの考慮事項](security-considerations-in-wcf.md)
- [セキュリティのベスト プラクティス](best-practices-for-security-in-wcf.md)
