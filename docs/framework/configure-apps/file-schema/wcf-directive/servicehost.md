---
title: '@ServiceHost'
ms.date: 03/30/2017
ms.assetid: 96ba6967-00f2-422f-9aa7-15de4d33ebf3
ms.openlocfilehash: cb425d9f4dadd97e93946a2b4cd9d059ea8504ce
ms.sourcegitcommit: 0edbeb66d71b8df10fcb374cfca4d731b58ccdb2
ms.contentlocale: ja-JP
ms.lasthandoff: 07/07/2020
ms.locfileid: "86051364"
---
# <a name="servicehost"></a>\@ServiceHost

サービス ホストの生成に使用されるファクトリを、ホストされるサービスと、.svc ファイルで提供されるホスティング コードのアクセスとコンパイルに必要なその他のプログラミング部分に関連付けます。

## <a name="syntax"></a>構文

```aspx-csharp
<% @ServiceHost
Service = "Service, ServiceNamespace"
Factory = "Factory, FactoryNamespace"
Debug = "Debug"
Language = "Language"
CodeBehind = "CodeBehind"
%>
```

## <a name="attributes"></a>属性

### <a name="service"></a>サービス

ホストされるサービスの CLR 型名。 これは、1 つ以上のサービス コンタクトを実装する型の修飾名にする必要があります。

### <a name="factory"></a>ファクトリ

サービス ホストのインスタンス化に使用されるサービス ホスト ファクトリの CLR 型名。 この属性は省略できます。 未指定の場合は、<xref:System.ServiceModel.Activation.ServiceHostFactory> のインスタンスを返す既定の <xref:System.ServiceModel.ServiceHost> が使用されます。

### <a name="debug"></a>デバッグ

デバッグシンボルを使用して Windows Communication Foundation (WCF) サービスをコンパイルする必要があるかどうかを示します。 `true`デバッグシンボルを使用して WCF サービスをコンパイルする必要がある場合は、それ以外の場合は `false` 。

### <a name="language"></a>Language

ファイル (.svc) 内のすべてのインライン コードをコンパイルするときに使用する言語を指定します。 値は任意のを表すことができます。、、およびを含む、.NET でサポートされている言語 `C#` `VB` `JS` 。それぞれ C#、Visual Basic、JScript .net を参照します。 この属性は省略できます。

### <a name="codebehind"></a>分離コード

Xml web サービスを実装するクラスが同じファイル内に存在せず、アセンブリにコンパイルされずに*\bin*ディレクトリに配置されている場合に、xml web サービスを実装するソースファイルを指定します。

## <a name="remarks"></a>注釈

<xref:System.ServiceModel.ServiceHost>サービスをホストするために使用されるは、Windows Communication Foundation (WCF) プログラミングモデル内の機能拡張ポイントです。 ファクトリ パターンは、ホスティング環境が直接インスタンス化できないポリモーフィック型の可能性があるため、<xref:System.ServiceModel.ServiceHost> のインスタンス化に使用されます。

既定の実装では <xref:System.ServiceModel.Activation.ServiceHostFactory> を使用して、<xref:System.ServiceModel.ServiceHost> のインスタンスを作成します。 ただし、ディレクティブでファクトリ実装の CLR 型名を指定することで、独自のファクトリ (派生ホストを返すもの) を指定でき `@ServiceHost` ます。

既定のファクトリの代わりにカスタムサービスホストファクトリを使用するには、次のようにディレクティブに型名を指定するだけ `@ServiceHost` です。

```xml
<% @ServiceHost Factory="DerivedFactory" Service="MyService" %>
```

ファクトリ実装はできるだけ軽量に保持してください。 多くのカスタム ロジックがある場合は、それらのロジックをファクトリ内部ではなくホスト内部に置くとコードがさらに再利用可能になります。

たとえば、の AJAX 対応エンドポイントを有効にするには、 `MyService` <xref:System.ServiceModel.Activation.WebScriptServiceHostFactory> 次の `Factory` <xref:System.ServiceModel.Activation.ServiceHostFactory> `@ServiceHost` 例に示すように、ディレクティブで属性の値としてを指定します。既定値は使用しません。

```aspx-csharp
<% @ServiceHost
Service="MyService"
Language="C#"
Debug="true"
Factory="WebScriptServiceHostFactory"
%>
```

## <a name="see-also"></a>関連項目

- [カスタム サービス ホスト](../../../wcf/samples/custom-service-host.md)
