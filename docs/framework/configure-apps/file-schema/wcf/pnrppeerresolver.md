---
title: <pnrpPeerResolver>
ms.date: 03/30/2017
ms.assetid: c1b34f3b-68e5-4911-a367-de49fb61dbc6
ms.openlocfilehash: d3e88d7f2dd991091d3d7abdc715e125ddc9ac56
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "73738777"
---
# \<pnrpPeerResolver>
リゾルバーとして PNRP (Peer Name Resolution Protocol) リゾルバーを使用することを指定します。 PNRP は既定のリゾルバーであるため、この要素は省略可能です。  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<bindings>**](bindings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<customBinding>**](custombinding.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<binding>**\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<pnrpResolver>**  
  
## <a name="syntax"></a>構文  
  
```xml  
<pnrpResolver resolverType="String" />
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|resolverType|使用されるリゾルバーを指定する文字列。 この属性は省略できます。 設定されていない場合、または空の文字列に設定されている場合は、PNRP が使用されます。|  
  
### <a name="child-elements"></a>子要素  
 なし  
  
### <a name="parent-elements"></a>親要素  
  
|要素|Description|  
|-------------|-----------------|  
|[\<binding>](bindings.md)|カスタム バインドのすべてのバインド機能を定義します。|  
  
## <a name="example"></a>例  
  
```xml  
<pnrpResolver resolverType="String" />
```  
  
## <a name="see-also"></a>関連項目

- <xref:System.ServiceModel.Configuration.PnrpPeerResolverElement>
- <xref:System.ServiceModel.Channels.PnrpPeerResolverBindingElement>
- <xref:System.ServiceModel.Channels.CustomBinding>
- [バインド](../../../wcf/bindings.md)
- [バインディングの拡張](../../../wcf/extending/extending-bindings.md)
- [カスタム バインディング](../../../wcf/extending/custom-bindings.md)
- [\<customBinding>](custombinding.md)
- [ピア リゾルバー](../../../wcf/feature-details/peer-resolvers.md)
