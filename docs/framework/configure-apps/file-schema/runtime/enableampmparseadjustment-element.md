---
title: <EnableAmPmParseAdjustment> 要素
ms.date: 03/30/2017
ms.assetid: fda998a5-f538-4f8b-a18c-ee7f35e16938
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 4bcde1bbb5419de2c363b422c327d55c2ce9eea1
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2019
ms.locfileid: "64607315"
---
# <a name="enableampmparseadjustment-element"></a>\<EnableAmPmParseAdjustment > 要素
日付と時刻の解析メソッドが日、月、1 時間、および AM/PM 指定子を含む日付の文字列を解析する調整済みの一連のルールを使用しているかどうかを判断します。  
  
 \<configuration>  
 \<runtime>  
\<EnableAmPmParseAdjustment>  
  
## <a name="syntax"></a>構文  
  
```xml  
<EnableAmPmParseAdjustment enabled="0"|"1" />  
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|`enabled`|必須の属性です。<br /><br /> 日付と時刻の解析メソッドで、日、月、時、午前/午後のみを含む日付の文字列を解析する調整済みの一連のルールを使用するかどうかを指定します。|  
  
### <a name="enabled-attribute"></a>enabled 属性  
  
|値|説明|  
|-----------|-----------------|  
|0|日付と時刻の解析メソッドを日、月、時、午前/午後のみを含む日付の文字列を解析するため調整済みの規則を使用しないでください。|  
|1|日付と時刻の解析メソッドは、調整済みの規則を使用して、日、月、時、午前/午後のみを含む日付文字列を解析するため。|  
  
### <a name="child-elements"></a>子要素  
 なし。  
  
### <a name="parent-elements"></a>親要素  
  
|要素|説明|  
|-------------|-----------------|  
|`configuration`|共通言語ランタイムおよび .NET Framework アプリケーションで使用されるすべての構成ファイルのルート要素です。|  
|`runtime`|ランタイム初期化オプションに関する情報を含んでいます。|  
  
## <a name="remarks"></a>Remarks  
 `<EnableAmPmParseAdjustment>`要素は、次のメソッドが 1 日と月の後に 1 時間と、AM/PM 指定子 (「10 4/6 AM」) などを含む日付文字列を解析する方法を制御します。  
  
- <xref:System.DateTime.Parse%2A?displayProperty=nameWithType>  
  
- <xref:System.DateTimeOffset.Parse%2A?displayProperty=nameWithType>  
  
- <xref:System.DateTime.TryParse%2A?displayProperty=nameWithType>  
  
- <xref:System.DateTimeOffset.TryParse%2A?displayProperty=nameWithType>  
  
- <xref:System.Convert.ToDateTime%2A?displayProperty=nameWithType>  
  
 その他のパターンが影響を受けません。  
  
 `<EnableAmPmParseAdjustment>`要素も何も起こりません、 <xref:System.DateTime.ParseExact%2A?displayProperty=nameWithType>、 <xref:System.DateTime.TryParseExact%2A?displayProperty=nameWithType>、 <xref:System.DateTimeOffset.ParseExact%2A?displayProperty=nameWithType>、および<xref:System.DateTimeOffset.TryParseExact%2A?displayProperty=nameWithType>メソッド。  
  
> [!IMPORTANT]
>  .NET Core と .NET ネイティブでは、調整済みの午前/午後解析規則は既定で有効にします。  
  
 解析の調整規則が有効でない場合は、文字列の最初の桁は、12 時間時計の時間として解釈され、午前/午後を除く、文字列の残りの部分は無視されます。 日付と時刻の解析メソッドによって返されるは、現在の日付と日付の文字列から抽出された日の時間で構成されます。  
  
 解析の調整規則が有効になっている場合はメソッドの解析、現在の年に属するものとして月と日を解釈し、12 時間制の時間で時間を解釈します。  
  
 次の表の違いを示しています、<xref:System.DateTime>ときの値、<xref:System.DateTime.Parse%28System.String%29?displayProperty=nameWithType>メソッドは、文字列の解析に使用される"「10 4/6 AM」、`<EnableAmPmParseAdjustment>`要素の`enabled`プロパティが「0」または「1」に設定します。 今日の日付が 2017 年 1 月 5 日し、日付が表示されますが、指定したカルチャの"G"書式指定文字列を使用して書式設定された場合と前提としています。  
  
|カルチャ名|有効になっている =「0」|enabled="1"|  
|------------------|------------------|------------------|  
|en-US|2017 年 1 月 5 4時 00分: 00 AM|2017 年 4 月 10 6時 00分: 00 AM|  
|en-GB|5/1/2017 6:00:00|10/4/2017 6:00:00|  
  
## <a name="see-also"></a>関連項目

- [\<runtime> 要素](../../../../../docs/framework/configure-apps/file-schema/runtime/runtime-element.md)
- [\<configuration> 要素](../../../../../docs/framework/configure-apps/file-schema/configuration-element.md)
