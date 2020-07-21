---
title: <claimsAuthenticationManager>
ms.date: 03/30/2017
ms.assetid: 6d30a450-6d13-4671-81a8-77e0204500c5
author: BrucePerlerMS
ms.openlocfilehash: a54fc2cea84bb9d08a9725d846fe38efd7b5475a
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "79152750"
---
# \<claimsAuthenticationManager>
入力方向の要求に対して要求認証マネージャーを登録します。  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.identityModel>**](system-identitymodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<identityConfiguration>**](identityconfiguration.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<claimsAuthenticationManager>**  
  
## <a name="syntax"></a>構文  
  
```xml  
<system.identityModel>  
  <identityConfiguration>  
    <claimsAuthenticationManager type=xs:string>  
      <optionalConfigurationElements />  
    </claimsAuthenticationManager>  
  </identityConfiguration>  
</system.identityModel>  
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|type|クラスから派生するカスタム型を指定し <xref:System.Security.Claims.ClaimsAuthenticationManager> ます。 属性を指定する方法の詳細については `type` 、「[カスタム型参照]」を参照してください。|  
  
### <a name="child-elements"></a>子要素  
 属性が存在しない場合、 `type` または属性がクラスを参照している場合、 `type` 要素は <xref:System.Security.Claims.ClaimsAuthenticationManager> `<claimsAuthenticationManager>` 子要素を受け取りません。ただし、から派生したクラス <xref:System.Security.Claims.ClaimsAuthenticationManager> は子構成要素を定義できます。  
  
### <a name="parent-elements"></a>親要素  
  
|要素|Description|  
|-------------|-----------------|  
|[\<identityConfiguration>](identityconfiguration.md)|サービスレベルの id 設定を指定します。|  
  
## <a name="remarks"></a>解説  
 クラスによって提供される既定の動作では、 <xref:System.Security.Claims.ClaimsAuthenticationManager> 入力方向の要求がエコーされます。 属性が指定されていない場合、 `type` または属性でクラスが指定されている場合、 `type` <xref:System.Security.Claims.ClaimsAuthenticationManager> 要素は `<claimsAuthenticationManager>` 子要素を受け取りません。 属性を指定して、 `type` クラスから派生した型を登録し、 <xref:System.Security.Claims.ClaimsAuthenticationManager> カスタム動作を実装することができます。 派生クラスでは、要素の子要素を使用した構成をサポートできます。これを行う `<claimsAuthenticationManager>` には、メソッドをオーバーライドして <xref:System.Security.Claims.ClaimsAuthenticationManager.LoadCustomConfiguration%2A> これらの要素を処理します。 子要素に対して定義されているスキーマは、クラスのデザイナーによって作成されます。  
  
 要素は、 `<claimsAuthenticationManager>` プロパティを設定し <xref:System.IdentityModel.Configuration.IdentityConfiguration.ClaimsAuthenticationManager%2A?displayProperty=nameWithType> ます。  
  
## <a name="example"></a>例  
  
```xml  
<system.identityModel>  
    <identityConfiguration name="MyIdentity">  
      <claimsAuthenticationManager type="MyNamespace.CustomClaimsAuthenticationManager, MyAssembly"/>
    </identityConfiguration>  
</system.identityModel>  
```
