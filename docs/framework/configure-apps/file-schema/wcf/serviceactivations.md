---
title: <serviceActivations>
ms.date: 03/30/2017
ms.assetid: 97e665b6-1c51-410b-928a-9bb42c954ddb
ms.openlocfilehash: 64ae0bfd90ae941fc78515c7936c998201c87485
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "70855138"
---
# \<serviceActivations>

Windows Communication Foundation (WCF) サービスの種類にマップする仮想サービスのアクティブ化の設定を定義する設定を追加できるようにする構成要素。 これにより、.svc ファイルを使用せずに、WAS/IIS でホストされているサービスをアクティブ化できます。

[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<serviceHostingEnvironment>**](servicehostingenvironment.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<serviceActivations>**  

## <a name="syntax"></a>構文

```xml
<serviceHostingEnvironment>
  <serviceActivations>
    <add factory="String"
         service="String" />
  </serviceActivations>
</serviceHostingEnvironment>
```

## <a name="attributes-and-elements"></a>属性および要素

以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

なし。

### <a name="child-elements"></a>子要素

|要素|説明|
|-------------|-----------------|
|[\<add>](add-of-serviceactivations.md)|サービス アプリケーションのアクティベーションを指定する構成要素を追加します。|

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[\<serviceHostingEnvironment>](servicehostingenvironment.md)|環境をホストするサービスがインスタンス化する特定のトランスポートの型を定義します。|

## <a name="remarks"></a>解説

web.config ファイルでアクティベーション設定を構成する方法を次の例に示します。

```xml
<configuration>
  <system.serviceModel>
    <serviceHostingEnvironment>
      <serviceActivations>
        <add service="GreetingService" />
      </serviceActivations>
    </serviceHostingEnvironment>
  </system.serviceModel>
</configuration>
```

この構成を使用して、.svc ファイルを使用せずに、GreetingService をアクティブ化できます。

`<serviceHostingEnvironment>` はアプリケーション レベルの構成であることに注意してください。 構成を格納した `web.config` は、仮想アプリケーションのルートの下に配置する必要があります。 また、 `serviceHostingEnvironment` は machineToApplication 継承可能なセクションです。 コンピューターのルートに単一のサービスを登録すると、アプリケーションの各サービスはこのサービスを継承します。

構成ベースのアクティベーションは、http および非 http プロトコル経由のアクティベーションをサポートします。 これには、relativeAddress、xoml、または .xamlx の拡張機能が必要です。 既知の buildProviders に対して独自の拡張子をマップできます。これにより、任意の拡張子を使用してサービスをアクティブ化できるようになります。 競合が発生した場合には、`<serviceActivations>` セクションにより、.svc の登録がオーバーライドされます。

## <a name="see-also"></a>関連項目

- <xref:System.ServiceModel.Configuration.ServiceActivationElementCollection>
- <xref:System.ServiceModel.Configuration.ServiceHostingEnvironmentSection>
- <xref:System.ServiceModel.ServiceHostingEnvironment>
