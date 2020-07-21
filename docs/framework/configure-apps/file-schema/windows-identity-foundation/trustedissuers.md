---
title: <trustedIssuers>
ms.date: 03/30/2017
ms.assetid: d818c917-07b4-40db-9801-8676561859fd
author: BrucePerlerMS
ms.openlocfilehash: 50fc7194823fb0c5c426fb54ffd50b17c3714ed9
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "70251756"
---
# \<trustedIssuers>
構成ベースの発行者名レジストリ () によって使用される、信頼された発行者の証明書の一覧を構成し <xref:System.IdentityModel.Tokens.ConfigurationBasedIssuerNameRegistry> ます。  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.identityModel>**](system-identitymodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<identityConfiguration>**](identityconfiguration.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<securityTokenHandlers>**](securitytokenhandlers.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<securityTokenHandlerConfiguration>**](securitytokenhandlerconfiguration.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<issuerNameRegistry>**](issuernameregistry.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<trustedIssuers>**  
  
## <a name="syntax"></a>構文  
  
```xml  
<system.identityModel>  
  <identityConfiguration>  
    <securityTokenHandlers>  
      <securityTokenHandlerConfiguration>  
        <issuerNameRegistry>  
          <trustedIssuers>  
            <add thumbprint=xs:string name=xs:string>  
            <clear>  
            <remove thumbprint=xs:string>  
          </trustedIssuers>  
        </issuerNameRegistry>  
      </securityTokenHandlerConfiguration>  
    </securityTokenHandlers>  
  </identityConfiguration>  
</system.identityModel>  
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
 なし  
  
### <a name="child-elements"></a>子要素  
  
|要素|説明|  
|-------------|-----------------|  
|`<add thumbprint=xs:string name=xs:string>`|信頼された発行者のコレクションに証明書を追加します。 証明書は属性で指定され `thumbprint` ます。 この属性は必須であり、証明書の拇印の asn.1 エンコード形式を含んでいる必要があります。 `name`属性は省略可能で、証明書のフレンドリ名を指定するために使用できます。|  
|`<clear>`|信頼された発行者のコレクションからすべての証明書を削除します。|  
|`<remove thumbprint=xs:string>`|信頼された発行者のコレクションから証明書を削除します。 証明書は属性で指定され `thumbprint` ます。 この属性は必須です。|  
  
### <a name="parent-elements"></a>親要素  
  
|要素|説明|  
|-------------|-----------------|  
|[\<issuerNameRegistry>](issuernameregistry.md)|発行者名レジストリを構成します。 **重要:** 要素 `type` の属性は、 `<issuerNameRegistry>` 要素を有効にするためにクラスを参照する必要があり <xref:System.IdentityModel.Tokens.ConfigurationBasedIssuerNameRegistry> `<trustedIssuers>` ます。|  
  
## <a name="remarks"></a>解説  
 Windows Identity Foundation (WIF) は、クラスの1つの実装を、クラスのすぐに使用できるようにし <xref:System.IdentityModel.Tokens.IssuerNameRegistry> <xref:System.IdentityModel.Tokens.ConfigurationBasedIssuerNameRegistry> ます。 構成発行者名レジストリは、構成から読み込まれる信頼された発行者の一覧を保持します。 リストでは、発行者によって生成されたトークンの署名を検証するために必要な x.509 証明書に各発行者名が関連付けられます。 信頼された発行者の証明書の一覧は、要素の下で指定され `<trustedIssuers>` ます。 リスト内の各要素は、ニーモニック発行者名と、その発行者によって生成されるトークンの署名を検証するために必要な x.509 証明書を関連付けます。 信頼された証明書は、asn.1 エンコード形式の証明書の拇印を使用して指定され、要素を使用してコレクションに追加され `<add>` ます。 要素と要素を使用して、一覧から発行者 (証明書) を消去または削除でき `<clear>` `<remove>` ます。  
  
 要素 `type` の属性は、 `<issuerNameRegistry>` 要素を有効にするためにクラスを参照する必要があり <xref:System.IdentityModel.Tokens.ConfigurationBasedIssuerNameRegistry> `<trustedIssuers>` ます。  
  
## <a name="example"></a>例  
 次の XML は、構成ベースの発行者名レジストリを指定する方法を示しています。  
  
```xml  
<issuerNameRegistry type="System.IdentityModel.Tokens.ConfigurationBasedIssuerNameRegistry, System.IdentityModel, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089">  
  <trustedIssuers>  
    <add thumbprint="9B74CB2F32 … B1DC01EF40D0" name="LocalSTS" />  
  </trustedIssuers>  
</issuerNameRegistry>  
```  
  
## <a name="see-also"></a>関連項目

- <xref:System.IdentityModel.Tokens.ConfigurationBasedIssuerNameRegistry>
- <xref:System.IdentityModel.Tokens.IssuerNameRegistry>
