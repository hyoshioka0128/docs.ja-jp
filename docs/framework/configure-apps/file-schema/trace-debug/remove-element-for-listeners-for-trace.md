---
title: <remove>のの <listeners> 要素<trace>
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.diagnostics/trace/listeners/remove
helpviewer_keywords:
- remove element
- <remove> element
ms.assetid: 9a5cd1b5-be1a-485f-8f0c-2890ad3ef3e0
ms.openlocfilehash: f06973ec30d5061e4a200d6bf7e68adcf6302018
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "74088845"
---
# <a name="remove-element-for-listeners-for-trace"></a>\<remove>のの \<listeners> 要素\<trace>
**リスナーコレクションから**リスナーを削除します。  

[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.diagnostics>**](system-diagnostics-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<trace>**](trace-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<listeners>**](listeners-element-for-trace.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<remove>**

## <a name="syntax"></a>構文  
  
```xml  
<remove name="listener name" />  
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|**name**|必須の属性です。<br /><br /> **リスナー**コレクションから削除するリスナーの名前。|  
  
### <a name="child-elements"></a>子要素  
 なし。  
  
### <a name="parent-elements"></a>親要素  
  
|要素|Description|  
|-------------|-----------------|  
|`configuration`|共通言語ランタイムおよび .NET Framework アプリケーションで使用されるすべての構成ファイルのルート要素です。|  
|`listeners`|メッセージを収集、格納、およびルーティングするリスナーを指定します。 リスナーは、適切なターゲットにトレース出力を送信します。|  
|`system.diagnostics`|メッセージを収集、格納、およびルーティングするトレース リスナーとトレース スイッチを設定するレベルを指定します。|  
|`trace`|ASP.NET トレース サービスを設定します。|  
  
## <a name="remarks"></a>解説  
  
> [!NOTE]
> コレクションからを削除する <xref:System.Diagnostics.DefaultTraceListener> `Listeners` と、、、、およびの各メソッドの動作が変更され <xref:System.Diagnostics.Debug.Assert%2A?displayProperty=nameWithType> <xref:System.Diagnostics.Trace.Assert%2A?displayProperty=nameWithType> <xref:System.Diagnostics.Debug.Fail%2A?displayProperty=nameWithType> <xref:System.Diagnostics.Trace.Fail%2A?displayProperty=nameWithType> ます。 通常、 `Assert` メソッドまたはメソッドを呼び出すと、 `Fail` メッセージボックスが表示されますが、 <xref:System.Diagnostics.DefaultTraceListener> がコレクションに含まれていない場合は、メッセージボックスは表示されません `Listeners` 。  
  
## <a name="example"></a>例  
 次の例は、トレース**リスナー**コレクションから既定のトレースリスナーを削除する方法を示しています。  
  
```xml  
<configuration>  
   <system.diagnostics>  
      <trace autoflush="true" indentsize="0">  
         <listeners>  
            <remove name="Default" />  
         </listeners>  
      </trace>  
   </system.diagnostics>  
</configuration>  
```  
  
## <a name="see-also"></a>関連項目

- <xref:System.Diagnostics.TraceListener>
- <xref:System.Diagnostics.DefaultTraceListener>
- <xref:System.Diagnostics.TextWriterTraceListener>
- <xref:System.Diagnostics.EventLogTraceListener>
- [トレースおよびデバッグ設定のスキーマ](index.md)
