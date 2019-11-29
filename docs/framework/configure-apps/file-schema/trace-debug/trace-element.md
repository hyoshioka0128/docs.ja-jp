---
title: <trace> 要素
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.diagnostics/trace
- http://schemas.microsoft.com/.NetConfiguration/v2.0#trace
helpviewer_keywords:
- <trace> element
- listeners
- trace element
- trace listener, <trace> element
ms.assetid: 7931c942-63c1-47c3-a045-9d9de3cacdbf
ms.openlocfilehash: 02fd794eb7b7b7f46f7f7bc4e43036cb4a4758ed
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/01/2019
ms.locfileid: "71699184"
---
# <a name="trace-element"></a>トレース > 要素の \<
トレース メッセージを収集、格納、およびルーティングするリスナーを保持します。  
  
[ **\<configuration>** ](../configuration-element.md)  
&nbsp;&nbsp;[ **\<の >** ](system-diagnostics-element.md)  
&nbsp;&nbsp;&nbsp;&nbsp; **\<トレース >**  
  
## <a name="syntax"></a>構文  
  
```xml  
<trace autoflush="true|false"   
       indentsize="indent value"  
       useGlobalLock="true| false"/>  
```  
  
## <a name="attributes-and-elements"></a>属性と要素  
 次のセクションでは、属性、子要素、親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|`autoflush`|省略可能な属性です。<br /><br /> 書き込み操作が行われるたびに、トレースリスナーが出力バッファーを自動的にフラッシュするかどうかを指定します。|  
|`indentsize`|省略可能な属性です。<br /><br /> インデントするスペースの数を指定します。|  
|`useGlobalLock`|省略可能な属性です。<br /><br /> グローバルロックを使用する必要があるかどうかを示します。|  
  
## <a name="autoflush-attribute"></a>autoflush 属性  
  
|値|説明|  
|-----------|-----------------|  
|`false`|では、出力バッファーは自動的にはフラッシュされません。 既定値です。|  
|`true`|出力バッファーを自動的にフラッシュします。|  
  
## <a name="usegloballock-attribute"></a>useGlobalLock 属性  
  
|値|説明|  
|-----------|-----------------|  
|`false`|リスナーがスレッドセーフである場合、はグローバルロックを使用しません。それ以外の場合、はグローバルロックを使用します。|  
|`true`|は、リスナーがスレッドセーフかどうかに関係なく、グローバルロックを使用します。 既定値です。|  
  
### <a name="child-elements"></a>子要素  
  
|要素|説明|  
|-------------|-----------------|  
|[\<listeners>](listeners-element-for-trace.md)|メッセージを収集、格納、およびルーティングするリスナーを指定します。|  
  
### <a name="parent-elements"></a>親要素  
  
|要素|説明|  
|-------------|-----------------|  
|`configuration`|共通言語ランタイムおよび .NET Framework アプリケーションで使用されるすべての構成ファイルのルート要素です。|  
|`system.diagnostics`|メッセージを収集、格納、およびルーティングするトレース リスナーとトレース スイッチを設定するレベルを指定します。|  
  
## <a name="example"></a>例  
 次の例は、`<trace>` 要素を使用して、リスナー `MyListener` を `Listeners` コレクションに追加する方法を示しています。 `MyListener` によって `MyListener.log` という名前のファイルが作成され、出力がファイルに書き込まれます。 `useGlobalLock` 属性は `false`に設定されています。これにより、トレースリスナーがスレッドセーフである場合は、グローバルロックが使用されません。 `autoflush` 属性は `true`に設定されます。これにより、<xref:System.Diagnostics.Trace.Flush%2A?displayProperty=nameWithType> メソッドが呼び出されているかどうかに関係なく、トレースリスナーがファイルに書き込みます。 `indentsize` 属性は 0 (ゼロ) に設定されます。これにより、<xref:System.Diagnostics.Trace.Indent%2A?displayProperty=nameWithType> メソッドが呼び出されたときにリスナーが0個のスペースにインデントを設定します。  
  
```xml  
<configuration>  
   <system.diagnostics>  
      <trace useGlobalLock="false" autoflush="true" indentsize="0">  
         <listeners>  
            <add name="myListener" type="System.Diagnostics.TextWriterTraceListener, system version=1.0.3300.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" initializeData="c:\myListener.log" />  
         </listeners>  
      </trace>  
   </system.diagnostics>  
</configuration>  
```  
  
## <a name="see-also"></a>参照

- <xref:System.Diagnostics.TraceListener>
- <xref:System.Diagnostics.DefaultTraceListener>
- <xref:System.Diagnostics.TextWriterTraceListener>
- <xref:System.Diagnostics.EventLogTraceListener>
- [トレースおよびデバッグ設定のスキーマ](index.md)
