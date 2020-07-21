---
title: <endpoint> の <client>
ms.date: 03/30/2017
ms.assetid: de6238ae-bbf8-48e9-a1b5-e24c0bea8afa
ms.openlocfilehash: f1ffbc1e8efac70523d7f631c8cf9ba9a1622bfc
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "70855323"
---
# <a name="endpoint-of-client"></a>\<endpoint> の \<client>
サーバーのサービス エンドポイントに接続するためにクライアントによって使用されるチャネル エンドポイントのコントラクト、バインディング、およびアドレスのプロパティを指定します。  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<client>**](client.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<endpoint>**  
  
## <a name="syntax"></a>構文  
  
```xml  
<endpoint address="String"
          behaviorConfiguration="String"
          binding="String"
          bindingConfiguration="String"
          contract="String"
          endpointConfiguration="String"
          kind="String"
          name="String">
</endpoint>
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|address|必須の文字列属性です。<br /><br /> エンドポイントのアドレスを指定します。 既定値は空の文字列です。 アドレスは、絶対 URI にする必要があります。|  
|behaviorConfiguration|エンドポイントのインスタンス化に使用される動作の動作名を含む文字列。 動作名は、サービスが定義される時点でスコープ内にある必要があります。 既定値は空の文字列です。|  
|binding|必須の文字列属性です。<br /><br /> 使用するバインディングの種類を示す文字列。 参照できるようにするには、種類は登録された構成セクションを持っている必要があります。 種類は、バインディングの種類の名前ではなくセクション名で登録されます。|  
|bindingConfiguration|省略可能。 エンドポイントがインスタンス化されるときに使用するバインディング構成の名前を含む文字列。 バインド構成は、エンドポイントが定義される時点でスコープ内にある必要があります。 既定値は空の文字列です。<br /><br /> この属性は、構成ファイル内の特定のバインディング構成を参照するために、`binding` と組み合わせて使用されます。 カスタム バインドを使用しようとする場合にこの属性を設定します。 そうでない場合は、例外がスローされることがあります。|  
|コントラクト (contract)|必須の文字列属性です。<br /><br /> このエンドポイントが公開するコントラクトを示す文字列。 アセンブリは、コントラクト型を実装する必要があります。|  
|endpointConfiguration|この標準エンドポイントの追加の構成情報を参照する `kind` 属性によって設定される標準エンドポイントの名前を指定する文字列。 同じ名前を `<standardEndpoints>` セクションに定義する必要があります。|  
|kind|適用する標準エンドポイントの種類を指定する文字列。 この型は、セクションまたは machine.config に登録する必要があり `<extensions>` ます。何も指定されていない場合は、共通のチャネルエンドポイントが作成されます。|  
|name|省略可能な文字列属性。 この属性は、特定のコントラクトのエンドポイントを一意に識別します。 特定のコントラクトの種類に、複数のクライアントを定義できます。 それぞれの定義は、一意の構成名で区別できるようにする必要があります。 この属性が省略されている場合、指定されたコントラクトの種類に関連する既定のエンドポイントとして、対応するエンドポイントが使用されます。 既定値は空の文字列です。<br /><br /> バインディングの `name` 属性は、WSDL を介した定義エクスポートに使用されます。|  
  
### <a name="child-elements"></a>子要素  
  
|要素|Description|  
|-------------|-----------------|  
|[\<headers>](headers.md)|アドレス ヘッダーのコレクション。|  
|[\<identity>](identity.md)|メッセージを交換する他のエンドポイントによるエンドポイントの認証を可能にする ID です。|  
  
### <a name="parent-elements"></a>親要素  
  
|要素|Description|  
|-------------|-----------------|  
|[\<client>](client.md)|クライアントが接続可能なエンドポイントの一覧を定義する設定セクションです。|  
  
## <a name="example"></a>例  
 これはチャネル エンドポイントの構成の例です。  
  
```xml  
<endpoint address="/HelloWorld/"
          bindingConfiguration="usingDefaults"
          name="MyBinding"
          binding="customBinding"
          contract="HelloWorld">
</endpoint>
```  
  
## <a name="see-also"></a>関連項目

- <xref:System.ServiceModel.Configuration.ChannelEndpointElement>
- <xref:System.ServiceModel.Configuration.ClientSection>
- <xref:System.ServiceModel.Configuration.ChannelEndpointElementCollection>
- <xref:System.ServiceModel.Configuration.ClientSection.Endpoints%2A>
- <xref:System.ServiceModel.Configuration.ChannelEndpointElement>
- [WCF クライアントの構成](../../../wcf/feature-details/client-configuration.md)
- [クライアント](../../../wcf/feature-details/clients.md)
