---
title: <claimsAuthorizationManager>
ms.date: 03/30/2017
ms.assetid: 9354eee3-f692-4ad6-8427-3169686b8bcc
author: BrucePerlerMS
ms.openlocfilehash: ddbe8a862940272e4192a3f4c0abdc1f9e8b5d48
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "70252079"
---
# \<claimsAuthorizationManager>
入力方向の要求に対して要求承認マネージャーを登録します。  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.identityModel>**](system-identitymodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<identityConfiguration>**](identityconfiguration.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<claimsAuthorizationManager>**  
  
## <a name="syntax"></a>構文  
  
```xml  
<system.identityModel>  
  <identityConfiguration>  
    <claimsAuthorizationManager type = xs:string>  
      <optionalConfigurationElements />  
    </claimsAuthorizationManager>  
  </identityConfiguration>  
</system.identityModel>  
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|type|クラスから派生するカスタム型 <xref:System.Security.Claims.ClaimsAuthorizationManager> 。 属性を指定する方法の詳細については `type` 、「[カスタム型参照](../windows-workflow-foundation/index.md)」を参照してください。|  
  
### <a name="child-elements"></a>子要素  
 属性が存在しない場合、 `type` または属性がクラスを参照している場合、 `type` 要素は <xref:System.Security.Claims.ClaimsAuthenticationManager> `<claimsAuthorizationManager>` 子要素を受け取りません。ただし、から派生したクラス <xref:System.Security.Claims.ClaimsAuthorizationManager> は子構成要素を定義できます。  
  
### <a name="parent-elements"></a>親要素  
  
|要素|Description|  
|-------------|-----------------|  
|[\<identityConfiguration>](identityconfiguration.md)|サービスレベルの id 設定を指定します。|  
  
## <a name="remarks"></a>解説  
 クラスによって提供される既定の動作では、 <xref:System.Security.Claims.ClaimsAuthorizationManager> 常に入力方向の要求が承認されます。 属性が指定されていない場合、 `type` または属性でクラスが指定されている場合、 `type` <xref:System.Security.Claims.ClaimsAuthorizationManager> 要素は `<claimsAuthorizationManager>` 子要素を受け取りません。 属性を指定して、 `type` クラスから派生した型を登録し、 <xref:System.Security.Claims.ClaimsAuthorizationManager> カスタム動作を実装することができます。 派生クラスでは、要素の子要素を使用した構成をサポートできます。これを行う `<claimsAuthorizationManager>` には、メソッドをオーバーライドして <xref:System.Security.Claims.ClaimsAuthorizationManager.LoadCustomConfiguration%2A> これらの要素を処理します。 子要素に対して定義されているスキーマは、クラスのデザイナーによって作成されます。  
  
> [!IMPORTANT]
> クラスまたはクラスを使用して、 <xref:System.IdentityModel.Services.ClaimsPrincipalPermission> <xref:System.IdentityModel.Services.ClaimsPrincipalPermissionAttribute> コード内にクレームベースのアクセス制御を提供する場合、要素によって参照される id 構成によって、 `<federationConfiguration>` 承認の決定に使用される要求承認マネージャーとポリシーが構成されます。 これは、Windows Communication Foundation (WCF) アプリケーションや Web ベースではないアプリケーションなど、パッシブな Web シナリオではないシナリオでも当てはまります。 アプリケーションがパッシブな Web アプリケーションでない場合は、 `<claimsAuthorizationManager>` 参照される id 構成の要素 (およびその子ポリシー要素が存在する場合) が適用される唯一の設定です。 その他すべての設定は無視されます。 詳細については、要素を参照してください [\<federationConfiguration>](federationconfiguration.md) 。  
  
 この要素は、 <xref:System.IdentityModel.Configuration.IdentityConfiguration.ClaimsAuthorizationManager%2A?displayProperty=nameWithType> プロパティを設定します。  
  
## <a name="example"></a>例  
 次の XML は、リソースアクションのペアで構成されるポリシーを実装するクレーム承認マネージャーの構成を示しています。これらのポリシーは、要求元がリソースに対してアクションを実行するために必要なクレームのブール値の組み合わせを指定します。 このポリシーを使用できる要求承認マネージャーを実装するコードについては、「」のサンプルを参照して `ClaimsBasedAuthorization` ください。  
  
```xml  
<system.identityModel>  
    <identityConfiguration>  
      <claimsAuthorizationManager type="ClaimsAuthorizationLibrary.MyClaimsAuthorizationManager, ClaimsAuthorizationLibrary">  
        <policy resource="http://localhost:28491/Developers.aspx" action="GET">  
          <or>  
            <claim claimType="http://schemas.microsoft.com/ws/2008/06/identity/claims/role" claimValue="developer" />  
            <claim claimType="http://schemas.xmlsoap.org/claims/Group" claimValue="Administrator" />  
          </or>  
        </policy>  
        <policy resource="http://localhost:28491/Administrators.aspx" action="GET">  
          <and>  
            <claim claimType="http://schemas.xmlsoap.org/claims/Group" claimValue="Administrator" />  
            <claim claimType="http://schemas.xmlsoap.org/ws/2005/05/identity/claims/country" claimValue="USA" />  
          </and>  
        </policy>  
        <policy resource="http://localhost:28491/Default.aspx" action="GET">  
        </policy>  
        <policy resource="http://localhost:28491/" action="GET">  
        </policy>  
        <policy resource="http://localhost:28491/Claims.aspx" action="GET">  
        </policy>  
      </claimsAuthorizationManager>  
    <identityConfiguration>  
<system.identityModel>  
```
