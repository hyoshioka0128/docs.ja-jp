---
title: <clear>のの <listeners> 要素<trace>
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.diagnostics/trace/listeners/clear
helpviewer_keywords:
- clear element for <listeners> for <trace>
- <clear> element for <listeners> for <trace>
ms.assetid: b44732a8-271f-4a06-ba9e-fe3298d6f192
ms.openlocfilehash: 905dad8274fede80f4809ff3c7a014049f9df450
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "79153543"
---
# <a name="clear-element-for-listeners-for-trace"></a>\<clear>のの \<listeners> 要素\<trace>
トレースの `Listeners` コレクションを削除します。  

[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.diagnostics>**](system-diagnostics-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<trace>**](trace-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<listeners>**](listeners-element-for-trace.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<clear>**

## <a name="syntax"></a>構文  
  
```xml  
<clear/>  
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
 なし。  
  
### <a name="child-elements"></a>子要素  
 [なし] :  
  
### <a name="parent-elements"></a>親要素  
  
|要素|説明|  
|-------------|-----------------|  
|`configuration`|共通言語ランタイムおよび .NET Framework アプリケーションで使用されるすべての構成ファイルのルート要素です。|  
|`system.diagnostics`|メッセージを収集、格納、およびルーティングするトレース リスナーとトレース スイッチを設定するレベルを指定します。|  
|`trace`|トレース メッセージを収集、格納、およびルーティングするリスナーを保持します。|  
|`listeners`|メッセージを収集、格納、およびルーティングするリスナーを格納します。 リスナーは、適切なターゲットにトレース出力を送信します。|  
  
## <a name="remarks"></a>解説  
 要素は、 `<clear>` トレースのコレクションからすべてのリスナーを削除し `Listeners` ます。 要素を使用 `<clear>` して、 `<add>` コレクション内に他のアクティブなリスナーが存在しないことを特定することができます。  
  
 コレクションは、 `Listeners` <xref:System.Diagnostics.TraceListenerCollection.Clear%2A> プロパティ () でメソッドを呼び出すことで、プログラムによって消去でき <xref:System.Diagnostics.Trace.Listeners%2A?displayProperty=nameWithType> `System.Diagnostics.Trace.Listeners.Clear()` ます。  
  
 この要素は、コンピューターの構成ファイル (machine.config) とアプリケーション構成ファイルで使用できます。  
  
> [!NOTE]
> 要素は、、、 `<clear>` <xref:System.Diagnostics.DefaultTraceListener> `Listeners` 、およびの各メソッドの動作を変更して、をコレクションから削除し <xref:System.Diagnostics.Debug.Assert%2A?displayProperty=nameWithType> <xref:System.Diagnostics.Trace.Assert%2A?displayProperty=nameWithType> <xref:System.Diagnostics.Debug.Fail%2A?displayProperty=nameWithType> <xref:System.Diagnostics.Trace.Fail%2A?displayProperty=nameWithType> ます。 通常、 `Assert` メソッドまたはメソッドを呼び出すと `Fail` 、メッセージボックスが表示されます。 ただし、 <xref:System.Diagnostics.DefaultTraceListener> がコレクションに含まれていない場合、メッセージボックスは表示されません `Listeners` 。  
  
## <a name="example"></a>例  
 次の例では、要素を使用し `<clear>` て、 `<add>` `console` `Listeners` トレースのコレクションにリスナーを追加する前に、要素を使用する方法を示します。  
  
```xml  
<configuration>  
  <system.diagnostics>  
    <trace autoflush="false" indentsize="4">  
      <listeners>  
        <clear/>  
        <add name="console"
          type="System.Diagnostics.ConsoleTraceListener" >  
          <filter type="System.Diagnostics.EventTypeFilter"
            initializeData="Error" />  
        </add>  
      </listeners>  
    </trace>  
  </system.diagnostics>  
</configuration>
```  
  
## <a name="see-also"></a>関連項目

- <xref:System.Diagnostics.Trace.Listeners%2A>
- <xref:System.Diagnostics.Trace>
- <xref:System.Diagnostics.Debug>
- <xref:System.Diagnostics.TraceSource>
- [トレースおよびデバッグ設定のスキーマ](index.md)
- [\<remove>](remove-element-for-listeners-for-trace.md)
- [トレース リスナー](../../../debug-trace-profile/trace-listeners.md)
