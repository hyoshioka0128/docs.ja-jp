---
title: <serviceTokenResolver>
ms.date: 03/30/2017
ms.assetid: 6e9001e1-e064-4f47-84b2-46225c177746
author: BrucePerlerMS
ms.openlocfilehash: 0983380e553acfe246d6b987784d818b8ae85b17
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "79152581"
---
# \<serviceTokenResolver>
トークンハンドラーコレクションのハンドラーによって使用されるサービストークンリゾルバーを登録します。 サービストークンリゾルバーは、受信トークンとメッセージの暗号化トークンを解決するために使用されます。  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.identityModel>**](system-identitymodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<identityConfiguration>**](identityconfiguration.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<securityTokenHandlers>**](securitytokenhandlers.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<securityTokenHandlerConfiguration>**](securitytokenhandlerconfiguration.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<serviceTokenResolver>**  
  
## <a name="syntax"></a>構文  
  
```xml  
<system.identityModel>  
  <identityConfiguration>  
    <securityTokenHandlers>  
      <securityTokenHandlerConfiguration>  
        <serviceTokenResolver type=xs:string>  
        </serviceTokenResolver>  
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
|type|サービストークンリゾルバーの種類を指定します。 <xref:System.IdentityModel.Selectors.SecurityTokenResolver>クラスから派生した型または型 <xref:System.IdentityModel.Selectors.SecurityTokenResolver> 。 属性を指定する方法の詳細については `type` 、「[カスタム型参照]」を参照してください。 必須。|  
  
### <a name="child-elements"></a>子要素  
 なし  
  
### <a name="parent-elements"></a>親要素  
  
|要素|Description|  
|-------------|-----------------|  
|[\<securityTokenHandlerConfiguration>](securitytokenhandlerconfiguration.md)|セキュリティトークンハンドラーのコレクションの構成を提供します。|  
  
## <a name="remarks"></a>解説  
 サービストークンリゾルバーを使用して、受信トークンとメッセージの暗号化トークンを解決できます。 これは、受信トークンの暗号化を解除するために使用する必要があるキーを取得するために使用されます。 属性を指定する必要があり `type` ます。 指定できる型は、 <xref:System.IdentityModel.Selectors.SecurityTokenResolver> またはクラスから派生したカスタム型のいずれか <xref:System.IdentityModel.Selectors.SecurityTokenResolver> です。  
  
 一部のトークンハンドラーでは、構成でサービストークンリゾルバーの設定を指定できます。 個々のトークンハンドラーの設定は、セキュリティトークンハンドラーコレクションで指定された設定よりも優先されます。  
  
> [!NOTE]
> 要素 `<serviceTokenResolver>` の子要素としての指定 [\<identityConfiguration>](identityconfiguration.md) は非推奨とされましたが、旧バージョンとの互換性のために引き続きサポートされています。 要素の設定は、要素の設定 `<securityTokenHandlerConfiguration>` よりも優先さ `<identityConfiguration>` れます。  
  
## <a name="example"></a>例  
  
```xml  
<serviceTokenResolver type="MyNamespace.CustomTokenResolver, MyAssembly" />  
```
