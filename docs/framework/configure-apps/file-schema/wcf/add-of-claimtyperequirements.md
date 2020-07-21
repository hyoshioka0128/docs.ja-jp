---
title: <add> の <claimTypeRequirements>
ms.date: 03/30/2017
ms.assetid: c68e83c9-39e8-4264-b1ce-b6a9eb5b98aa
ms.openlocfilehash: 6ba935f7f6dae0e4d9e6581f53a50c684efcbed3
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "79153088"
---
# <a name="add-of-claimtyperequirements"></a>\<add> の \<claimTypeRequirements>
フェデレーション資格情報に表示されると予想される必須のクレームおよび省略可能なクレームの種類を指定します。 たとえば、サービスは、クレームの種類の特定のセットを処理する必要がある受信資格情報について要件を記述します。  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<bindings>**](bindings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<customBinding>**](custombinding.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<binding>**\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<security>**](security-of-custombinding.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<issuedTokenParameters>**](issuedtokenparameters.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<claimTypeRequirements>**](claimtyperequirements-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<add>**  
  
## <a name="syntax"></a>構文  
  
```xml  
<claimTypeRequirements>
  <add claimType="URI"
       isOptional="Boolean" />
</claimTypeRequirements>
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|claimType|クレームの種類を定義する URI。 たとえば、Web サイトから製品を購入するために、ユーザーは、十分な与信限度額を備えた有効なクレジット カードを示す必要があります。 クレームの種類として、クレジット カードの URI があります。|  
|isOptional|これが省略可能なクレームかどうかを指定するブール値。 これが必須のクレームの場合は、この属性を `false` に設定します。<br /><br /> サービスが必須でない情報を求めるときにこの属性を使用できます。 たとえば、ユーザーが名、姓、住所を入力する必要があるのに、電話番号は任意であると判断したとします。|  
  
### <a name="child-elements"></a>子要素  
 なし。  
  
### <a name="parent-elements"></a>親要素  
  
|要素|Description|  
|-------------|-----------------|  
|[\<claimTypeRequirements>](claimtyperequirements-element.md)|必須のクレームの種類のコレクションを指定します。<br /><br /> フェデレーション シナリオでは、サービスが受信資格情報についての要件を記述します。 たとえば、受信資格情報は、特定のクレーム タイプのセットを処理する必要があります。 このコレクションの要素はそれぞれ、フェデレーション資格情報に表示されると予想される必須の要求および省略可能な要求の種類を指定します。|  
  
## <a name="remarks"></a>解説  
 フェデレーション シナリオでは、サービスが受信資格情報についての要件を記述します。 たとえば、受信資格情報は、特定のクレーム タイプのセットを処理する必要があります。 この要件はセキュリティ ポリシー内に明記されます。 クライアントがフェデレーション サービスの資格情報 (CardSpace など) を要求する場合、クライアントは要件をトークン要求 (RequestSecurityToken) に設定します。これにより、フェデレーション サービスは、要件どおりの資格情報を発行できます。  
  
## <a name="example"></a>例  
 次の構成では、2 つのクレームの種類の要件をセキュリティ バインディングに追加しています。  
  
```xml  
<bindings>
  <wsFederationHttpBinding>
    <binding name="myFederatedBinding">
      <security mode="Message">
        <message issuedTokenType="urn:oasis:names:tc:SAML:1.0:assertion">
          <claimTypeRequirements>
            <add claimType="http://schemas.microsoft.com/ws/2005/05/identity/claims/EmailAddress" />
            <add claimType="http://schemas.microsoft.com/ws/2005/05/identity/claims/UserName"
                 optional="true" />
          </claimTypeRequirements>
        </message>
      </security>
    </binding>
  </wsFederationHttpBinding>
</bindings>
```  
  
## <a name="see-also"></a>関連項目

- <xref:System.ServiceModel.Security.Tokens.ClaimTypeRequirement>
- <xref:System.ServiceModel.Security.Tokens.IssuedSecurityTokenParameters.ClaimTypeRequirements%2A>
- <xref:System.ServiceModel.Configuration.IssuedTokenParametersElement.ClaimTypeRequirements%2A>
- <xref:System.ServiceModel.Configuration.ClaimTypeElementCollection>
- <xref:System.ServiceModel.Configuration.ClaimTypeElement>
- <xref:System.ServiceModel.Channels.CustomBinding>
- [\<claimTypeRequirements>](claimtyperequirements-element.md)
- [バインド](../../../wcf/bindings.md)
- [バインディングの拡張](../../../wcf/extending/extending-bindings.md)
- [カスタム バインディング](../../../wcf/extending/custom-bindings.md)
- [\<customBinding>](custombinding.md)
- [方法: SecurityBindingElement を使用してカスタム バインドを作成する](../../../wcf/feature-details/how-to-create-a-custom-binding-using-the-securitybindingelement.md)
- [カスタム バインディング セキュリティ](../../../wcf/samples/custom-binding-security.md)
