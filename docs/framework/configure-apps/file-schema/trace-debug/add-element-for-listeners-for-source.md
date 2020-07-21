---
title: <add>のの <listeners> 要素<source>
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.diagnostics/sources/source/listeners/add
helpviewer_keywords:
- initializeData attribute
- add element for <listeners> for <source>
- <add> element for <listeners> for <source>
ms.assetid: 4ce36ac1-81ef-48e8-b8b2-b5a5b0e2adcb
ms.openlocfilehash: 883eef32172c5a7f900197995b4c57c3d5a84e19
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "79153686"
---
# <a name="add-element-for-listeners-for-source"></a>\<add>のの \<listeners> 要素\<source>
トレース ソースの `Listeners` コレクションにリスナーを追加します。  

[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.diagnostics>**](system-diagnostics-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<sources>**](sources-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<source>**](source-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<listeners>**](listeners-element-for-source.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<add>**

## <a name="syntax"></a>構文  
  
```xml  
<add name="name"
  type="TraceListenerClassName, Version, Culture, PublicKeyToken"  
  initializeData="data"/>  
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|`type`|必須属性。コレクション内のリスナーを参照している場合を除き、 `sharedListeners` 名前で参照する必要があります ([例](#example)を参照)。<br /><br /> リスナーの種類を指定します。 [「完全修飾型名の指定](../../../reflection-and-codedom/specifying-fully-qualified-type-names.md)」で指定した要件を満たす文字列を使用する必要があります。|  
|`initializeData`|省略可能な属性です。<br /><br /> 指定したクラスのコンストラクターに渡される文字列。 <xref:System.Configuration.ConfigurationException>クラスに文字列を受け取るコンストラクターがない場合は、がスローされます。|  
|`name`|省略可能な属性です。<br /><br /> リスナーの名前を指定します。|  
|`traceOutputOptions`|省略可能な属性です。<br /><br /> <xref:System.Diagnostics.TraceListener.TraceOutputOptions%2A>トレースリスナーのプロパティ値を指定します。|  
|[カスタム属性]|省略可能な属性。<br /><br /> リスナーのメソッドによって識別されるリスナー固有の属性の値を指定し <xref:System.Diagnostics.TraceListener.GetSupportedAttributes%2A> ます。 <xref:System.Diagnostics.DelimitedListTraceListener.Delimiter%2A>は、クラスに固有の追加属性の例です <xref:System.Diagnostics.DelimitedListTraceListener> 。|  
  
### <a name="child-elements"></a>子要素  
  
|要素|Description|  
|-------------|-----------------|  
|[\<filter>](filter-element-for-add-for-listeners-for-source.md)|トレース ソースの `Listeners` コレクション内のリスナーにフィルターを追加します。|  
  
### <a name="parent-elements"></a>親要素  
  
|要素|Description|  
|-------------|-----------------|  
|`configuration`|共通言語ランタイムおよび .NET Framework アプリケーションで使用されるすべての構成ファイルのルート要素です。|  
|`system.diagnostics`|メッセージを収集、格納、およびルーティングするトレース リスナーとトレース スイッチを設定するレベルを指定します。|  
|`sources`|トレース メッセージを開始するトレース ソースを保持します。|  
|`source`|トレース メッセージを開始するトレース ソースを指定します。|  
|`listeners`|メッセージを収集、格納、およびルーティングするリスナーを指定します。|  
  
## <a name="remarks"></a>解説  
 .NET Framework に付属しているリスナークラスは、クラスから派生し <xref:System.Diagnostics.TraceListener> ます。  
  
 トレースリスナーの属性を指定しない場合 `name` 、 <xref:System.Diagnostics.TraceListener.Name%2A> トレースリスナーのプロパティの既定値は空の文字列 ("") になります。 アプリケーションにリスナーが1つしかない場合は、名前を指定せずに追加することができます。名前に空の文字列を指定することで削除できます。 ただし、アプリケーションに複数のリスナーがある場合は、各トレースリスナーに対して一意の名前を指定する必要があります。これにより、コレクション内の個々のトレースリスナーを識別して管理することができ <xref:System.Diagnostics.TraceSource.Listeners%2A?displayProperty=nameWithType> ます。  
  
> [!NOTE]
> 同じ種類の複数のトレースリスナーを同じ名前で追加すると、その型と名前のトレースリスナーは1つだけになり、コレクションに追加され `Listeners` ます。 ただし、プログラムを使用して複数の同じリスナーをコレクションに追加することはでき `Listeners` ます。  
  
 属性の値は、 `initializeData` 作成するリスナーの種類によって異なります。 すべてのトレースリスナーでを指定する必要はありません `initializeData` 。  
  
> [!NOTE]
> 属性を使用すると、 `initializeData` "initializeData" 属性が宣言されていないことを示すコンパイラの警告が表示されることがあります。 この警告は、属性を認識しない抽象基本クラスに対して構成設定が検証されるために発生し <xref:System.Diagnostics.TraceListener> `initializeData` ます。 通常、パラメーターを受け取るコンストラクターを持つトレースリスナーの実装では、この警告を無視できます。  
  
 次の表に、.NET Framework に含まれているトレースリスナーとその属性の値を示し `initializeData` ます。  
  
|トレースリスナークラス|initializeData 属性値|  
|--------------------------|------------------------------------|  
|<xref:System.Diagnostics.ConsoleTraceListener?displayProperty=nameWithType>|`useErrorStream`コンストラクターの値 <xref:System.Diagnostics.ConsoleTraceListener.%23ctor%2A> 。  `initializeData`トレース出力およびデバッグ出力を標準エラーストリームに書き込むには、属性を "" に設定します `true` 。 `false` 標準出力ストリームに書き込むには、"" に設定します。|  
|<xref:System.Diagnostics.DelimitedListTraceListener?displayProperty=nameWithType>|<xref:System.Diagnostics.DelimitedListTraceListener> が出力を書き込むファイルの名前。|  
|<xref:System.Diagnostics.EventLogTraceListener?displayProperty=nameWithType>|既存のイベント ログ ソースの名前。|  
|<xref:System.Diagnostics.EventSchemaTraceListener?displayProperty=nameWithType>|が書き込み先となるファイルの名前 <xref:System.Diagnostics.EventSchemaTraceListener> 。|  
|<xref:System.Diagnostics.TextWriterTraceListener?displayProperty=nameWithType>|が書き込み先となるファイルの名前 <xref:System.Diagnostics.TextWriterTraceListener> 。|  
|<xref:System.Diagnostics.XmlWriterTraceListener?displayProperty=nameWithType>|が書き込み先となるファイルの名前 <xref:System.Diagnostics.XmlWriterTraceListener> 。|  
  
## <a name="configuration-file"></a>構成ファイル  
 この要素は、コンピューターの構成ファイル (machine.config) とアプリケーション構成ファイルで使用できます。  
  
## <a name="example"></a>例  
 次の例では、要素を使用して、 `<add>` リスナー `console` およびを `textListener` `Listeners` トレースソースのコレクションに追加する方法を示し `TraceSourceApp` ます。 リスナーは、 `textListener` トレース出力をファイル myListener .log に書き込みます。  
  
```xml  
<configuration>  
  <system.diagnostics>  
    <sources>  
      <source name="TraceSourceApp" switchName="sourceSwitch"
        switchType="System.Diagnostics.SourceSwitch">  
        <listeners>  
          <add name="console"
            type="System.Diagnostics.ConsoleTraceListener"/>  
          <add name="textListener"/>  
          <remove name="Default"/>  
        </listeners>  
      </source>  
    </sources>  
    <sharedListeners>  
      <add name="textListener"
        type="System.Diagnostics.TextWriterTraceListener"
        initializeData="myListener.log"/>  
    </sharedListeners>  
    <switches>  
      <add name="sourceSwitch" value="Warning"/>  
    </switches>  
  </system.diagnostics>  
</configuration>
```  
  
## <a name="see-also"></a>関連項目

- <xref:System.Diagnostics.TraceSource>
- <xref:System.Diagnostics.TraceListener>
- [トレースおよびデバッグ設定のスキーマ](index.md)
- [トレース リスナー](../../../debug-trace-profile/trace-listeners.md)
