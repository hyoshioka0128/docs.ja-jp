---
title: <add>のの <listeners> 要素<trace>
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.diagnostics/trace/listeners/add
helpviewer_keywords:
- initializeData attribute
- <add> element for <listeners>
- add element for <listeners>
ms.assetid: 81e804a3-ef11-4d39-bbde-bfa012c179e2
ms.openlocfilehash: c64673908dc9afe67d97c08f93e5b9d9533bd34d
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "79153673"
---
# <a name="add-element-for-listeners-for-trace"></a>\<add>のの \<listeners> 要素\<trace>
リスナーを**リスナー**コレクションに追加します。  

[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.diagnostics>**](system-diagnostics-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<trace>**](trace-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<listeners>**](listeners-element-for-trace.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<add>**

## <a name="syntax"></a>構文  
  
```xml  
<add name="name"
     type="trace listener class name, Version, Culture, PublicKeyToken"  
     initializeData="data"/>  
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|**type**|必須の属性です。<br /><br /> リスナーの種類を指定します。 [「完全修飾型名の指定](../../../reflection-and-codedom/specifying-fully-qualified-type-names.md)」で指定した要件を満たす文字列を使用する必要があります。|  
|**initializeData**|省略可能な属性です。<br /><br /> 指定したクラスのコンストラクターに渡される文字列。|  
|**name**|省略可能な属性です。<br /><br /> リスナーの名前を指定します。|  
  
### <a name="child-elements"></a>子要素  
  
|要素|Description|  
|-------------|-----------------|  
|[\<filter>](filter-element-for-add-for-listeners-for-trace.md)|トレースのコレクションのリスナーにフィルターを追加し `Listeners` ます。|  
  
### <a name="parent-elements"></a>親要素  
  
|要素|Description|  
|-------------|-----------------|  
|`configuration`|共通言語ランタイムおよび .NET Framework アプリケーションで使用されるすべての構成ファイルのルート要素です。|  
|`listeners`|メッセージを収集、格納、およびルーティングするリスナーを指定します。 リスナーは、適切なターゲットにトレース出力を送信します。|  
|`system.diagnostics`|ASP.NET 構成セクションのルート要素を指定します。|  
|`trace`|トレース メッセージを収集、格納、およびルーティングするリスナーを保持します。|  
  
## <a name="remarks"></a>解説  
 <xref:System.Diagnostics.Debug>クラスと <xref:System.Diagnostics.Trace> クラスは、同じ**Listeners**コレクションを共有します。 これらのクラスのいずれかのコレクションにリスナーオブジェクトを追加すると、他のクラスは同じリスナーを使用します。 リスナークラスはから派生し <xref:System.Diagnostics.TraceListener> ます。  
  
 トレースリスナーの属性を指定しない場合 `name` 、 <xref:System.Diagnostics.TraceListener.Name%2A> トレースリスナーのは既定で空の文字列 ("") になります。 アプリケーションにリスナーが1つしかない場合は、名前を指定せずにリスナーを追加し、名前に空の文字列を指定することで削除できます。 ただし、アプリケーションに複数のリスナーがある場合は、各トレースリスナーに一意の名前を指定する必要があります。これにより、コレクションとコレクション内の個々のトレースリスナーを識別して管理でき <xref:System.Diagnostics.Debug.Listeners%2A> <xref:System.Diagnostics.Trace.Listeners%2A> ます。  
  
> [!NOTE]
> 同じ種類の複数のトレースリスナーを同じ名前で追加すると、その型と名前のトレースリスナーは1つだけになり、コレクションに追加され `Listeners` ます。 ただし、プログラムを使用して複数の同じリスナーをコレクションに追加することはでき `Listeners` ます。  
  
 **Initializedata**属性の値は、作成するリスナーの種類によって異なります。 すべてのトレースリスナーで**Initializedata**を指定する必要はありません。  
  
> [!NOTE]
> 属性を使用すると、 `initializeData` "initializeData" 属性が宣言されていないことを示すコンパイラの警告が表示されることがあります。 この警告は、属性を認識しない抽象基本クラスに対して構成設定が検証されるために発生し <xref:System.Diagnostics.TraceListener> `initializeData` ます。 通常、パラメーターを受け取るコンストラクターを持つトレースリスナーの実装では、この警告を無視できます。  
  
 次の表に、.NET Framework に含まれるトレースリスナーと、 **Initializedata**属性の値について説明します。  
  
|トレースリスナークラス|initializeData 属性値|  
|--------------------------|------------------------------------|  
|<xref:System.Diagnostics.ConsoleTraceListener?displayProperty=nameWithType>|`useErrorStream`コンストラクターの値 <xref:System.Diagnostics.ConsoleTraceListener.%23ctor%2A> 。  属性を `initializeData` "" に設定し、 `true` トレース出力とデバッグ出力をに設定し <xref:System.Console.Error%2A?displayProperty=nameWithType> ます。書き込み先となる " `false` " <xref:System.Console.Out%2A?displayProperty=nameWithType> 。|  
|<xref:System.Diagnostics.DelimitedListTraceListener?displayProperty=nameWithType>|<xref:System.Diagnostics.DelimitedListTraceListener> が出力を書き込むファイルの名前。|  
|<xref:System.Diagnostics.EventLogTraceListener?displayProperty=nameWithType>|既存のイベントログソースの名前。|  
|<xref:System.Diagnostics.EventSchemaTraceListener?displayProperty=nameWithType>|が書き込み先となるファイルの名前 <xref:System.Diagnostics.EventSchemaTraceListener> 。|  
|<xref:System.Diagnostics.TextWriterTraceListener?displayProperty=nameWithType>|が書き込み先となるファイルの名前 <xref:System.Diagnostics.TextWriterTraceListener> 。|  
|<xref:System.Diagnostics.XmlWriterTraceListener?displayProperty=nameWithType>|が書き込み先となるファイルの名前 <xref:System.Diagnostics.XmlWriterTraceListener> 。|  
  
## <a name="example"></a>例  
 次の例は、要素を使用して **\<add>** リスナー `MyListener` と `MyEventListener` **リスナー**コレクションに追加する方法を示しています。 `MyListener`という名前のファイルを作成し、その `MyListener.log` 出力をファイルに書き込みます。 `MyEventListener`イベントログにエントリを作成します。  
  
```xml  
<configuration>  
   <system.diagnostics>  
      <trace autoflush="true" indentsize="0">  
         <listeners>  
            <add name="myListener" type="System.Diagnostics.TextWriterTraceListener, system, version=1.0.3300.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" initializeData="c:\myListener.log" />  
            <add name="MyEventListener"  
                 type="System.Diagnostics.EventLogTraceListener, system, version=1.0.3300.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"                 initializeData="MyConfigEventLog"/>  
            <add name="configConsoleListener"  
                 type="System.Diagnostics.ConsoleTraceListener, system, version=1.0.3300.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"/>  
         </listeners>  
      </trace>  
   </system.diagnostics>  
</configuration>  
```  
  
## <a name="see-also"></a>関連項目

- <xref:System.Diagnostics.Trace>
- <xref:System.Diagnostics.Debug>
- <xref:System.Diagnostics.EventLogTraceListener>
- <xref:System.Diagnostics.ConsoleTraceListener>
- <xref:System.Diagnostics.TextWriterTraceListener>
- [トレースおよびデバッグ設定のスキーマ](index.md)
- [トレース リスナー](../../../debug-trace-profile/trace-listeners.md)
