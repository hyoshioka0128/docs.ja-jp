---
title: <audienceUris>
ms.date: 03/30/2017
ms.assetid: 7a3d8515-d756-4afe-a22d-07cbe2217ee3
author: BrucePerlerMS
ms.openlocfilehash: bd04e4ebdf5c58adaeea0ff0ca5993d7d9ce38f1
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "70252169"
---
# \<audienceUris>
証明書利用者 (RP) の許容される識別子である Uri のセットを指定します。 トークンは、許可されている対象 URI の 1 つに範囲が設定されていない限り、受け入れられません。  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.identityModel>**](system-identitymodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<identityConfiguration>**](identityconfiguration.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<securityTokenHandlers>**](securitytokenhandlers.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<securityTokenHandlerConfiguration>**](securitytokenhandlerconfiguration.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<audienceUris>**  
  
## <a name="syntax"></a>構文  
  
```xml  
<system.identityModel>  
  <identityConfiguration>  
    <securityTokenHandlers>  
      <securityTokenHandlerConfiguration>  
        <audienceUris mode=xs:string>  
          <add value=xs:string />  
          <clear />  
          <remove value=xs:string />  
        </audienceUris>  
      </securityTokenHandlerConfiguration>  
    </securityTokenHandlers>  
  </identityConfiguration>  
</system.identityModel>  
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|mode|<xref:System.IdentityModel.Selectors.AudienceUriMode>対象ユーザーの制限を受信トークンに適用する必要があるかどうかを示す値です。 指定できる値は、"Always"、"Never"、および "BearerKeyOnly" です。 既定値は "Always" です。 省略可能。|  
  
### <a name="child-elements"></a>子要素  
  
|要素|Description|  
|-------------|-----------------|  
|`<add value=xs:string>`|属性によって指定された URI を `value` audienceUris コレクションに追加します。 `value` 属性は必須です。 URI では大文字と小文字が区別されます。|  
|`<clear>`|AudienceUris コレクションをクリアします。 すべての識別子はコレクションから削除されます。|  
|`<remove value=xs:string>`|属性によって指定された URI を `value` audienceUris コレクションから削除します。 `value` 属性は必須です。 URI では大文字と小文字が区別されます。|  
  
### <a name="parent-elements"></a>親要素  
  
|要素|Description|  
|-------------|-----------------|  
|[\<securityTokenHandlerConfiguration>](securitytokenhandlerconfiguration.md)|セキュリティトークンハンドラーのコレクションの構成を提供します。|  
  
## <a name="remarks"></a>解説  
 既定では、コレクションは空です。`<add>`コレクションを `<clear>` 変更するには、、、およびの各要素を使用し `<remove>` ます。 <xref:System.IdentityModel.Tokens.SamlSecurityTokenHandler>オブジェクトと <xref:System.IdentityModel.Tokens.Saml2SecurityTokenHandler> オブジェクトは、AUDIENCE uri コレクションの値を使用して、オブジェクトで許可されている対象ユーザー uri 制限を構成し <xref:System.IdentityModel.Tokens.SamlSecurityTokenRequirement> ます。  
  
 `<audienceUris>`要素は、クラスによって表され <xref:System.IdentityModel.Configuration.AudienceUriElementCollection> ます。 コレクションに追加された個々の URI は、クラスによって表され <xref:System.IdentityModel.Configuration.AudienceUriElement> ます。  
  
> [!NOTE]
> 要素の `<audienceUris>` 子要素としての要素の使用は [\<identityConfiguration>](identityconfiguration.md) 非推奨とされましたが、旧バージョンとの互換性のために引き続きサポートされています。 要素の設定は、要素の設定 `<securityTokenHandlerConfiguration>` よりも優先さ `<identityConfiguration>` れます。  
  
## <a name="example"></a>例  
 次の XML は、アプリケーションに対して許容される対象ユーザーの Uri を構成する方法を示しています。 この例では、単一の URI を構成します。 この URI にスコープが設定されているトークンは受け入れられ、それ以外はすべて拒否されます。  
  
```xml  
<audienceUris>  
  <add value="http://localhost:19851/"/>  
</audienceUris>  
```
