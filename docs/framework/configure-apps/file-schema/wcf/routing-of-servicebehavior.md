---
title: <routing> の <serviceBehavior>
ms.date: 03/30/2017
ms.assetid: d8f9c844-4629-4a45-9599-856dc8f01794
ms.openlocfilehash: 0998f4fc61de7099879ba6e122eed1e64588baec
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "70397730"
---
# <a name="routing-of-servicebehavior"></a>\<routing> の \<serviceBehavior>
ルーティング構成の動的な変更を可能にするルーティング サービスへの実行時アクセスを提供します。  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<behaviors>**](behaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<serviceBehaviors>**](servicebehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<behavior>**](behavior-of-servicebehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<routing>**  
  
## <a name="syntax"></a>構文  
  
```xml  
<behaviors>
  <serviceBehaviors>
    <behavior name="String">
      <routing filterTable="String"
               routeOnHeadersOnly="Boolean"
               SoapProcessingEnabled="Boolean" />
    </behavior>
  </serviceBehaviors>
</behaviors>
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|filterTable|ルーティング サービスによって評価されるフィルターを含むルーティング テーブルの名前を指定する文字列。 この値は `name` 、セクション内の要素の属性と一致している必要があり [\<filterTable>](filtertable.md) [\<filterTables>](filtertables.md) ます。|  
|routeOnHeaderOnly|フィルターがメッセージの本文とヘッダーの両方を調べるか、ヘッダーのみを調べるかを指定するブール値。 既定値は、`true` です。|  
|soapProcessingEnabled|SOAP 処理を実行するかどうかを指定するブール値。|  
  
### <a name="child-elements"></a>子要素  
 なし。  
  
### <a name="parent-elements"></a>親要素  
  
|要素|Description|  
|-------------|-----------------|  
|[\<behavior>](behavior-of-endpointbehaviors.md)|動作の要素を指定します。|  
  
## <a name="remarks"></a>解説  
 サービスの動作構成に追加すると、この構成要素により、サービスのルーティングが有効になります。 この要素には、サービスで使用される実際のルーティング テーブルを指定できます。  
  
 この構成セクションを使用すると、配置パターンの変更時にルーティング設定を変更できます。 実行時には、新しいルーティング設定を使用した独自のルーティング拡張を登録できます。ルーティング サービスは (開始時に適用されていた規則に関係なく) 更新済みの構成情報を使用して新たなメッセージとセッションにサービスを提供します。ただし、インフライトのメッセージやセッションには以前の規則が適用されます。  このようにして、実行時において、セッション セーフでリサイクルの程度を抑えた状態でのルーティング サービスの再構成が可能となります。  
