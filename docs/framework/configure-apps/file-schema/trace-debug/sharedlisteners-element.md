---
title: <sharedListeners> 要素
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#sharedListeners
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.diagnostics/sharedListeners
helpviewer_keywords:
- <sharedListeners> element
- listeners
- shared listeners
- trace listeners, <sharedListeners> element
- sharedListeners element
ms.assetid: de200534-19dd-4156-86cf-c50521802c4c
ms.openlocfilehash: 69f15cc9583b397017ac30a0c567914495867c18
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "79153322"
---
# <a name="sharedlisteners-element"></a>\<sharedListeners> 要素
任意の source 要素または trace 要素が参照できるリスナーを含みます。  これらのリスナーは、既定ではトレースを受信せず、実行時にこれらのリスナーを取得することはできません。 共有リスナーとして識別されるリスナーは、名前を指定してソースまたはトレースに追加できます。  
  
[**\<configuration>**](../configuration-element.md)  
&nbsp;&nbsp;[**\<system.diagnostics>**](system-diagnostics-element.md)  
&nbsp;&nbsp;&nbsp;&nbsp;**\<sharedListeners>**  
  
## <a name="syntax"></a>構文  
  
```xml  
<sharedListeners>
  <add>...</add>  
</sharedListeners>  
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
 なし。  
  
### <a name="child-elements"></a>子要素  
  
|要素|説明|  
|-------------|-----------------|  
|[\<add>](add-element-for-listeners-for-trace.md)|`sharedListeners` コレクションにリスナーを追加します。|  
  
### <a name="parent-elements"></a>親要素  
  
|要素|説明|  
|-------------|-----------------|  
|`Configuration`|共通言語ランタイムおよび .NET Framework アプリケーションで使用されるすべての構成ファイルのルート要素です。|  
|`system.diagnostics`|ASP.NET 構成セクションのルート要素を指定します。|  
  
## <a name="remarks"></a>解説  
 リスナーを共有リスナーコレクションに追加しても、それがアクティブなリスナーになることはありません。 トレースソースまたはトレースに追加するには、そのトレース要素のコレクションに追加する必要があり `Listeners` ます。 .NET Framework 内のリスナークラスは、クラスから派生し <xref:System.Diagnostics.TraceListener> ます。  
  
 この要素は、コンピューターの構成ファイル (machine.config) とアプリケーション構成ファイルで使用できます。  
  
## <a name="example"></a>例  
 次の例は、要素を使用し `<sharedListeners>` `console` て、 `Listeners` クラスとクラスの両方のコレクションにリスナーを追加する方法を示して <xref:System.Diagnostics.TraceSource> <xref:System.Diagnostics.Trace> います。 コンソールトレースリスナーは、またはの呼び出しを通じて、トレース情報をコンソールに書き込み <xref:System.Diagnostics.TraceSource> <xref:System.Diagnostics.Trace> ます。  
  
```xml  
<configuration>  
  <system.diagnostics>  
    <sharedListeners>  
      <add name="console" type="System.Diagnostics.ConsoleTraceListener" >  
        <filter type="System.Diagnostics.EventTypeFilter"  
          initializeData="Warning" />  
      </add>  
    </sharedListeners>  
    <sources>  
      <source name="mySource" switchName="sourceSwitch"  >  
        <listeners>  
          <add name="console" />  
        </listeners>  
      </source>  
    </sources>  
    <switches>  
      <add name="sourceSwitch" value="Verbose"/>  
    </switches>  
    <trace>  
      <listeners>  
        <add name="console" />  
      </listeners>  
    </trace>  
  </system.diagnostics>  
</configuration>
```  
  
## <a name="see-also"></a>関連項目

- <xref:System.Diagnostics.TraceListener>
- [トレースおよびデバッグ設定のスキーマ](index.md)
- [トレース リスナー](../../../debug-trace-profile/trace-listeners.md)
