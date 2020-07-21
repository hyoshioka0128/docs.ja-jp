---
title: <filter>のの <add> 要素 <listeners><source>
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#filter
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.diagnostics/sources/source/listeners/add/filter
helpviewer_keywords:
- initializeData attribute
- <filter> element for <add> for <listeners> for <source>
- filter element for <add> for <listeners> for <source>
ms.assetid: 15808b80-4579-4c25-b385-178cfdf154ba
ms.openlocfilehash: 0cb668782de263d5f784691f46cb8b74541d942b
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "79153517"
---
# <a name="filter-element-for-add-for-listeners-for-source"></a>\<filter>のの \<add> 要素 \<listeners>\<source>
トレース ソースの `Listeners` コレクション内のリスナーにフィルターを追加します。  

[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.diagnostics>**](system-diagnostics-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<sources>**](sources-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<source>**](source-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<listeners>**](listeners-element-for-source.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<add>**](add-element-for-listeners-for-source.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<filter>**

## <a name="syntax"></a>構文  
  
```xml  
<filter
  type="traceFilterClassName"
  initializeData="data" />  
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|`type`|必須の属性です。<br /><br /> フィルターの種類を指定します。この型はクラスから継承する必要があり <xref:System.Diagnostics.TraceFilter> ます。 型の名前空間で修飾された名前を使用できます。これは、型のプロパティに対応し <xref:System.Type.FullName%2A> ます。または、プロパティに対応するアセンブリ情報を含む完全修飾型名を使用することもでき <xref:System.Type.AssemblyQualifiedName%2A> ます。 完全修飾型名の詳細については、「[完全修飾型名の指定](../../../reflection-and-codedom/specifying-fully-qualified-type-names.md)」を参照してください。|  
|`initializeData`|省略可能な属性です。<br /><br /> 指定されたフィルタークラスのコンストラクターに渡される文字列。|  
  
### <a name="child-elements"></a>子要素  
 なし。  
  
### <a name="parent-elements"></a>親要素  
  
|要素|Description|  
|-------------|-----------------|  
|`configuration`|共通言語ランタイムおよび .NET Framework アプリケーションで使用されるすべての構成ファイルのルート要素です。|  
|`system.diagnostics`|メッセージを収集、格納、およびルーティングするトレース リスナーとトレース スイッチを設定するレベルを指定します。|  
|`sources`|トレース メッセージを開始するトレース ソースを保持します。|  
|`source`|トレース メッセージを開始するトレース ソースを指定します。|  
|`listeners`|メッセージを収集、格納、およびルーティングするリスナーを格納します。 リスナーは、適切なターゲットにトレース出力を送信します。|  
|`add`|トレース ソースの `Listeners` コレクションにリスナーを追加します。|  
  
## <a name="remarks"></a>解説  
 `<filter>`要素は `<add>` 、で定義されているリスナーの名前だけでなく、リスナーの種類を指定するトレースソースリスナーの要素に格納されている必要があり [\<sharedListeners>](sharedlisteners-element.md) ます。 リスナーがで定義されている場合は [\<sharedListeners>](sharedlisteners-element.md) 、そのリスナーのフィルターをその要素で定義する必要があります。  
  
 この要素は、コンピューターの構成ファイル (machine.config) とアプリケーション構成ファイルで使用できます。  
  
## <a name="example"></a>例  
 次の例では、要素を使用して、フィルター `<filter>` `console` `Listeners` イベントレベルをとして指定し、トレースソースのコレクション内のリスナーにフィルターを追加する方法を示し `myTraceSource` `Error` ます。  
  
```xml  
<configuration>  
  <system.diagnostics>  
    <sources>  
      <source name="myTraceSource" switchName="SourceSwitch"
        switchType="System.Diagnostics.SourceSwitch"  >  
        <listeners>  
          <add name="console"
            type="System.Diagnostics.ConsoleTraceListener" >  
            <filter type="System.Diagnostics.EventTypeFilter"
              initializeData="Error" />  
          </add>  
          <remove name="Default" />  
        </listeners>  
      </source>  
    </sources>  
    <switches>  
      <add name="SourceSwitch" value="Warning" />  
    </switches>  
  </system.diagnostics>  
</configuration>  
```  
  
## <a name="see-also"></a>関連項目

- <xref:System.Diagnostics.TraceSource>
- <xref:System.Diagnostics.TraceListener>
- <xref:System.Diagnostics.TraceListener.Filter%2A?displayProperty=nameWithType>
- <xref:System.Diagnostics.TraceFilter>
- [トレースおよびデバッグ設定のスキーマ](index.md)
