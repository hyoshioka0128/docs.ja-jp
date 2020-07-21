---
title: <endpoint> 要素
ms.date: 03/30/2017
ms.assetid: 2fc8fedc-78d0-4e87-8142-fbfd26c15a4e
ms.openlocfilehash: fb9d3bf9b5f1a742abcc70d78af026c179ec4c4d
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "70855383"
---
# <a name="endpoint-element"></a>\<endpoint> 要素
サービスの公開に使用されるサービス エンドポイントのバインディング、コントラクト、およびアドレスのプロパティを指定します。  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<services>**](services.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<service>**](service.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<endpoint>**  
  
## <a name="syntax"></a>構文  
  
```xml  
<endpoint address="String"
          behaviorConfiguration="String"
          binding="String"
          bindingConfiguration="String"
          bindingName="String"
          bindingNamespace="String"
          contract="String"
          endpointConfiguration="String"
          isSystemEndpoint="Boolean"
          kind="String"
          listenUriMode="Explicit/Unique"
          listenUri="Uri">
</endpoint>
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|address|エンドポイントのアドレスを含む文字列。 アドレスは、絶対または相対アドレスとして指定できます。 相対アドレスが提供されている場合、ホストは、そのバインディングで使用されるトランスポート スキームに適したベース アドレスが提供されることを想定します。 アドレスが構成されていない場合、ベース アドレスはそのエンドポイントのアドレスと見なされます。<br /><br /> 既定値は空の文字列です。|  
|behaviorConfiguration|エンドポイントで使用される動作の名前を含む文字列。|  
|binding|使用するバインディングの種類を指定する必須の文字列属性。 参照できるようにするには、種類は登録された構成セクションを持っている必要があります。 種類は、バインディングの種類の名前ではなくセクション名で登録されます。|  
|bindingConfiguration|エンドポイントがインスタンス化されるときに使用するバインディングのバインディング名を指定する文字列。 バインディング名は、エンドポイントが定義される時点でスコープ内にある必要があります。 既定値は空の文字列です。<br /><br /> この属性は、構成ファイル内の特定のバインディング構成を参照するために、`binding` と組み合わせて使用されます。 カスタム バインドを使用しようとする場合にこの属性を設定します。 そうでない場合は、例外がスローされることがあります。|  
|bindingName|WSDL を介した定義エクスポートに使用するバインディングの一意の修飾名を指定する文字列。 既定値は空の文字列です。|  
|bindingNamespace|WSDL を介した定義エクスポートに使用するバインディングの名前空間の修飾名を指定する文字列。 既定値は空の文字列です。|  
|コントラクト (contract)|このエンドポイントが公開するコントラクトを示す文字列。 アセンブリは、コントラクト型を実装する必要があります。 サービス実装が単一のコントラクトの型を実装する場合は、このプロパティを省略できます。 既定値は空の文字列です。|  
|endpointConfiguration|この標準エンドポイントの追加の構成情報を参照する `kind` 属性によって設定される標準エンドポイントの名前を指定する文字列。 同じ名前を `<standardEndpoints>` セクションに定義する必要があります。|  
|isSystemEndpoint|インフラストラクチャ エンドポイントであるかどうかを指定するブール値。|  
|kind|適用する標準エンドポイントの種類を指定する文字列。 この型は、セクションまたは machine.config に登録する必要があり `<extensions>` ます。何も指定されていない場合は、共通のサービスエンドポイントが作成されます。|  
|listenUriMode|リッスンするサービスに提供される `ListenUri` をトランスポートが処理する方法を指定します。 有効な値は、次のとおりです。<br /><br /> -Explicit<br />-一意<br /><br /> 既定値は Explicit です。|  
|listenUri|サービス エンドポイントがリッスンする URI を指定する文字列。 既定値は空の文字列です。|  
|name|省略可能な属性です。 サービス エンドポイントの名前を指定する文字列。 既定値は、バインディング名とコントラクトの説明の名前を連結した値です。 サービスには複数のエンドポイントが存在する場合があるため、エンドポイントの `name` 属性はサービスの名前とは異なります。|  
  
### <a name="child-elements"></a>子要素  
  
|要素|Description|  
|-------------|-----------------|  
|[\<headers>](headers.md)|アドレス ヘッダーのコレクション。|  
|[\<identity>](identity.md)|メッセージを交換する他のエンドポイントによるエンドポイントの認証を可能にする ID です。|  
  
### <a name="parent-elements"></a>親要素  
  
|要素|Description|  
|-------------|-----------------|  
|[\<service>](service.md)|クライアントが接続可能なエンドポイントの一覧を定義する設定セクションです。|  
  
## <a name="example"></a>例  
 これはサービス エンドポイントの構成の例です。  
  
```xml  
<endpoint address="/HelloWorld/"
          bindingConfiguration="usingDefaults"
          bindingName="MyBinding"
          binding="customBinding"
          contract="HelloWorld">
  <headers>
    <region xmlns="http://tempuri.org/">EastCoast</region>
    <member xmlns="http://tempuri.org/">Gold</member>
  </headers>
</endpoint>
```  
  
## <a name="see-also"></a>関連項目

- <xref:System.ServiceModel.Configuration.ServiceEndpointElement>
- <xref:System.ServiceModel.EndpointAddress>
- <xref:System.ServiceModel.Description.ServiceEndpoint>
- [エンドポイント:アドレス、バインディング、およびコントラクト](../../../wcf/feature-details/endpoints-addresses-bindings-and-contracts.md)
- [方法: 構成にサービス エンドポイントを作成する](../../../wcf/feature-details/how-to-create-a-service-endpoint-in-configuration.md)
