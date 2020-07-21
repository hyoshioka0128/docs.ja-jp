---
title: <bindingExtensions>
ms.date: 03/30/2017
ms.assetid: 8373f94d-d095-486f-8f1e-4ac2f72b58c7
ms.openlocfilehash: bd6aeb32e0994bceb9e56bcb1c6267f4cb64a5a4
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "73039145"
---
# \<bindingExtensions>

このセクションは、コンピューターまたはアプリケーションの構成ファイルからユーザー定義のバインディングを使用できます。 このコレクションにユーザー定義のバインディングを追加するには、`add` キーワードを使用し、要素の `type` 属性をユーザー定義のバインディングに設定して、`name` 属性をユーザー定義のバインディングの名前に設定します。

バインディングの拡張により、ユーザーは、エンドポイント構成の一部として使用するユーザー定義のバインディングを作成できます。 プログラムではバインディング拡張は、抽象クラス <xref:System.ServiceModel.Channels.Binding> を実装する型です。

次の例では、要素と属性を使用して、 `add` `name` 構成ファイルのセクションにバインド拡張機能を追加し `bindingExtensions` ます。

```xml
<system.serviceModel>
  <extensions>
    <bindingExtensions>
      <add name="MyBinding"
           type="Microsoft.ServiceModel.Samples.MyBinding, MyBinding,
                 Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
    </bindingExtensions>
  </extensions>
</system.serviceModel>
```

構成機能を要素に追加するには、ユーザーは `bindingSection` を記述して登録する必要があります。 詳細については、<xref:System.Configuration> を参照してください。

要素とその構成の種類を定義した後、次の例に示すように、エンドポイントの一部として拡張機能を使用できます。

```xml
<services>
  <service name="MyService">
    <endpoint address="myAddress"
              binding="MyBinding" />
  </service>
</services>
```

## <a name="see-also"></a>関連項目

- [バインディングの拡張](../../../wcf/extending/extending-bindings.md)
