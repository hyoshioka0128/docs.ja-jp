---
title: <filters> の <routing>
ms.date: 03/30/2017
ms.assetid: 7993cf90-9afd-4c3c-9608-184d5da1105c
ms.openlocfilehash: c9bc3a2c379e14d8cf687676a3ec40702d150e1e
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "70855235"
---
# <a name="filters-of-routing"></a>\<filters> の \<routing>

<xref:System.ServiceModel.Dispatcher.MessageFilter>受信メッセージを評価するときに使用する Windows Communication Foundation (WCF) の種類を決定する一連のルーティングフィルターを定義するための構成セクションを表します。

[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;[**\<routing>**](routing.md)\
&nbsp;&nbsp;&nbsp;&nbsp;**\<filters>**  
  
## <a name="syntax"></a>構文  
  
```xml  
<system.serviceModel>
  <routing>
    <filters>
      <filter customType="String"
              filterData="String"
              filterType="Action/Address/AddressPrefix/And/Custom/Endpoint/MatchAll/XPath"
              name="String" />
    </filters>
  </routing>
</system.serviceModel>
```  
  
## <a name="attributes-and-elements"></a>属性と要素

以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

なし

### <a name="child-elements"></a>子要素

|     | Description |
| --- | ----------- |
| [**\<filter>**](filter.md) | <xref:System.ServiceModel.Dispatcher.MessageFilter>受信メッセージを評価するときに使用される Windows Communication Foundation (WCF) の種類を決定するルーティングフィルターを格納します。 |

### <a name="parent-elements"></a>親要素

|     | Description |
| --- | ----------- |
| [**\<routing>**](routing.md) | 一連のルーティングフィルターを定義するための構成セクションを表します。これにより、受信メッセージを評価するときに使用される Windows Communication Foundation (WCF) の種類、 <xref:System.ServiceModel.Dispatcher.MessageFilter> およびフィルターが一致したときにメッセージを送信するターゲットエンドポイントを定義するルーティングテーブルが決定されます。 |

## <a name="see-also"></a>関連項目

- <xref:System.ServiceModel.Routing.Configuration.FilterElement?displayProperty=nameWithType>
