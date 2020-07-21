---
title: <security> の <netNamedPipeBinding>
ms.date: 03/30/2017
ms.assetid: bb3cb022-637e-49fd-92e8-6766038affa7
ms.openlocfilehash: 31ea31ce6880a770c966350cd931e487396c4d63
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "73736442"
---
# <a name="security-of-netnamedpipebinding"></a>\<security> の \<netNamedPipeBinding>
バインディングのセキュリティ設定を定義します。  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<bindings>**](bindings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<netNamedPipeBinding>**](netnamedpipebinding.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<binding>**\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<security>**  
  
## <a name="syntax"></a>構文  
  
```xml  
<netNamedPipeBinding>
  <binding>
    <security mode="None/Transport">
      <transport protectionLevel="None/Sign/EncryptAndSign" />
    </security>
  </binding>
</netNamedPipeBinding>
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|mode|このバインディングに適用されるセキュリティの種類を指定します。 有効な値は次のとおりです。<br /><br /> -None: セキュリティを無効にします。<br />-Transport: セキュリティは、基になるトランスポートベースのセキュリティを使用して提供されます。 このモードでは保護レベルを制御することができます。<br />-既定値は Transport です。 この属性は <xref:System.ServiceModel.NetNamedPipeSecurityMode> 型です。|  
  
### <a name="child-elements"></a>子要素  
  
|要素|Description|  
|-------------|-----------------|  
|transport|トランスポートのセキュリティ設定を定義します。 この要素は <xref:System.ServiceModel.Configuration.NamedPipeTransportSecurityElement> 型です。|  
  
### <a name="parent-elements"></a>親要素  
  
|要素|Description|  
|-------------|-----------------|  
|binding|のバインディング要素 [\<netNamedPipeBinding>](netnamedpipebinding.md) 。|  
  
## <a name="see-also"></a>関連項目

- <xref:System.ServiceModel.NetNamedPipeSecurity>
- <xref:System.ServiceModel.NetNamedPipeBinding.Security%2A>
- <xref:System.ServiceModel.Configuration.NetNamedPipeBindingElement.Security%2A>
- <xref:System.ServiceModel.Configuration.NetNamedPipeSecurityElement>
- [サービスおよびクライアントのセキュリティ保護](../../../wcf/feature-details/securing-services-and-clients.md)
- [資格情報の種類の選択](../../../wcf/feature-details/selecting-a-credential-type.md)
- [バインド](../../../wcf/bindings.md)
- [システムが提供するバインディングの構成](../../../wcf/feature-details/configuring-system-provided-bindings.md)
- [サービスとクライアントを構成するためのバインディングの使用](../../../wcf/using-bindings-to-configure-services-and-clients.md)
- [\<binding>](bindings.md)
