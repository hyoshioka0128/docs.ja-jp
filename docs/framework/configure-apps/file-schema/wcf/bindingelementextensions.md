---
title: <bindingElementExtensions>
ms.date: 03/30/2017
ms.assetid: bb597fc0-c947-451c-afda-bf23d42f4f4d
ms.openlocfilehash: c323a65ace332d2ecd1e03330dddbe7ca17ff5bd
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "69926369"
---
# \<bindingElementExtensions>
このセクションは、コンピューターまたはアプリケーションの構成ファイルからカスタム バインディング要素を使用できます。 このコレクションにカスタム バインド要素を追加するには、`add` キーワードを使用し、要素の `type` 属性をバインド要素拡張に設定して、`name` 属性をカスタム バインド要素に設定します。  
  
 バインディングの拡張により、ユーザーは、カスタム バインドの一部として使用するユーザー定義のバインド要素を作成できます。 プログラムではバインディング拡張は、抽象クラス <xref:System.ServiceModel.Channels.BindingElement> を実装する型です。 構成ファイルでは、`bindingElementExtensions` セクションは、拡張要素を定義するために使用されます。  
  
 次の例は、`add` 要素と `name` 属性を使用して、構成ファイルの `bindingElementExtensions` セクションにバインディング拡張を追加します。  
  
```xml  
<system.serviceModel>
  <extensions>
    <bindingElementExtensions>
      <add name="udpTransport"
           type="Microsoft.ServiceModel.Samples.UdpTransportSection, UdpTransport,
                 Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
    </bindingElementExtensions>
  </extensions>
</system.serviceModel>
```  
  
 構成機能を要素に追加するには、ユーザーは `bindingElementExtensionSection` を記述して登録する必要があります。 詳細については、<xref:System.Configuration> を参照してください。  
  
 要素とその構成の型を定義したら、次の例に示すように拡張をカスタム バインドの一部として使用できます。  
  
```xml  
<customBinding>
  <binding name="test2">
    <udpTransport />
    <binaryMessageEncoding maxReadPoolSize="211"
                           maxWritePoolSize="2132"
                           maxSessionSize="3141" />
  </binding>
</customBinding>
```  
  
## <a name="see-also"></a>関連項目

- <xref:System.ServiceModel.Configuration.BindingElementExtensionElement>
- [バインディングの拡張](../../../wcf/extending/extending-bindings.md)
