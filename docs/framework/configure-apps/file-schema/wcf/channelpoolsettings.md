---
title: <channelPoolSettings>
ms.date: 03/30/2017
ms.assetid: 4755f3d3-4213-4c68-ae7f-45b67d744459
ms.openlocfilehash: 26537980a6be5c0fe12661d93a6ba5fe862ceb4e
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "70398157"
---
# \<channelPoolSettings>
カスタム バインディングのチャネル プール設定を指定します。  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<bindings>**](bindings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<customBinding>**](custombinding.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<binding>**\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<oneWay>**](oneway.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<channelPoolSettings>**  
  
## <a name="syntax"></a>構文  
  
```xml  
<channelPoolSettings idleTimeout="TimeSpan"
                     leaseTimeout="TimeSpan"
                     maxOutboundConnectionsPerEndpoint="Integer" />
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|`idleTimeout`|プール内のチャネルの接続が切断されるまでの最大アイドル時間を指定する正の <xref:System.TimeSpan>。 既定値は 00:02:00 です。|  
|`leaseTimeout`|プールに返されたチャネルが閉じられるまでの時間を指定する <xref:System.TimeSpan>。 既定値は 00:10:00 です。|  
|`maxOutboundChannelsPerEndpoint`|各リモート エンドポイントのプール内に格納できるチャネルの最大数を指定する正の整数。 既定値は 10 です。|  
  
### <a name="child-elements"></a>子要素  
 なし。  
  
### <a name="parent-elements"></a>親要素  
  
|要素|Description|  
|-------------|-----------------|  
|[\<oneWay>](oneway.md)|カスタム バインドでパケット ルーティングを有効にします。|  
  
## <a name="remarks"></a>解説  
 クォータは、リソースの過剰な消費を防ぐためのポリシー メカニズムとして使用されます。 クォータは、悪質な、または意図的でないサービス拒否 (DOS) 攻撃を防ぎます。 カスタム チャネルにチャネル クォータを設定するには、この要素を使用します。  
  
 `ChannelPoolSettings` では、次の 3 つのクォータを指定します。  
  
- `idleTimeout` クォータは、サーバーでは、長時間リソースを停滞させることによるサービス拒否 (DOS) 攻撃を軽減するために使用されます。 クライアントでは、適切な値を設定することで、サービスとの接続の信頼性を高めることができます。 既定値では、リソースが控えめに割り当てられています。 開発環境、および小規模のインストール シナリオに適しています。 インストールでリソースが不足している場合、または追加リソースが使用可能であるにもかかわらず接続が制限されている場合、サービス管理者は値を確認する必要があります。  
  
- `leaseTimeout` クォータは、負荷分散機能との統合、および信頼性の向上のために使用されます。 既定値では、リソースが控えめに割り当てられています。 開発環境、および小規模のインストール シナリオに適しています。 インストールでリソースが不足している場合、または追加リソースが使用可能であるにもかかわらず接続が制限されている場合、サービス管理者は値を確認する必要があります。  
  
- `maxOutboundChannelsPerEndpoint` クォータは、サーバーとクライアントの両方に対するキャッシュ制限を設定し、信頼性向上のために使用されます。 既定値ではリソースが控えめに割り当てられており、開発環境および小規模なインストール シナリオに適しています。 インストールでリソースが不足している場合、または追加リソースが使用可能であるにもかかわらず接続が制限されている場合、サービス管理者は値を確認する必要があります。  
  
## <a name="see-also"></a>関連項目

- <xref:System.ServiceModel.Channels.OneWayBindingElement.ChannelPoolSettings%2A>
- <xref:System.ServiceModel.Channels.ChannelPoolSettings>
- <xref:System.ServiceModel.Configuration.OneWayElement.ChannelPoolSettings%2A>
- <xref:System.ServiceModel.Configuration.ChannelPoolSettingsElement>
- <xref:System.ServiceModel.Channels.CustomBinding>
- [\<oneWay>](oneway.md)
- [バインド](../../../wcf/bindings.md)
- [バインディングの拡張](../../../wcf/extending/extending-bindings.md)
- [カスタム バインディング](../../../wcf/extending/custom-bindings.md)
- [\<customBinding>](custombinding.md)
