---
title: <trace> の <listeners> の <clear> 要素
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.diagnostics/trace/listeners/clear
helpviewer_keywords:
- clear element for <listeners> for <trace>
- <clear> element for <listeners> for <trace>
ms.assetid: b44732a8-271f-4a06-ba9e-fe3298d6f192
ms.openlocfilehash: 0361580724351f8f42d058d5e20354e3335bac2f
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/01/2019
ms.locfileid: "71699378"
---
# <a name="clear-element-for-listeners-for-trace"></a>\<trace @no__t の \< リスナー > の > 要素
トレースの `Listeners` コレクションを削除します。  
  
[ **\<configuration>** ](../configuration-element.md)  
&nbsp; @ no__t-1[ **\<system. diagnostics >** ](system-diagnostics-element.md)  
&nbsp; @ no__t-1 @ no__t @ no__t-3[ **\<trace >** ](trace-element.md)  
&nbsp; @ no__t-1 @ no__t @ no__t @ no__t-5[ **\<listeners >** します。](listeners-element-for-trace.md)  
&nbsp; @ no__t-1 @ no__t @ no__t @ no__t-5 @ no__t-6 @ no__t-7 **\<clear > を削除**します。  
  
## <a name="syntax"></a>構文  
  
```xml  
<clear/>  
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
 [なし] :  
  
### <a name="child-elements"></a>子要素  
 なし。  
  
### <a name="parent-elements"></a>親要素  
  
|要素|説明|  
|-------------|-----------------|  
|`configuration`|共通言語ランタイムおよび .NET Framework アプリケーションで使用されるすべての構成ファイルのルート要素です。|  
|`system.diagnostics`|メッセージを収集、格納、およびルーティングするトレース リスナーとトレース スイッチを設定するレベルを指定します。|  
|`trace`|トレース メッセージを収集、格納、およびルーティングするリスナーを保持します。|  
|`listeners`|メッセージを収集、格納、およびルーティングするリスナーを格納します。 リスナーは、適切なターゲットにトレース出力を送信します。|  
  
## <a name="remarks"></a>コメント  
 @No__t-0 要素は、トレースの `Listeners` コレクションからすべてのリスナーを削除します。 @No__t-1 要素を使用して、コレクション内に他のアクティブなリスナーが存在しないことを特定するには、`<clear>` 要素を使用します。  
  
 @No__t-2 プロパティの <xref:System.Diagnostics.TraceListenerCollection.Clear%2A> メソッド (`System.Diagnostics.Trace.Listeners.Clear()`) を呼び出すことで、プログラムによって @no__t 0 のコレクションを消去できます。  
  
 この要素は、コンピューターの構成ファイル (machine.config) とアプリケーション構成ファイルで使用できます。  
  
> [!NOTE]
> @No__t-0 要素は、`Listeners` コレクションから <xref:System.Diagnostics.DefaultTraceListener> を削除し、<xref:System.Diagnostics.Debug.Assert%2A?displayProperty=nameWithType>、@no__t 4、<xref:System.Diagnostics.Debug.Fail%2A?displayProperty=nameWithType>、および @no__t 6 の各メソッドの動作を変更します。 通常、`Assert` または `Fail` メソッドを呼び出すと、メッセージボックスが表示されます。 ただし、<xref:System.Diagnostics.DefaultTraceListener> が `Listeners` コレクションに含まれていない場合、メッセージボックスは表示されません。  
  
## <a name="example"></a>例  
 次の例では、`<clear>` の要素を使用して、`<add>` の要素を使用してリスナー `console` をトレースの `Listeners` コレクションに追加する方法を示します。  
  
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
