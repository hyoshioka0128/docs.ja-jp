---
title: <exposedMethod>
ms.date: 03/30/2017
ms.assetid: 61c938cd-4ee9-4b06-ab28-922ef491ab11
ms.openlocfilehash: 46f2872fb289c2793c356ea179deb3ce52e6d65e
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "70855312"
---
# \<exposedMethod>
COM+ コンポーネントのインターフェイスが Web サービスとして公開されるときに公開される COM+ メソッドを表します。  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<comContracts>**](comcontracts.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<comContract>**](comcontract.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<exposedMethods>**](exposedmethods.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<exposedMethod>**  
  
## <a name="syntax"></a>構文  
  
```xml  
<comContracts>
  <comContract>
    <exposedMethods>
      <exposedMethod name="String" />
    </exposedMethods>
  </comContract>
</comContracts>
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|name|COM+ コンポーネントのインターフェイスが Web サービスとして公開されるときに公開される COM+ メソッドを含む文字列。|  
  
### <a name="child-elements"></a>子要素  
 なし。  
  
### <a name="parent-elements"></a>親要素  
  
|要素|Description|  
|-------------|-----------------|  
|[\<exposedMethods>](exposedmethods.md)|要素のコレクション [\<exposedMethod>](exposedmethod.md) 。|  
  
## <a name="remarks"></a>解説  
 COM+ 統合構成ツール (ComSvcConfig.exe) を使用して、COM インターフェイスから特定のメソッドを追加して、生成されるサービス コントラクトに表示できます。  
  
 たとえば、次のコマンドを使用して、`IFinances`.Financial コンポーネントの `ItemOrders` COM インターフェイスから、3 つの名前付きメソッドを、生成されるサービス コントラクトに追加できます。  
  
 `ComSvcConfig.exe /i /application:OnlineStore /contract:ItemOrders.Financial,IFinances.{TransferFunds,AddFunds,RemoveFunds} /hosting:complus`  
  
 また、Comsvcconfig.exe を実行すると、前述のメソッドを要素として一覧表示する次のサービスコントラクトが生成され [\<exposedMethod>](exposedmethod.md) ます。  
  
```xml  
<comContract contractType="{C551FBA9-E3AA-4272-8C2A-84BD8D290AC7}"
             name="IFinances"
             namespace="http://contoso.com/services/financial">
  <exposedMethod name="TransferFunds"/>
  <exposedMethod name="AddFunds"/>
  <exposedMethod name="RemoveFunds"/>
</comContract>
```  
  
 サービスの初期化時に、ランタイムは、要素のリストに含まれているメソッドのみを反映し、追加することによって、サービスコントラクトの生成を試み [\<exposedMethod>](exposedmethod.md) ます。 トレースは、サービス コントラクトに含まれないインターフェイス メソッド用に作成されます。  
  
## <a name="see-also"></a>関連項目

- <xref:System.ServiceModel.Configuration.ComMethodElementCollection>
- <xref:System.ServiceModel.Configuration.ComMethodElement>
- [\<comContracts>](comcontracts.md)
- [COM + アプリケーションとの統合](../../../wcf/feature-details/integrating-with-com-plus-applications.md)
- [方法: COM+ サービス設定を構成する](../../../wcf/feature-details/how-to-configure-com-service-settings.md)
