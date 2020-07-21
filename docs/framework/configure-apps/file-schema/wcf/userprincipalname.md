---
title: <userPrincipalName>
ms.date: 03/30/2017
ms.assetid: 68032f69-149e-4613-bae4-18314d4fd294
ms.openlocfilehash: 299af8c4a013d17d7c5b7285f6fb89892c4164a8
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "70854829"
---
# \<userPrincipalName>
クライアントで認証するサービスのユーザー プリンシパル名 (UPN) を指定します。  
  
UPN の設定の詳細については、「[サービス id と認証](../../../wcf/feature-details/service-identity-and-authentication.md)」を参照してください。  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<client>**](client.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<endpoint>**](endpoint-of-client.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<identity>**](identity.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<userPrincipalName>**  
  
## <a name="syntax"></a>構文  
  
```xml  
<userPrincipalName value="String" />
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|value|ユーザー アカウント名 (ユーザー ログイン名と呼ばれることもある) と、ユーザー アカウントの検索範囲のドメインを識別するドメイン名です。 これは、Windows ドメインにログオンするための標準的使用方法です。 形式は、 someone@example.com (電子メールアドレスの場合) です。|  
  
### <a name="child-elements"></a>子要素  
 なし。  
  
### <a name="parent-elements"></a>親要素  
  
|要素|Description|  
|-------------|-----------------|  
|[\<identity>](identity.md)|クライアントで認証するサービスの ID を指定します。|  
  
## <a name="remarks"></a>解説  
 この id を持つエンドポイントに接続するセキュリティで保護された Windows Communication Foundation (WCF) クライアントは、エンドポイントで SSPI 認証を実行するときに UPN を使用します。  
  
## <a name="example"></a>例  
 次の構成コードは、クライアントで認証するサービスの UPN を指定します。  
  
```xml  
<identity>
  <userPrincipalName value="someone@cohowinery.com" />
</identity>
```  
  
## <a name="see-also"></a>関連項目

- <xref:System.ServiceModel.Configuration.IdentityElement>
- <xref:System.ServiceModel.EndpointAddress>
- <xref:System.ServiceModel.EndpointAddress.Identity%2A>
- <xref:System.ServiceModel.UpnEndpointIdentity>
- [サービス ID と認証](../../../wcf/feature-details/service-identity-and-authentication.md)
- [\<identity>](identity.md)
