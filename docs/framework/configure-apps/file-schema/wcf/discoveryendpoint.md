---
title: <discoveryEndpoint>
ms.date: 03/30/2017
ms.assetid: fae2f48b-a635-4e4b-859d-a1432ac37e1c
ms.openlocfilehash: 32b14f8fb3235040a51455f2099a403c8312c699
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "70855398"
---
# \<discoveryEndpoint>

この構成要素は、固定探索コントラクトが含まれた標準エンドポイントを定義します。 サービスの構成に追加すると、この要素により、探索メッセージをリッスンする場所が指定されます。 クライアントの構成に追加すると、この要素により、探索クエリの送信先となる場所が指定されます。  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<standardEndpoints>**](standardendpoints.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<discoveryEndpoint>**  
  
## <a name="syntax"></a>構文  
  
```xml  
<system.serviceModel>
  <standardEndpoints>
    <discoveryEndpoint>
      <standardEndpoint discoveryMode="Adhoc/Managed"
                        discoveryVersion="WSDiscovery11/WSDiscoveryApril2005"
                        maxResponseDelay="Timespan"
                        name="String" />
    </discoveryEndpoint>
  </standardEndpoints>
</system.serviceModel>
```  
  
## <a name="attributes-and-elements"></a>属性と要素

以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性

| 属性        | 説明 |  
| ---------------- | ----------- |  
| discoveryMode    | 探索プロトコルのモードを示す文字列。 有効な値は "アドホック" および "マネージ" です。 マネージド モードでは、プロトコルは Discoverable サービスのリポジトリとして機能する Discovery Proxy に依存します。 アドホック モードでは、プロトコルは UDP マルチキャスト メカニズムを使用して利用可能なサービスを探索する必要があります。 プロパティの詳細については、「」を参照してください <xref:System.ServiceModel.Discovery.DiscoveryEndpoint.DiscoveryMode%2A> 。 |  
| discoveryVersion | WS-Discovery プロトコルの 2 つのバージョンのうち、1 つを指定する文字列。 有効値は WSDiscovery11 と WSDiscoveryApril2005 です。 この値は、<xref:System.ServiceModel.Discovery.DiscoveryVersion> 型です。 |  
| maxResponseDelay | Discovery プロトコルが Probe Match や Resolve Match などのメッセージを送信するまでの待機時間の最大値を指定する Timespan 値。<br /><br /> すべての ProbeMatch が同時に送信されると、ネットワーク ストームが発生することがあります。 これを防ぐために、各 ProbeMatch はランダムな時間だけ待機して送信されます。 ランダムな待機時間は、0 からこの属性に設定された値の範囲内で設定されます。 この属性を 0 に設定すると、ProbeMatch メッセージは待機せずに短いループで送信されます。 それ以外の場合は、ProbeMatch メッセージはランダムな時間だけ待機して送信されます。すべての ProbeMatch メッセージの送信にかかる合計時間が maxResponseDelay を超えることはありません。 この値はサービスのみに関連するもので、クライアントが使用するものではありません。 |  
| `name`           | 標準エンドポイントの構成名を指定する文字列。 この名前は、サービス エンドポイントの `endpointConfiguration` 属性で使用され、標準エンドポイントと構成を関連付けます。 |  
  
### <a name="child-elements"></a>子要素

なし。  
  
### <a name="parent-elements"></a>親要素

| 要素 | Description |  
| ------- | ----------- |  
| [\<standardEndpoints>](standardendpoints.md) | 1 つ以上のプロパティ (アドレス、バインディング、コントラクト) が固定されている、あらかじめ定義されたエンドポイントである標準エンドポイントのコレクション。 |  
  
## <a name="example"></a>例

ピア ネットワーク マルチキャスト トランスポート経由で探索メッセージをリッスンするサービスの例を次に示します。 この例では、明示的に WS-Discovery April 2005 バージョンを指定します。  
  
標準エンドポイントの構成はサービスごとに定義します。サービス間で共有することはできません。 別のサービスで同じ探索エンドポイントを使用するには、該当のサービスのセクションに同じ構成を追加する必要があります。  
  
```xml  
<services>
  <service name="CalculatorService"
           behaviorConfiguration="CalculatorServiceBehavior">
    <endpoint binding="basicHttpBinding"
              address="calculator"
              contract="ICalculatorService" />
    <endpoint name="peerNetDiscovery"
              binding="peerTcpBinding"
              address="net.p2p://discoveryMesh/multicast"
              kind="discoveryEndpoint"
              endpointConfiguration="peerTcpDiscoveryEndpointConfiguration"
              bindingConfiguration="discoveryPeerTcpBindingConfig" />
  </service>
</services>
<standardEndpoints>
  <discoveryEndpoint>
    <standardEndpoint name="peerTcpDiscoveryEndpointConfiguration"
                      version="WSDiscoveryApril2005" />
  </discoveryEndpoint>
</standardEndpoints>
```  
  
## <a name="see-also"></a>関連項目

- <xref:System.ServiceModel.Discovery.DiscoveryEndpoint>
