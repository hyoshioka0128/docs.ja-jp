---
title: <sharedListeners> の <add> 要素
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.diagnostics/sharedListeners/add
helpviewer_keywords:
- initializeData attribute
- <add> element for <sharedListeners>
- add element for <sharedListeners>
ms.assetid: 1595e1bc-2492-421f-8384-7f382eb8eb57
ms.openlocfilehash: 5588892ec75a791eda1eb043936c0af95e79354e
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "79153608"
---
# <a name="add-element-for-sharedlisteners"></a>\<sharedListeners> の \<add> 要素
`sharedListeners` コレクションにリスナーを追加します。 `sharedListeners`[\<source>](source-element.md)またはが参照できるリスナーのコレクションです [\<trace>](trace-element.md) 。  既定では、コレクション内のリスナー `sharedListeners` はコレクション内に配置されません `Listeners` 。 これらは、またはに名前で追加する必要があり [\<source>](source-element.md) [\<trace>](trace-element.md) ます。 実行時にコードでコレクション内のリスナーを取得することはできません `sharedListeners` 。  

[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.diagnostics>**](system-diagnostics-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<sharedListeners>**](sharedlisteners-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<add>**

## <a name="syntax"></a>構文  
  
```xml  
<add name="name"
  type="TraceListenerClassName, Version, Culture, PublicKeyToken"  
  initializeData="data"
  traceOutputOptions = "None"
/>  
```
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|`name`|必須の属性です。<br /><br /> 共有リスナーをコレクションに追加するために使用されるリスナーの名前を指定し `Listeners` ます。|  
|`type`|必須の属性です。<br /><br /> リスナーの種類を指定します。 [「完全修飾型名の指定](../../../reflection-and-codedom/specifying-fully-qualified-type-names.md)」で指定した要件を満たす文字列を使用する必要があります。|  
|`initializeData`|省略可能な属性です。<br /><br /> 指定したクラスのコンストラクターに渡される文字列。|  
|`traceOutputOptions`|省略可能な属性です。<br/><br/><xref:System.Diagnostics.TraceOptions>トレース出力に書き込まれるデータを示す1つ以上の列挙メンバーの文字列形式。 複数の項目は、コンマで区切られます。 既定値は "None" です。|

### <a name="child-elements"></a>子要素  
  
|要素|Description|  
|-------------|-----------------|  
|[\<filter>](filter-element-for-add-for-sharedlisteners.md)|`sharedListeners` コレクションのリスナーにフィルターを追加します。|  
  
### <a name="parent-elements"></a>親要素  
  
|要素|Description|  
|-------------|-----------------|  
|`configuration`|共通言語ランタイムおよび .NET Framework アプリケーションで使用されるすべての構成ファイルのルート要素です。|  
|`system.diagnostics`|メッセージを収集、格納、およびルーティングするトレース リスナーとトレース スイッチを設定するレベルを指定します。|  
|`sharedListeners`|任意のソースまたはトレース要素が参照できるリスナーのコレクション。|  
  
## <a name="remarks"></a>解説  
 .NET Framework に付属しているリスナークラスは、クラスから派生し <xref:System.Diagnostics.TraceListener> ます。 属性の値 `name` は、 `Listeners` トレースまたはトレースソースのコレクションに共有リスナーを追加するために使用されます。 属性の値は、 `initializeData` 作成するリスナーの種類によって異なります。 すべてのトレースリスナーでを指定する必要はありません `initializeData` 。  
  
> [!NOTE]
> 属性を使用すると、 `initializeData` "initializeData" 属性が宣言されていないことを示すコンパイラの警告が表示されることがあります。 この警告は、属性を認識しない抽象基本クラスに対して構成設定が検証されるために発生し <xref:System.Diagnostics.TraceListener> `initializeData` ます。 通常、パラメーターを受け取るコンストラクターを持つトレースリスナーの実装では、この警告を無視できます。  
  
 次の表に、.NET Framework に含まれているトレースリスナーとその属性の値を示し `initializeData` ます。  
  
|トレースリスナークラス|initializeData 属性値|  
|--------------------------|------------------------------------|  
|<xref:System.Diagnostics.ConsoleTraceListener>|`useErrorStream`コンストラクターの値 <xref:System.Diagnostics.ConsoleTraceListener.%23ctor%2A> 。  `initializeData`トレース出力およびデバッグ出力を標準エラーストリームに書き込むには、属性を "" に設定します `true` 。 `false` 標準出力ストリームに書き込むには、"" に設定します。|  
|<xref:System.Diagnostics.DelimitedListTraceListener>|<xref:System.Diagnostics.DelimitedListTraceListener> が出力を書き込むファイルの名前。|  
|<xref:System.Diagnostics.EventLogTraceListener?displayProperty=nameWithType>|既存のイベント ログ ソースの名前。|  
|<xref:System.Diagnostics.EventSchemaTraceListener?displayProperty=nameWithType>|が書き込み先となるファイルの名前 <xref:System.Diagnostics.EventSchemaTraceListener> 。|  
|<xref:System.Diagnostics.TextWriterTraceListener?displayProperty=nameWithType>|が書き込み先となるファイルの名前 <xref:System.Diagnostics.TextWriterTraceListener> 。|  
|<xref:System.Diagnostics.XmlWriterTraceListener>|が書き込み先となるファイルの名前 <xref:System.Diagnostics.XmlWriterTraceListener> 。|  
  
## <a name="configuration-file"></a>構成ファイル  
 この要素は、コンピューターの構成ファイル (machine.config) とアプリケーション構成ファイルで使用できます。  
  
## <a name="example"></a>例  
 次の例は、要素を使用してをコレクションに追加する方法を示して `<add>` <xref:System.Diagnostics.TextWriterTraceListener> `textListener` `sharedListeners` います。   `textListener`は、トレースソースのコレクションに名前によって追加され `Listeners` `TraceSourceApp` ます。 リスナーは、 `textListener` トレース出力をファイル myListener .log に書き込みます。  
  
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
