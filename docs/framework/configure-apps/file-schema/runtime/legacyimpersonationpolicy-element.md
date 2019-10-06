---
title: <legacyImpersonationPolicy> 要素
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#legacyImpersonationPolicy
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/runtime/legacyImpersonationPolicy
helpviewer_keywords:
- <legacyImpersonationPolicy> element
- legacyImpersonationPolicy element
ms.assetid: 6e00af10-42f3-4235-8415-1bb2db78394e
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: cd09598800b74c4807163bc921806f5b470e0d24
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2019
ms.locfileid: "70252497"
---
# <a name="legacyimpersonationpolicy-element"></a>\<legacyImpersonationPolicy> 要素
Windows ID が、現在のスレッドの実行コンテキストのフロー設定に関係なく、非同期ポイント間でフローしないことを指定します。  
  
[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<runtime>** ](runtime-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp; **\<legacyImpersonationPolicy>**  
  
## <a name="syntax"></a>構文  
  
```xml  
<legacyImpersonationPolicy    
   enabled="true|false"/>  
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|`enabled`|必須の属性です。<br /><br /> 現在のスレッド<xref:System.Security.Principal.WindowsIdentity>の<xref:System.Threading.ExecutionContext>フロー設定に関係なく、が非同期ポイント間でフローしないように指定します。|  
  
## <a name="enabled-attribute"></a>enabled 属性  
  
|値|説明|  
|-----------|-----------------|  
|`false`|<xref:System.Security.Principal.WindowsIdentity>現在のスレッドのフロー設定に<xref:System.Threading.ExecutionContext>応じて、非同期ポイント間をフローします。 既定値です。|  
|`true`|<xref:System.Security.Principal.WindowsIdentity>は、現在のスレッドの<xref:System.Threading.ExecutionContext>フロー設定に関係なく、非同期ポイント間ではフローしません。|  
  
### <a name="child-elements"></a>子要素  
 なし。  
  
### <a name="parent-elements"></a>親要素  
  
|要素|説明|  
|-------------|-----------------|  
|`configuration`|共通言語ランタイムおよび .NET Framework アプリケーションで使用されるすべての構成ファイルのルート要素です。|  
|`runtime`|アセンブリのバインディングとガベージ コレクションに関する情報が含まれています。|  
  
## <a name="remarks"></a>Remarks  
 .NET Framework バージョン1.0 および1.1 では、は<xref:System.Security.Principal.WindowsIdentity>ユーザー定義の非同期ポイント間ではフローしません。 .NET Framework バージョン2.0 以降では、現在実行中<xref:System.Threading.ExecutionContext>のスレッドに関する情報を格納するオブジェクトが存在し、アプリケーションドメイン内の非同期ポイント間をフローします。 は<xref:System.Security.Principal.WindowsIdentity> 、この実行コンテキストに含まれているため、非同期ポイント間でもフローします。つまり、権限借用コンテキストが存在する場合は、同様にフローが行われます。  
  
 .NET Framework 2.0 以降では、 `<legacyImpersonationPolicy>`要素を使用して、が非同期ポイント間でフローしないこと<xref:System.Security.Principal.WindowsIdentity>を指定できます。  
  
> [!NOTE]
> 共通言語ランタイム (CLR) は、マネージコードの外部で実行される偽装操作 (アンマネージコードへのプラットフォーム呼び出し、Win32 関数への直接呼び出しなど) を使用して実行される偽装操作を認識します。 要素が<xref:System.Security.Principal.WindowsIdentity> true(`<alwaysFlowImpersonationPolicy enabled="true"/>`) に設定されていない限り、非同期のポイント間でフローできるのはマネージオブジェクトだけです。 `alwaysFlowImpersonationPolicy` `alwaysFlowImpersonationPolicy`要素を true に設定すると、偽装がどのように実行されたかに関係なく、Windows id が常に非同期のポイントでフローすることを指定します。 非同期ポイント間でアンマネージ偽装をフローする方法の詳細については、「 [ \<alwaysFlowImpersonationPolicy> 要素](alwaysflowimpersonationpolicy-element.md)」を参照してください。  
  
 この既定の動作は、次の2つの方法で変更できます。  
  
1. マネージコード内で、スレッド単位で。  
  
     <xref:System.Threading.ExecutionContext.SuppressFlow%2A?displayProperty=nameWithType>、、 <xref:System.Threading.ExecutionContext> または<xref:System.Security.SecurityContext.SuppressFlow%2A?displayProperty=nameWithType>メソッドを使用してと<xref:System.Security.SecurityContext>の設定を変更することで、スレッド単位でフローを抑制できます。 <xref:System.Security.SecurityContext.SuppressFlowWindowsIdentity%2A?displayProperty=nameWithType>  
  
2. アンマネージホストインターフェイスを呼び出して、共通言語ランタイム (CLR) を読み込みます。  
  
     アンマネージホストインターフェイス (単純なマネージ実行可能ファイルではなく) を使用して CLR を読み込む場合は、 [Corbindtoruntimeex 関数](../../../unmanaged-api/hosting/corbindtoruntimeex-function.md)関数の呼び出しで特別なフラグを指定できます。 プロセス全体で互換モードを有効にするには、 `flags` [corbindtoruntimeex 関数](../../../unmanaged-api/hosting/corbindtoruntimeex-function.md)のパラメーターを STARTUP_LEGACY_IMPERSONATION に設定します。  
  
 詳細については、「 [ \<alwaysFlowImpersonationPolicy> 要素](alwaysflowimpersonationpolicy-element.md)」を参照してください。  
  
## <a name="configuration-file"></a>構成ファイル  
 .NET Framework アプリケーションでは、この要素はアプリケーション構成ファイルでのみ使用できます。  
  
 ASP.NET アプリケーションの場合、偽装フローは、 \<Windows フォルダー> \Microsoft.NET\Framework\vx.x.xxxx ディレクトリにある aspnet ファイルで構成できます。  
  
 ASP.NET は、既定では、次の構成設定を使用して、aspnet ファイル内の偽装フローを無効にします。  
  
``` xml
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
 次の例は、非同期ポイント間で Windows id をフローしない従来の動作を指定する方法を示しています。  
  
```xml  
<configuration>  
   <runtime>  
      <legacyImpersonationPolicy enabled="true"/>  
   </runtime>  
</configuration>  
```  
  
## <a name="see-also"></a>関連項目

- [ランタイム設定スキーマ](index.md)
- [構成ファイル スキーマ](../index.md)
- [\<alwaysFlowImpersonationPolicy> 要素](alwaysflowimpersonationpolicy-element.md)
