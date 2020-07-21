---
title: <runtime> の <assemblyIdentity> 要素
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/runtime/assemblyBinding/dependentAssembly/assemblyIdentity
- http://schemas.microsoft.com/.NetConfiguration/v2.0#assemblyIdentity
helpviewer_keywords:
- <assemblyIdentity> element
- container tags, <assemblyIdentity> element
- assemblyIdentity element
ms.assetid: cea4d187-6398-4da4-af09-c1abc6a349c1
ms.openlocfilehash: b026dafbde796bbd8726de56b532ed6710ba2290
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "79154310"
---
# <a name="assemblyidentity-element-for-runtime"></a>\<runtime> の \<assemblyIdentity> 要素
アセンブリに関する識別情報を格納します。  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<runtime>**](runtime-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<assemblyBinding>**](assemblybinding-element-for-runtime.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<dependentAssembly>**](dependentassembly-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<assemblyIdentity>**  
  
## <a name="syntax"></a>構文  
  
```xml  
   <assemblyIdentity
name="assembly name"  
publicKeyToken="public key token"  
culture="assembly culture"/>  
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|`name`|必須の属性です。<br /><br /> アセンブリの名前|  
|`culture`|省略可能な属性です。<br /><br /> アセンブリの言語と国/地域を指定する文字列。|  
|`publicKeyToken`|省略可能な属性です。<br /><br /> アセンブリの厳密な名前を指定する16進値。|  
|`processorArchitecture`|省略可能な属性です。<br /><br /> プロセッサ固有のコードを含むアセンブリのプロセッサアーキテクチャを指定する、"x86"、"amd64"、"msil"、または "ia64" のいずれかの値。 値の大文字と小文字は区別されません。 属性に他の値が割り当てられている場合は、 `<assemblyIdentity>` 要素全体が無視されます。 以下を参照してください。<xref:System.Reflection.ProcessorArchitecture>|  
  
## <a name="processorarchitecture-attribute"></a>processorArchitecture 属性  
  
|値|Description|  
|-----------|-----------------|  
|`amd64`|AMD x86-64 アーキテクチャのみ。|  
|`ia64`|Intel Itanium アーキテクチャのみ。|  
|`msil`|プロセッサおよびワードあたりのビット数に関して中立|  
|`x86`|64ビットプラットフォーム上のネイティブまたは Windows on Windows (WOW) 環境の32ビット x86 プロセッサ。|  
  
### <a name="child-elements"></a>子要素  
 なし。  
  
### <a name="parent-elements"></a>親要素  
  
|要素|Description|  
|-------------|-----------------|  
|`assemblyBinding`|アセンブリ バージョンのリダイレクトおよびアセンブリの位置に関する情報が含まれます。|  
|`configuration`|共通言語ランタイムおよび .NET Framework アプリケーションで使用されるすべての構成ファイルのルート要素です。|  
|`dependentAssembly`|各アセンブリのバインディング ポリシーとアセンブリの場所をカプセル化します。 `<dependentAssembly>`アセンブリごとに1つの要素を使用します。|  
|`runtime`|アセンブリのバインディングとガベージ コレクションに関する情報が含まれています。|  
  
## <a name="remarks"></a>解説  
 すべて **\<dependentAssembly>** の要素には1つ **\<assemblyIdentity>** の子要素が必要です。  
  
 `processorArchitecture`属性が存在する場合、要素は、 `<assemblyIdentity>` 対応するプロセッサアーキテクチャを持つアセンブリにのみ適用されます。 `processorArchitecture`属性が存在しない場合、要素は、 `<assemblyIdentity>` 任意のプロセッサアーキテクチャを持つアセンブリに適用できます。  
  
 次の例では、2つの異なる2つのプロセッサアーキテクチャを対象とする同じ名前の2つのアセンブリの構成ファイルを示しています。これらのバージョンは、同期中に保持されていません。X86 プラットフォームでアプリケーションを実行すると、最初の `<assemblyIdentity>` 要素が適用され、もう一方の要素は無視されます。 アプリケーションが x86 または ia64 以外のプラットフォームで実行されている場合は、両方とも無視されます。  
  
```xml  
<configuration>  
   <runtime>  
      <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">  
         <dependentAssembly>  
            <assemblyIdentity name="MyAssembly"  
                  publicKeyToken="14a739be0244c389"  
                  culture="neutral"  
                  processorArchitecture="x86" />  
            <bindingRedirect oldVersion= "1.0.0.0"
                  newVersion="1.1.0.0" />  
         </dependentAssembly>  
         <dependentAssembly>  
            <assemblyIdentity name="MyAssembly"  
                  publicKeyToken="14a739be0244c389"  
                  culture="neutral"
                  processorArchitecture="ia64" />  
            <bindingRedirect oldVersion="1.0.0.0"
                  newVersion="2.0.0.0" />  
         </dependentAssembly>  
      </assemblyBinding>  
   </runtime>  
</configuration>  
```  
  
 属性のない要素が構成ファイルに含まれて `<assemblyIdentity>` `processorArchitecture` おり、プラットフォームに一致する要素が含まれていない場合、属性のない要素 `processorArchitecture` が使用されます。  
  
## <a name="example"></a>例  
 次の例は、アセンブリに関する情報を提供する方法を示しています。  
  
```xml  
<configuration>  
   <runtime>  
      <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">  
         <dependentAssembly>  
            <assemblyIdentity name="myAssembly"  
                              publicKeyToken="32ab4ba45e0a69a1"  
                              culture="neutral" />  
            <!--Redirection and codeBase policy for myAssembly.-->  
         </dependentAssembly>  
      </assemblyBinding>  
   </runtime>  
</configuration>  
```  
  
## <a name="see-also"></a>関連項目

- [ランタイム設定スキーマ](index.md)
- [構成ファイル スキーマ](../index.md)
- [アセンブリ バージョンのリダイレクト](../../redirect-assembly-versions.md)
