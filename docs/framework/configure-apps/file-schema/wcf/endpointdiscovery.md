---
title: <endpointDiscovery>
ms.date: 03/30/2017
ms.assetid: 70812717-888a-4748-9640-0df6715ff029
ms.openlocfilehash: 98b1655f42b7b43604ed4ab9d66870ec204a9590
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "70398016"
---
# \<endpointDiscovery>
エンドポイントのさまざまな探索設定を指定します (探索可能性、スコープ、メタデータに対するカスタム拡張など)。  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<behaviors>**](behaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<endpointBehaviors>**](endpointbehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<behavior>**](behavior-of-endpointbehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<endpointDiscovery>**  
  
## <a name="syntax"></a>構文  
  
```xml  
<behaviors>
  <endpointBehaviors>
    <behavior name="String">
      <endpointDiscovery enabled="Boolean">
        <scopes>
          <add scope="URI"/>
        </scopes>
        <extensions />
      </endpointDiscovery>
    </behavior>
  </endpointBehaviors>
</behaviors>
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|enabled|このエンドポイントで探索可能性が有効かどうかを指定するブール値です。 既定値は、`false` です。|  
  
### <a name="child-elements"></a>子要素  
  
|要素|Description|  
|-------------|-----------------|  
|[\<scopes>](scopes.md)|エンドポイントのスコープ URI のコレクション。 複数の URI を 1 つのエンドポイントに関連付けることができます。|  
|[\<extensions>](extensions.md)[/ \<endpointDiscovery> ]|エンドポイントで発行されるカスタム メタデータを指定できる、XML 要素のコレクション。|  
|\<types>|検索するインターフェイスのコレクション。|  
  
### <a name="parent-elements"></a>親要素  
  
|要素|Description|  
|-------------|-----------------|  
|[\<behavior>](behavior-of-endpointbehaviors.md)|動作の要素を指定します。|  
|||  
  
## <a name="remarks"></a>解説  
 エンドポイントの動作構成に追加し、`enabled` 属性を `true` に設定すると、この構成要素の探索可能性が有効になります。 また、子要素を使用して、 [\<scopes>](scopes.md) クエリ中にサービスエンドポイントをフィルター処理するために使用できるカスタムスコープ uri を指定したり、 [\<extensions>](extensions.md) 標準の探索可能なメタデータ (EPR、Contracttypename、Bindingname、Scope、ListenURI) と共に発行する必要があるカスタムメタデータを指定したりすることができます。  
  
 この構成要素は、探索可能性 [\<serviceDiscovery>](servicediscovery.md) のサービスレベルコントロールを提供する要素に依存します。 これは [\<serviceDiscovery>](servicediscovery.md) 、が構成内に存在しない場合に、この要素の設定が無視されることを意味します。  
  
## <a name="example"></a>例  
 次の構成例では、フィルターのスコープと、エンドポイントで発行される拡張メタデータを指定しています。  
  
```xml  
<services>
  <service name="CalculatorService"
           behaviorConfiguration="CalculatorServiceBehavior">
    <endpoint binding="basicHttpBinding"
              address="calculator"
              contract="ICalculatorService"
              behaviorConfiguration="calculatorEndpointBehavior" />
  </service>
</services>
<behaviors>
  <serviceBehaviors>
    <behavior name="CalculatorServiceBehavior">
      <serviceDiscovery />
    </behavior>
  </serviceBehaviors>
  <endpointBehaviors>
    <behavior name="calculatorEndpointBehavior">
      <endpointDiscovery enabled="true">
        <scopes>
          <add scope="http://contoso/test1" />
          <add scope="http://contoso/test2" />
        </scopes>
        <extensions>
          <e:Publisher xmlns:e="http://example.org">
            <e:Name>The Example Organization</e:Name>
            <e:Address>One Example Way, ExampleTown, EX 12345</e:Address>
            <e:Contact>support@example.org</e:Contact>
          </e:Publisher>
          <AnotherCustomMetadata>Custom Metadata</AnotherCustomMetadata>
        </extensions>
      </endpointDiscovery>
    </behavior>
  </endpointBehaviors>
</behaviors>
```  
  
## <a name="see-also"></a>関連項目

- <xref:System.ServiceModel.Discovery.EndpointDiscoveryBehavior>
