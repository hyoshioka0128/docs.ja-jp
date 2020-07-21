---
title: <comContract>
ms.date: 03/30/2017
ms.assetid: 3f8e1c0c-cfdf-4c79-ac65-c64e9323a51c
ms.openlocfilehash: b499294af71ba230dcf985d4af1d013b1ca260cf
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "70850030"
---
# \<comContract>
COM+ 統合サービス コントラクトを指定します。  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<comContracts>**](comcontracts.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<comContract>**  
  
## <a name="syntax"></a>構文  
  
```xml  
<comContracts>
  <comContract contract="String"
               namespace="String"
               name="String"
               requireSession="Boolean">
    <exposedMethods>
      <exposedMethod name="String" />
    </exposedMethods>
    <userDefinedTypes>
      <userDefinedType name="String"
                       typeLibID="String"
                       typeLibVersion="String"
                       typeDefID="String">
      </userDefinedType>
    </userDefinedTypes>
    <persistableTypes>
      <persistableType id="String"
                       name="String">
      </persistableType>
    </persistableTypes>
  </comContract>
</comContracts>
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|コントラクト (contract)|コントラクトの種類を含む文字列。|  
|name|コントラクト名を含む文字列。|  
|namespace|コントラクトの名前空間を含む文字列。|  
|requiresSession|コントラクトをセッションの多いバインディングでのみ使用できるかどうかを指定するブール値。 サービスが初期化される場合、統合ランタイムは、この設定が、使用されるバインディングの種類と一貫していることを保証します。 コントラクト内の 1 つ以上のバインディングが競合する場合は、例外が生成されます。 このプロパティが `false` で、一方向のチャネルを使用し、いずれかの [out] パラメーターが存在する場合は、例外も発生します。|  
  
### <a name="child-elements"></a>子要素  
  
|要素|Description|  
|-------------|-----------------|  
|persistableTypes|すべての永続型。|  
|userDefinedTypes|サービス コントラクトに含まれるユーザー定義型 (UDT) のコレクション。|  
|exposedMethods|COM+ コンポーネントのインターフェイスが Web サービスとして公開されるときに公開される COM+ メソッドのコレクション。|  
  
### <a name="parent-elements"></a>親要素  
  
|要素|Description|  
|-------------|-----------------|  
|comContracts|`comContract` 要素のコレクションを含みます。|  
  
## <a name="remarks"></a>解説  
 現在、COM + 統合サービスコントラクトは名前空間に限定され `http://tempuri.org` ており、コントラクト名はサポートする COM インターフェイスから派生します。 ただし、構成ファイルの `comContracts` セクションと `comContract` 要素を使用して代替を指定することができます。 たとえば、次の構成を使用して、名前空間、コントラクト名、組み込まれるユーザー定義型、およびサービス コントラクトのその他の設定を指定できます。  
  
```xml  
<comContracts>
  <comContract contract="{5163B1E7-F0CF-4B6A-9A02-4AB654F34284}"
               namespace="http://tempuri.org/5163B1E7-F0CF-4B6A-9A02-4AB654F34284"
               name="_Broker"
               requireSession="true">
    <exposedMethods>
      <exposedMethod name="BuyStock" />
      <exposedMethod name="SellStock" />
      <exposedMethod name="ExecuteTransaction" />
    </exposedMethods>
  </comContract>
</comContracts>
```  
  
 サービスが初期化される場合、指定した名前空間およびコントラクト名が、生成されるサービスの説明に適用されます。  
  
## <a name="see-also"></a>関連項目

- <xref:System.ServiceModel.Configuration.ComContractElementCollection>
- <xref:System.ServiceModel.Configuration.ComContractElement>
- [\<comContracts>](comcontracts.md)
- [COM + アプリケーションとの統合](../../../wcf/feature-details/integrating-with-com-plus-applications.md)
- [方法: COM+ サービス設定を構成する](../../../wcf/feature-details/how-to-configure-com-service-settings.md)
