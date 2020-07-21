---
title: SAML トークンとクレーム
description: WFC が SAML トークンを使用して、別のエンティティに関する1つのエンティティによって作成されたクレームのセットであるステートメントを実行する方法について説明します。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WCF, federation
- federation
- issued tokens
- SAML token
ms.assetid: 930b6e34-9eab-4e95-826c-4e06659bb977
ms.openlocfilehash: c054e594af69def96879852a5145675b3123614a
ms.sourcegitcommit: 358a28048f36a8dca39a9fe6e6ac1f1913acadd5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85244947"
---
# <a name="saml-tokens-and-claims"></a>SAML トークンとクレーム
セキュリティアサーションマークアップ言語 (SAML)*トークン*は、クレームの XML 表現です。 既定では、フェデレーションセキュリティシナリオで使用される SAML トークン Windows Communication Foundation (WCF) では、*トークンが発行*されます。  
  
 SAML トークンは、ステートメント (特定のエンティティによって他のエンティティに関して作成されるクレームのセット) を伝達します。 たとえば、フェデレーション セキュリティ シナリオでは、ステートメントがセキュリティ トークン サービスによって、システム内の特定のユーザーに関して作成されます。 セキュリティ トークン サービスは、トークンに含まれるステートメントの信憑性を示すために SAML トークンに署名します。 また、SAML トークンは、SAML トークンのユーザーが証明として提示する暗号化キー マテリアルに関連付けられています。 これが証拠となり、証明書利用者は、SAML トークンが実際にそのユーザーに対して発行されたことを確認できます。 一般的なシナリオでの例を次に示します。  
  
1. クライアントは、セキュリティ トークン サービスから SAML トークンを要求し、Windows 資格情報を使用して、そのセキュリティ トークン サービスに対して認証を行います。  
  
2. セキュリティ トークン サービスは、SAML トークンをクライアントに発行します。 SAML トークンは、セキュリティ トークン サービスに関連付けられた証明書を使用して署名され、ターゲット サービス用に暗号化された証明キーを含んでいます。  
  
3. クライアントは、*証明キー*のコピーも受け取ります。 次に、クライアントは SAML トークンをアプリケーションサービス (*証明書利用者*) に提示し、その証明キーを使用してメッセージに署名します。  
  
4. SAML トークンの署名は、そのトークンがセキュリティ トークン サービスによって発行されたことを証明書利用者に示します。 また、証明キーを使用して作成されたメッセージ署名は、トークンがそのクライアントに対して発行されたことを示します。  
  
## <a name="from-claims-to-samlattributes"></a>クレームから SamlAttributes  
 WCF では、SAML トークン内のステートメントはオブジェクトとしてモデル化されます。オブジェクトのプロパティがで、 <xref:System.IdentityModel.Tokens.SamlAttribute> <xref:System.IdentityModel.Claims.Claim> <xref:System.IdentityModel.Claims.Claim> <xref:System.IdentityModel.Claims.Claim.Right%2A> <xref:System.IdentityModel.Claims.Rights.PossessProperty%2A> <xref:System.IdentityModel.Claims.Claim.Resource%2A> プロパティが型 <xref:System.String> である場合は、オブジェクトから直接データを設定できます。 次に例を示します。  
  
 [!code-csharp[c_CreateSTS#8](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_creatests/cs/source.cs#8)]
 [!code-vb[c_CreateSTS#8](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_creatests/vb/source.vb#8)]  
  
> [!NOTE]
> セキュリティ トークン サービスによって発行されたか、または認証の一部としてクライアントからサービスに提示されたときに、SAML トークンがメッセージ内にシリアル化される場合、メッセージの最大クォータ サイズが、SAML トークンおよびメッセージの他の部分を格納できるだけの大きさである必要があります。 通常は、既定のメッセージ クォータ サイズで十分です。 ただし、何百ものクレームを含んでいるために SAML トークンのサイズが大きい場合には、シリアル化されたトークンを格納できるように、クォータを増やす必要が生じることがあります。 詳細については、「[データのセキュリティに関する考慮事項](security-considerations-for-data.md)」を参照してください。  
  
## <a name="from-samlattributes-to-claims"></a>SamlAttributes からクレーム  
 SAML トークンがメッセージで受信されると、SAML トークン内のさまざまなステートメントは、 <xref:System.IdentityModel.Policy.IAuthorizationPolicy> オブジェクトに変換され、<xref:System.IdentityModel.Policy.AuthorizationContext> に配置されます。 各 SAML ステートメントのクレームは <xref:System.IdentityModel.Policy.AuthorizationContext.ClaimSets%2A> の <xref:System.IdentityModel.Policy.AuthorizationContext> プロパティによって返され、これを調べることによってユーザーの認証と承認を行うかどうかを決定できます。  
  
## <a name="see-also"></a>関連項目

- <xref:System.IdentityModel.Policy.AuthorizationContext>
- <xref:System.IdentityModel.Policy.IAuthorizationPolicy>
- <xref:System.IdentityModel.Claims.ClaimSet>
- [フェデレーション](federation.md)
- [方法: フェデレーション クライアントを作成する](how-to-create-a-federated-client.md)
- [方法: フェデレーション サービスで資格情報を設定する](how-to-configure-credentials-on-a-federation-service.md)
- [ID モデルを使用したクレームと承認の管理](managing-claims-and-authorization-with-the-identity-model.md)
- [クレームとトークン](claims-and-tokens.md)
- [クレームの作成とリソース値](claim-creation-and-resource-values.md)
- [方法: カスタム クレームを作成する](../extending/how-to-create-a-custom-claim.md)
