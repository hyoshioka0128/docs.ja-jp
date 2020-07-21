---
title: <alwaysFlowImpersonationPolicy> 要素
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/runtime/alwaysFlowImpersonationPolicy
- http://schemas.microsoft.com/.NetConfiguration/v2.0#alwaysFlowImpersonationPolicy
helpviewer_keywords:
- alwaysFlowImpersonationPolicy element
- <alwaysFlowImpersonationPolicy> element
ms.assetid: ee622801-9e46-470b-85ab-88c4b1dd2ee1
ms.openlocfilehash: 7c8ac37932a528ff0f000cbaab49124dec51b88c
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "79154484"
---
# <a name="alwaysflowimpersonationpolicy-element"></a>\<alwaysFlowImpersonationPolicy> 要素
偽装の実行方法に関係なく、Windows ID が常に非同期ポイント間でフローすることを指定します。  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<runtime>**](runtime-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;**\<alwaysFlowImpersonationPolicy>**\  
  
## <a name="syntax"></a>構文  
  
```xml  
<alwaysFlowImpersonationPolicy
  enabled="true|false"/>  
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|`enabled`|必須の属性です。<br /><br /> Windows id が非同期ポイント間でフローするかどうかを示します。|  
  
## <a name="enabled-attribute"></a>enabled 属性  
  
|値|Description|  
|-----------|-----------------|  
|`false`|などのマネージメソッドを使用して偽装を実行しない限り、Windows id は非同期ポイント間ではフローしません <xref:System.Security.Principal.WindowsIdentity.Impersonate%2A> 。 既定値です。|  
|`true`|Windows id は、偽装がどのように実行されたかに関係なく、常に非同期のポイント間でフローします。|  
  
### <a name="child-elements"></a>子要素  
 なし。  
  
### <a name="parent-elements"></a>親要素  
  
|要素|Description|  
|-------------|-----------------|  
|`configuration`|共通言語ランタイムおよび .NET Framework アプリケーションで使用されるすべての構成ファイルのルート要素です。|  
|`runtime`|アセンブリのバインディングとガベージ コレクションに関する情報が含まれています。|  
  
## <a name="remarks"></a>解説  
 .NET Framework バージョン1.0 および1.1 では、Windows id は非同期ポイント間ではフローしません。 .NET Framework バージョン2.0 では、 <xref:System.Threading.ExecutionContext> 現在実行中のスレッドに関する情報を格納するオブジェクトがあり、アプリケーションドメイン内の非同期ポイント間でフローします。 また、は、 <xref:System.Security.Principal.WindowsIdentity> 非同期ポイント全体をフローする情報の一部としてもフローします。これは、などのマネージメソッドを使用して偽装が行われた場合に、 <xref:System.Security.Principal.WindowsIdentity.Impersonate%2A> ネイティブメソッドへのプラットフォーム呼び出しなどの他の方法を使用して行われなかった場合に限ります。 この要素は、偽装がどのように実現されたかに関係なく、Windows id が非同期ポイント間でフローすることを指定するために使用されます。  
  
 この既定の動作は、次の2つの方法で変更できます。  
  
1. マネージコード内で、スレッド単位で。  
  
     <xref:System.Threading.ExecutionContext> <xref:System.Security.SecurityContext> <xref:System.Threading.ExecutionContext.SuppressFlow%2A?displayProperty=nameWithType> 、 <xref:System.Security.SecurityContext.SuppressFlowWindowsIdentity%2A?displayProperty=nameWithType> 、またはメソッドを使用しておよび設定を変更することで、スレッド単位でフローを抑制でき <xref:System.Security.SecurityContext.SuppressFlow%2A?displayProperty=nameWithType> ます。  
  
2. アンマネージホストインターフェイスを呼び出して、共通言語ランタイム (CLR) を読み込みます。  
  
     アンマネージホストインターフェイス (単純なマネージ実行可能ファイルではなく) を使用して CLR を読み込む場合は、 [Corbindtoruntimeex 関数](../../../unmanaged-api/hosting/corbindtoruntimeex-function.md)関数の呼び出しで特別なフラグを指定できます。 プロセス全体で互換モードを有効にするには、 `flags` [Corbindtoruntimeex 関数](../../../unmanaged-api/hosting/corbindtoruntimeex-function.md)のパラメーターをに設定し `STARTUP_ALWAYSFLOW_IMPERSONATION` ます。  
  
## <a name="configuration-file"></a>構成ファイル  
 .NET Framework アプリケーションでは、この要素はアプリケーション構成ファイルでのみ使用できます。  
  
 ASP.NET アプリケーションでは、\Microsoft.NET\Framework\vx.x.xxxx ディレクトリにある aspnet ファイルで偽装フローを構成でき \<Windows Folder> ます。  
  
 ASP.NET は、既定では、次の構成設定を使用して、aspnet ファイル内の偽装フローを無効にします。  
  
```xml
<configuration>  
   <runtime>  
      <legacyImpersonationPolicy enabled="true"/>  
      <alwaysFlowImpersonationPolicy enabled="false"/>  
   </runtime>  
</configuration>  
```  
  
 ASP.NET で、代わりに偽装のフローを許可する場合は、次の構成設定を明示的に使用する必要があります。  
  
```xml  
<configuration>  
   <runtime>  
      <legacyImpersonationPolicy enabled="false"/>  
      <alwaysFlowImpersonationPolicy enabled="true"/>  
   </runtime>  
</configuration>  
```  
  
## <a name="example"></a>例  
 次の例では、マネージメソッド以外の方法で権限借用が行われた場合でも、Windows id を非同期ポイント間でフローするように指定する方法を示します。  
  
```xml  
<configuration>  
  <runtime>  
    <alwaysFlowImpersonationPolicy enabled="true"/>  
  </runtime>  
</configuration>  
```  
  
## <a name="see-also"></a>関連項目

- [ランタイム設定スキーマ](index.md)
- [構成ファイル スキーマ](../index.md)
- [\<legacyImpersonationPolicy>Element](legacyimpersonationpolicy-element.md)
