---
title: <custom>
ms.date: 03/30/2017
ms.assetid: a6f65a00-bd1a-4d4a-955a-fe009ec02ab8
ms.openlocfilehash: 598b341e8b09acd11ba215e6add3adf9e44b2b81
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "70400460"
---
# \<custom>
ユーザー設定のピア リゾルバー サービスの設定を指定します。  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<bindings>**](bindings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<netPeerTcpBinding>**](netpeertcpbinding.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<binding>**\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<resolver>**](resolver.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<custom>**  
  
## <a name="syntax"></a>構文  
  
```xml  
<custom address="Uri"
        resolverType="String">
  <headers/>
  <identity/>
</custom>
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|`address`|カスタム ピア リゾルバー サービスをホストするピア ノードのエンドポイント アドレスを指定する URI。|  
|`resolverType`|カスタム ピア リゾルバー サービスの種類を指定する文字列。|  
  
### <a name="child-elements"></a>子要素  
  
|要素|Description|  
|-------------|-----------------|  
|[\<identity>](identity.md)|この要素を使用して構成されたカスタム ピア リゾルバーの ID を指定します。 この要素は <xref:System.ServiceModel.Configuration.IdentityElement> 型です。|  
|[\<headers>](headers-element.md)|カスタム ピア リゾルバーによって処理される SOAP メッセージに使用するアドレス ヘッダーのコレクション。|  
  
### <a name="parent-elements"></a>親要素  
  
|要素|Description|  
|-------------|-----------------|  
|[\<resolver>](resolver.md)|ピア メッシュ ID を解決してメッシュに参加する複数ノードを表すピア ノード アドレスのセットを取得するために使用されるピア リゾルバー。|  
  
## <a name="remarks"></a>解説  
 この要素は、サービスをホストするピアのエンドポイント アドレスや特定のバインディング設定など、カスタム ピア リゾルバー サービスの基本設定を定義します。 カスタム競合回避モジュールの作成の詳細については、「 [PeerChannel アプリケーションへのカスタム競合回避モジュールの追加](https://docs.microsoft.com/previous-versions/ms730105(v=vs.90))」を参照してください。  
  
## <a name="see-also"></a>関連項目

- <xref:System.ServiceModel.PeerResolvers.CustomPeerResolverService>
- <xref:System.ServiceModel.PeerResolvers.PeerCustomResolverSettings>
- <xref:System.ServiceModel.Configuration.PeerResolverElement.Custom%2A>
- <xref:System.ServiceModel.Configuration.PeerCustomResolverElement>
- [ピア リゾルバー](../../../wcf/feature-details/peer-resolvers.md)
- [PeerChannel アプリケーションへのカスタム リゾルバーの追加](https://docs.microsoft.com/previous-versions/ms730105(v=vs.90))
