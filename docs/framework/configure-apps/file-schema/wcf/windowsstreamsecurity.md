---
title: <windowsStreamSecurity>
ms.date: 03/30/2017
ms.assetid: 926bea29-90c7-4a26-9cf0-fb4aa44f6f70
ms.openlocfilehash: dab8505a9ddb348a6f7fe16ae9acb3a0119a8b06
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "73735887"
---
# \<windowsStreamSecurity>
カスタム バインディングの Windows ストリーム セキュリティ設定を指定します。  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<bindings>**](bindings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<customBinding>**](custombinding.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<binding>**\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<windowsStreamSecurity>**  
  
## <a name="syntax"></a>構文  
  
```xml  
<windowsStreamSecurity protectionLevel="None/Sign/EncryptAndSign" />
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|protectionLevel|メッセージ レベルのセキュリティを定義します。 メッセージに署名を付けることで、メッセージの転送中に第三者によって改ざんされるリスクが軽減されます。 暗号化によって、トランスポート中にデータ レベルのプライバシーが提供されます。 有効な値は次のとおりです。<br /><br /> -None: 保護がありません。<br />-Sign: メッセージは署名されています。<br />-EncryptAndSign: メッセージは署名され、暗号化されます。<br /><br /> 既定値は EncryptAndSign です。<br /><br /> この属性は <xref:System.Net.Security.ProtectionLevel> 型です。|  
  
### <a name="child-elements"></a>子要素  
 なし  
  
### <a name="parent-elements"></a>親要素  
  
|要素|Description|  
|-------------|-----------------|  
|[\<binding>](bindings.md)|カスタム バインドのすべてのバインド機能を定義します。|  
  
## <a name="remarks"></a>解説  
 TCP などのストリーム指向プロトコルおよび名前付きパイプを使用するトランスポートは、ストリーム ベースのトランスポート アップグレードをサポートします。 特に、WCF にはセキュリティ アップグレードが用意されています。 このトランスポートセキュリティの構成は、この構成要素およびによってカプセル化され、これを [\<sslStreamSecurity>](sslstreamsecurity.md) 構成してカスタムバインドに追加することができます。  
  
## <a name="see-also"></a>関連項目

- <xref:System.ServiceModel.Channels.CustomBinding>
- <xref:System.ServiceModel.Configuration.WindowsStreamSecurityElement>
- <xref:System.ServiceModel.Channels.WindowsStreamSecurityBindingElement>
- [バインド](../../../wcf/bindings.md)
- [バインディングの拡張](../../../wcf/extending/extending-bindings.md)
- [カスタム バインディング](../../../wcf/extending/custom-bindings.md)
- [\<customBinding>](custombinding.md)
