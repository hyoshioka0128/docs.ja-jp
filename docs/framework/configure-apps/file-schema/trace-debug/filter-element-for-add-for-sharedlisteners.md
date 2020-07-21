---
title: <filter>のの <add> 要素<sharedListeners>
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.diagnostics/sharedListeners/add/filter
helpviewer_keywords:
- filter element for <add> for <sharedListeners>
- initializeData attribute
- <filter> element for <add> for <sharedListeners>
- filters, trace listeners
- trace listeners, filters
ms.assetid: 7d4e7faa-2e4e-4379-ac76-f6cd7f2f8fac
ms.openlocfilehash: 6fb52cdfa5792ab6059b60d8dbb91c107cd666ca
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "79153454"
---
# <a name="filter-element-for-add-for-sharedlisteners"></a>\<filter>のの \<add> 要素\<sharedListeners>
`sharedListeners` コレクションのリスナーにフィルターを追加します。  

[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.diagnostics>**](system-diagnostics-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<sharedListeners>**](sharedlisteners-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<add>**](add-element-for-sharedlisteners.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<filter>**

## <a name="syntax"></a>構文  
  
```xml  
<filter type="System.Diagnostics.EventTypeFilter"
  initializeData="Warning" />  
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|**type**|必須の属性です。<br /><br /> フィルターの種類を指定します。 型の完全な名前 (プロパティの形式) のみを使用することも、 <xref:System.Type.FullName%2A?displayProperty=nameWithType> アセンブリ情報を含む完全修飾型名 (プロパティの形式) を使用することもでき <xref:System.Type.AssemblyQualifiedName%2A?displayProperty=nameWithType> ます。 完全修飾型名の作成の詳細については、「[完全修飾型名の指定](../../../reflection-and-codedom/specifying-fully-qualified-type-names.md)」を参照してください。|  
|**initializeData**|省略可能な属性です。<br /><br /> 指定したクラスのコンストラクターに渡される文字列。|  
  
### <a name="child-elements"></a>子要素  
 なし。  
  
### <a name="parent-elements"></a>親要素  
  
|要素|Description|  
|-------------|-----------------|  
|`configuration`|共通言語ランタイムおよび .NET Framework アプリケーションで使用されるすべての構成ファイルのルート要素です。|  
|`system.diagnostics`|メッセージを収集、格納、およびルーティングするトレース リスナーとトレース スイッチを設定するレベルを指定します。|  
|`sharedListeners`|任意のソースまたはトレース要素が参照できるリスナーのコレクション。|  
|`add`|リスナーを**sharedListeners**コレクションに追加します。|  
  
## <a name="remarks"></a>解説  
 リスナーが要素の要素で定義されている場合 `<add>` `<sharedListeners>` 、そのリスナーのフィルターは、要素の子である要素で定義されている必要があり `<filter>` `<add>` ます。  
  
 この要素は、コンピューターの構成ファイル (machine.config) とアプリケーション構成ファイルで使用できます。  
  
## <a name="example"></a>例  
 次の例は、要素を使用して、 `<filter>` コレクション内のトレースリスナーにフィルターを追加する方法を示して `console` `sharedListeners` います。  
  
```xml  
<configuration>  
  <system.diagnostics>  
    <sources>  
      <source name="myTraceSource" >  
        <listeners>  
          <add name="console" />  
          <remove name="Default" />  
        </listeners>  
      </source>  
    </sources>  
    <sharedListeners>  
      <add name="console"
        type="System.Diagnostics.ConsoleTraceListener" >  
        <filter type="System.Diagnostics.EventTypeFilter"
          initializeData="Error" />  
      </add>  
    </sharedListeners>  
  </system.diagnostics>  
</configuration>  
```  
  
## <a name="see-also"></a>関連項目

- <xref:System.Diagnostics.TraceFilter>
- <xref:System.Diagnostics.TraceListener>
- <xref:System.Diagnostics.TraceSource>
- [トレースおよびデバッグ設定のスキーマ](index.md)
