---
title: 信頼できるメッセージング プロトコル バージョン 1.1
ms.date: 03/30/2017
ms.assetid: 0da47b82-f8eb-42da-8bfe-e56ce7ba6f59
ms.openlocfilehash: ad0a77842c10965749eab4e76bb123938e07e9d5
ms.sourcegitcommit: ee5b798427f81237a3c23d1fd81fff7fdc21e8d3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/28/2020
ms.locfileid: "84144722"
---
# <a name="reliable-messaging-protocol-version-11"></a>信頼できるメッセージング プロトコル バージョン 1.1

このトピックでは、HTTP トランスポートを使用した相互運用に必要な Ws-reliablemessaging 2007 (バージョン 1.1) プロトコルの Windows Communication Foundation (WCF) 実装の詳細について説明します。 WCF は、このトピックで説明する制約と説明を使用して、ws-reliablemessaging 仕様に従います。 Ws-reliablemessaging バージョン1.1 プロトコルは .NET Framework 3.5 以降で実装されることに注意してください。

Ws-reliablemessaging 2 月2007プロトコルは、WCF でによって実装され <xref:System.ServiceModel.Channels.ReliableSessionBindingElement> ます。

便宜上、ここでは次のロールを使用します。

- イニシエーター : WS-Reliable メッセージ シーケンスの作成を開始するクライアント。

- レスポンダー : イニシエーターの要求を受け取るサービス。

 このドキュメントでは、次の表に示すプレフィックスと名前空間を使用します。

|Prefix|名前空間|
|-|-|
|wsrm|`http://docs.oasis-open.org/ws-rx/wsrm/200702`|
|netrm|`http://schemas.microsoft.com/ws/2006/05/rm`|
|s|`http://www.w3.org/2003/05/soap-envelope`|
|wsa|`http://schemas.xmlsoap.org/ws/2005/08/addressing`|
|wsse|`http://docs.oasis-open.org/wss/2004/01/oasis-200401-wssecurity-secext-1.0.xsd`|
|wsrmp|`http://docs.oasis-open.org/ws-rx/wsrmp/200702`|
|netrmp|`http://schemas.microsoft.com/ws-rx/wsrmp/200702`|
|wsp|(WS-Policy 1.2 または WS-Policy 1.5 のいずれか)|

## <a name="messaging"></a>メッセージング

### <a name="sequence-creation"></a>シーケンスの作成

WCF `CreateSequence` では、メッセージとメッセージを実装して、 `CreateSequenceResponse` 信頼できるメッセージシーケンスを確立します。 以下の制約が適用されます。

- B1101: WCF イニシエーターは `CreateSequence` 、メッセージの、、およびと同じエンドポイント参照を使用し `ReplyTo` `AcksTo` `Offer/Endpoint` ます。

- R1102: `AcksTo` メッセージの `ReplyTo`、`Offer/Endpoint`、および `CreateSequence` の各エンドポイント参照には、オクテット単位で一致する同じ文字列表現のアドレス値が必要です。

  - WCF レスポンダーは、 `AcksTo` `ReplyTo` `Endpoint` シーケンスを作成する前に、、、およびの各エンドポイント参照の URI 部分が同一であることを確認します。

- R1103: `AcksTo` メッセージの `ReplyTo`、`Offer/Endpoint`、および `CreateSequence` の各エンドポイント参照には、同一の参照パラメーターのセットが必要です。

  - WCF では強制されませんが、の参照パラメーターとの `AcksTo` `ReplyTo` `Offer/Endpoint` エンドポイント参照が同一であることを前提 `CreateSequence` とし、エンドポイント参照の参照パラメーターを使用して `ReplyTo` 受信確認と逆方向シーケンスメッセージを使用します。

- B1104: WCF イニシエーターは、メッセージ内に省略可能なまたは要素を生成しません `Expires` `Offer/Expires` `CreateSequence` 。

- B1105: メッセージにアクセスするとき `CreateSequence` 、WCF レスポンダーは要素の値を `Expires` 要素の `CreateSequence` 値として使用し `Expires` `CreateSequenceResponse` ます。 それ以外の場合、WCF レスポンダーはとの値を読み取り、無視し `Expires` `Offer/Expires` ます。

- B1106: メッセージにアクセスするときに、 `CreateSequenceResponse` WCF イニシエーターは省略可能な値を読み取り `Expires` ますが、使用しません。

- B1107: WCF の開始側と応答側は常に、 `IncompleteSequenceBehavior` 要素と要素にオプションの要素を生成し `CreateSequence/Offer` `CreateSequenceResponse` ます。

- B1108: WCF では、 `DiscardFollowingFirstGap` `NoDiscard` 要素内の値と値のみが使用さ `IncompleteSequenceBehavior` れます。

  - WS-ReliableMessaging では、セッションを形成する、相関する 2 つの逆方向シーケンスを確立するために、`Offer` 機構を利用しています。

- B1109: に `CreateSequence` 要素が含まれている場合 `Offer` 、WCF レスポンダーの一方向は、要素のないで応答することによって提供されるシーケンスを拒否し `CreateSequenceResponse` `Accept` ます。

- B1110: 信頼できるメッセージングレスポンダーが提供されたシーケンスを拒否する場合、WCF イニシエーターは新しく確立されたシーケンスをエラーにします。

- B1111: に `CreateSequence` 要素が含まれていない場合 `Offer` 、双方向の WCF レスポンダーは、エラーで応答することによって提供されたシーケンスを拒否し `CreateSequenceRefused` ます。

- R1112: 2 つの逆方向シーケンスが `Offer` 機構を使用して確立された場合、`[address]` エンドポイント参照の `CreateSequenceResponse/Accept/AcksTo` プロパティは、バイト単位で `CreateSequence` メッセージの送信先 URI と一致する必要があります。

- R1113: 2 つの逆方向シーケンスが `Offer` 機構を使用して確立された場合、イニシエーターからレスポンダーに流れる両方のシーケンスにあるすべてのメッセージは、同じエンドポイント参照に送信される必要があります。

WCF では、ws-reliablemessaging を使用して、イニシエーターとレスポンダーの間に信頼できるセッションを確立します。 WCF Ws-reliablemessaging 実装は、一方向、要求/応答、および全二重のメッセージングパターンに対して信頼できるセッションを提供します。 `Offer` および `CreateSequence` で WS-ReliableMessaging の `CreateSequenceResponse` 機構を使用すると、相関する 2 つの逆方向シーケンスを確立できます。また、Offer 機構は、すべてのメッセージ エンドポイントに適したセッション プロトコルを提供します。 WCF では、セッション整合性に対するエンドツーエンドの保護を含むこのようなセッションに対してセキュリティ保証が提供されるため、同じパーティを対象としたメッセージが同じ送信先に到着することを確認することが実用的です。 また、これにより、アプリケーション メッセージにシーケンス受信確認を抱き合わせることができます。 したがって、制約 R1102、R1112、および R1113 は WCF に適用されます。

`CreateSequence` メッセージの例を次に示します。

```xml
<s:Envelope>
  <s:Header>
    <wsa:Action s:mustUnderstand="1">http://docs.oasis-open.org/ws-rx/wsrm/200702/CreateSequence</wsa:Action>
    <wsa:MessageID>urn:uuid:949cca61-8813-42ff-ab33-18d9e3fa82fa</wsa:MessageID>
    <wsa:ReplyTo>
        <wsa:Address>http://Business456.com/clientA</wsa:Address>
    </wsa:ReplyTo>
    <wsa:To s:mustUnderstand="1">http://BusinessABC.com/serviceA</wsa:To>
  </s:Header>
  <s:Body>
    <wsrm:CreateSequence>
      <wsrm:AcksTo>
        <wsa:Address>http://Business456.com/clientA</wsa:Address>
      </wsrm:AcksTo>
      <wsrm:Offer>
        <wsrm:Identifier>urn:uuid:066b4730-fc82-458a-a5c1-210be4fb4e4e</wsrm:Identifier>
        <wsrm:Endpoint>
          <wsa:Address>http://Business456.com/clientA</wsa:Address>
        </wsrm:Endpoint>
        <wsrm:IncompleteSequenceBehavior>DiscardFollowingFirstGap</wsrm:IncompleteSequenceBehavior>
      </wsrm:Offer>
    </wsrm:CreateSequence>
  </s:Body>
</s:Envelope>
```

`CreateSequenceResponse` メッセージの例を次に示します。

```xml
<s:Envelope>
  <s:Header>
    <wsa:Action s:mustUnderstand="1">http://docs.oasis-open.org/ws-rx/wsrm/200702/CreateSequenceResponse</wsa:Action>
    <wsa:RelatesTo>urn:uuid:949cca61-8813-42ff-ab33-18d9e3fa82fa</wsa:RelatesTo>
    <wsa:To s:mustUnderstand="1">http://Business456.com/clientA</wsa:To>
  </s:Header>
  <s:Body>
    <wsrm:CreateSequenceResponse>
      <wsrm:Identifier>urn:uuid:656652b8-9af2-4e94-9d07-2dc21c05ed27</wsrm:Identifier>
      <wsrm:IncompleteSequenceBehavior>DiscardFollowingFirstGap</wsrm:IncompleteSequenceBehavior>
      <wsrm:Accept>
        <wsrm:AcksTo>
          <wsa:Address>http://BusinessABC.com/serviceA</wsa:Address>
        </wsrm:AcksTo>
      </wsrm:Accept>
    </wsrm:CreateSequenceResponse>
  </s:Body>
</s:Envelope>
```

### <a name="closing-a-sequence"></a>シーケンスを閉じる

WCF は、メッセージとメッセージを使用して、 `CloseSequence` `CloseSequenceResponse` 信頼性の高いメッセージングソースによるシャットダウンを実行します。 WCF の信頼できるメッセージの送信先はシャットダウンを開始せず、WCF Reliable Messaging source は、信頼できるメッセージングの送信先が開始したシャットダウンをサポートしていません。 以下の制約が適用されます。

- B1201: WCF Reliable Messaging ソースは、シーケンスをシャットダウンするために常にメッセージを送信し `CloseSequence` ます。

- B1202: 信頼できるメッセージの送信元は、`CloseSequence` メッセージを送信する前に、すべてのシーケンス メッセージの受信確認を待機します。

- B1203: 信頼できるメッセージの送信元は、シーケンスにメッセージが含まれない場合を除き、常にオプションの `LastMsgNumber` 要素を含めます。

- R1204: 信頼できるメッセージの送信先は、`CloseSequence` メッセージを送信してシャットダウンを開始することはできません。

- B1205: メッセージを受信する `CloseSequence` と、WCF Reliable Messaging ソースはシーケンスが不完全であると見なし、エラーを送信します。

 `CloseSequence` メッセージの例を次に示します。

```xml
<s:Envelope>
  <s:Header>
    <wsa:Action s:mustUnderstand="1">http://docs.oasis-open.org/ws-rx/wsrm/200702/CloseSequence</wsa:Action>
    <wsa:MessageID>urn:uuid:6ce1d4c3-e1c1-474f-a8c9-4210e37f7877</wsa:MessageID>
    <wsa:ReplyTo>
      <wsa:Address>http://Business456.com/clientA</wsa:Address>
    </wsa:ReplyTo>
    <wsa:To s:mustUnderstand="1">http://BusinessABC.com/serviceA</wsa:To>
  </s:Header>
  <s:Body>
    <wsrm:CloseSequence>
      <wsrm:Identifier>urn:uuid:656652b8-9af2-4e94-9d07-2dc21c05ed27</wsrm:Identifier>
      <wsrm:LastMsgNumber>30</wsrm:LastMsgNumber>
    </wsrm:CloseSequence>
  </s:Body>
</s:Envelope>
```

メッセージの例 `CloseSequenceResponse` :

```xml
<s:Envelope>
  <s:Header>
    <wsrm:SequenceAcknowledgement>
      <wsrm:Identifier>urn:uuid:656652b8-9af2-4e94-9d07-2dc21c05ed27</wsrm:Identifier>
      <wsrm:AcknowledgementRange Lower="1" Upper="30"></wsrm:AcknowledgementRange>
      <wsrm:Final></wsrm:Final>
      <netrm:BufferRemaining>8</netrm:BufferRemaining>
    </wsrm:SequenceAcknowledgement>
    <wsa:Action s:mustUnderstand="1">http://docs.oasis-open.org/ws-rx/wsrm/200702/CloseSequenceResponse</wsa:Action>
    <wsa:RelatesTo>urn:uuid:6ce1d4c3-e1c1-474f-a8c9-4210e37f7877</wsa:RelatesTo>
    <wsa:To s:mustUnderstand="1">http://Business456.com/clientA</wsa:To>
  </s:Header>
  <s:Body>
    <wsrm:CloseSequenceResponse>
      <wsrm:Identifier>urn:uuid:656652b8-9af2-4e94-9d07-2dc21c05ed27</wsrm:Identifier>
    </wsrm:CloseSequenceResponse>
  </s:Body>
</s:Envelope>
```

### <a name="sequence-termination"></a>シーケンスの終了

WCF は `TerminateSequence/TerminateSequenceResponse` 、ハンドシェイクを完了した後に、主にハンドシェイクを使用し `CloseSequence/CloseSequenceResponse` ます。 WCF の信頼できるメッセージの送信先は、終了を開始せず、信頼できるメッセージの送信元は、信頼できるメッセージの送信先が開始した終了をサポートしていません。 以下の制約が適用されます。

- B1301: WCF イニシエーターは、ハンドシェイクが `TerminateSequence` 正常に完了した後にのみメッセージを送信し `CloseSequence/CloseSequenceResponse` ます。

- R1302: WCF `LastMsgNumber` は、要素が `CloseSequence` 特定のシーケンスのすべてのメッセージとメッセージで一貫していることを検証 `TerminateSequence` します。 つまり、`LastMsgNumber` は、すべての `CloseSequence` メッセージおよび `TerminateSequence` メッセージに存在しないか、すべての `CloseSequence` メッセージおよび `TerminateSequence` メッセージに存在し、同一であるかのいずれかです。

- B1303: `TerminateSequence` ハンドシェイクの後、`CloseSequence/CloseSequenceResponse` メッセージを受け取ると、信頼できるメッセージの送信先が `TerminateSequenceResponse` メッセージで応答します。 信頼できるメッセージの配信元は、`TerminateSequence` メッセージを送信する前に最終受信確認を受けるため、信頼できるメッセージの送信先ではシーケンスが終了したことが確実にわかり、すぐにリソースを再要求します。

- B1304: ハンドシェイクの前にメッセージを受信すると、 `TerminateSequence` `CloseSequence/CloseSequenceResponse` WCF の信頼できるメッセージの送信先がメッセージで応答し `TerminateSequenceResponse` ます。 信頼できるメッセージの送信先でシーケンスが一貫していると判断した場合、信頼できるメッセージの送信先は、リソースを再要求する前にアプリケーションの送信先で指定された時間待機し、クライアントが最終受信確認を受け取ることができるようにします。 それ以外の場合は、信頼できるメッセージの送信先はすぐにリソースを再要求し、`Faulted` イベントを発生させて、不明なシーケンスの終了をアプリケーションの送信先に示します。

`TerminateSequence` メッセージの例を次に示します。

```xml
<s:Envelope>
  <s:Header>
    <wsa:Action s:mustUnderstand="1">http://docs.oasis-open.org/ws-rx/wsrm/200702/TerminateSequence</wsa:Action>
    <wsa:MessageID>urn:uuid:3597a398-4f3c-40f4-9335-8f1515572fdf</wsa:MessageID>
    <wsa:ReplyTo>
      <wsa:Address>http://Business456.com/clientA</wsa:Address>
    </wsa:ReplyTo>
    <wsa:To s:mustUnderstand="1">http://BusinessABC.com/serviceA</wsa:To>
  </s:Header>
  <s:Body>
    <wsrm:TerminateSequence>
      <wsrm:Identifier>urn:uuid:656652b8-9af2-4e94-9d07-2dc21c05ed27</wsrm:Identifier>
      <wsrm:LastMsgNumber>30</wsrm:LastMsgNumber>
      </wsrm:TerminateSequence>
  </s:Body>
</s:Envelope>
```

メッセージの例 `TerminateSequenceResponse` :

```xml
<s:Envelope>
  <s:Header>
    <wsrm:SequenceAcknowledgement>
      <wsrm:Identifier>urn:uuid:656652b8-9af2-4e94-9d07-2dc21c05ed27</wsrm:Identifier>
      <wsrm:AcknowledgementRange Lower="1" Upper="30"></wsrm:AcknowledgementRange>
      <wsrm:Final></wsrm:Final>
      <netrm:BufferRemaining>8</netrm:BufferRemaining>
    </wsrm:SequenceAcknowledgement>
    <wsa:Action s:mustUnderstand="1">http://docs.oasis-open.org/ws-rx/wsrm/200702/TerminateSequenceResponse</wsa:Action>
    <wsa:RelatesTo>urn:uuid:3597a398-4f3c-40f4-9335-8f1515572fdf</wsa:RelatesTo>
    <wsa:To s:mustUnderstand="1">://Business456.com/clientA</wsa:To>
  </s:Header>
  <s:Body>
    <wsrm:TerminateSequenceResponse>
      <wsrm:Identifier>urn:uuid:656652b8-9af2-4e94-9d07-2dc21c05ed27</wsrm:Identifier>
    </wsrm:TerminateSequenceResponse>
  </s:Body>
</s:Envelope>
```

### <a name="sequences"></a>シーケンス

シーケンスに適用される制約を以下に示します。

- B1401: WCF は `xs:long` 、最大値である9223372036854775807を超えるシーケンス番号を生成してアクセスします。

`Sequence` ヘッダーの例を次に示します。

```xml
<wsrm:Sequence s:mustUnderstand="1">
  <wsrm:Identifier>urn:uuid:656652b8-9af2-4e94-9d07-2dc21c05ed27</wsrm:Identifier>
  <wsrm:MessageNumber>1</wsrm:MessageNumber>
</wsrm:Sequence>
```

### <a name="request-acknowledgement"></a>受信確認の要求

WCF は、 `AckRequested` キープアライブメカニズムとしてヘッダーを使用します。

`AckRequested` ヘッダーの例を次に示します。

```xml
<wsrm:AckRequested>
  <wsrm:Identifier>urn:uuid:656652b8-9af2-4e94-9d07-2dc21c05ed27</wsrm:Identifier>
</wsrm:AckRequested>
```

### <a name="sequenceacknowledgement"></a>SequenceAcknowledgement

WCF では、WS-RELIABLEMESSAGING で提供されるシーケンス受信確認に "豚" メカニズムを使用します。 以下の制約が適用されます。

- R1601: 2 つの逆方向シーケンスが機構を使用して確立されると、 `Offer` `SequenceAcknowledgement` 目的の受信者に送信されるアプリケーションメッセージにヘッダーが含まれる場合があります。 リモートのエンドポイントは、追加された `SequenceAcknowledgement` ヘッダーにアクセスできる必要があります。

- B1602: WCF では `SequenceAcknowledgement` 、要素を含むヘッダーは生成されません `Nack` 。 WCF は、各 `Nack` 要素にシーケンス番号が含まれていることを検証しますが、それ以外の場合は `Nack` 要素と値を無視します。

 `SequenceAcknowledgement` ヘッダーの例を次に示します。

```xml
<wsrm:SequenceAcknowledgement>
  <wsrm:Identifier>urn:uuid:656652b8-9af2-4e94-9d07-2dc21c05ed27</wsrm:Identifier>
  <wsrm:AcknowledgementRange Lower="1" Upper="1"></wsrm:AcknowledgementRange>
</wsrm:SequenceAcknowledgement>
```

### <a name="ws-reliablemessaging-faults"></a>WS-ReliableMessaging エラー

次に、WS-RELIABLEMESSAGING エラーの WCF 実装に適用される制約の一覧を示します。 以下の制約が適用されます。

- B1701: WCF ではエラーは生成されません `MessageNumberRollover` 。

- B1702: SOAP 1.2 では、サービスエンドポイントが接続制限に達し、新しい接続を処理できない場合に、 `CreateSequenceRefused` 次の例に示すように、WCF によって入れ子になったエラーサブコードが生成さ `netrm:ConnectionLimitReached` れます。

```xml
<s:Envelope>
  <s:Header>
    <wsa:Action>http://docs.oasis-open.org/ws-rx/wsrm/200702/fault</wsa:Action>
  </s:Header>
  <s:Body>
    <s:Fault>
      <s:Code>
        <s:Value>s:Receiver</s:Value>
        <s:Subcode>
          <s:Value>wsrm:CreateSequenceRefused</s:Value>
          <s:Subcode>
            <s:Value>netrm:ConnectionLimitReached</s:Value>
          </s:Subcode>
        </s:Subcode>
      </s:Code>
      <s:Reason>
        <s:Text xml:lang="en">Server 'http://BusinessABC.com/serviceA' is too busy to process this request. Try again later.</s:Text>
      </s:Reason>
    </s:Fault>
  </s:Body>
</s:Envelope>
```

### <a name="ws-addressing-faults"></a>WS-Addressing エラー

Ws-reliablemessaging では WS-ADDRESSING を使用するため、WCF の Ws-reliablemessaging 実装で WS-ADDRESSING エラーが生成され、送信されることがあります。 このセクションでは、WCF が明示的に生成し、ws-reliablemessaging 層で送信する WS-ADDRESSING エラーについて説明します。

- B1801: WCF `Message Addressing Header Required` は、次のいずれかに該当する場合にエラーを生成して送信します。

  - `CreateSequence`、`CloseSequence`、または `TerminateSequence` メッセージに `MessageId` ヘッダーがない。

  - `CreateSequence`、`CloseSequence`、または `TerminateSequence` メッセージに `ReplyTo` ヘッダーがない。

  - `CreateSequenceResponse`、`CloseSequenceResponse`、または `TerminateSequenceResponse` メッセージに `RelatesTo` ヘッダーがない。

- B1802: WCF は、メッセージの `Endpoint Unavailable` アドレス指定ヘッダーの検査に基づいてシーケンスを処理できるエンドポイントをリッスンしていないことを示すために、エラーを生成して送信します `CreateSequence` 。

## <a name="protocol-composition"></a>プロトコル コンポジション

### <a name="composition-with-ws-addressing"></a>WS-Addressing によるコンポジション

WCF は、ws-addressing の2つのバージョンをサポートしています。 ws-addressing 2004/08 [WS-ADDRESSING] と W3C WS-ADDRESSING 1.0 の推奨事項 [WS-FEDERATION-CORE] と [WS-FEDERATION-SOAP]。

WS-ReliableMessaging 仕様に記載されているのは、WS-Addressing 2004/08 だけですが、使用する WS-Addressing のバージョンが制限されているわけではありません。 WCF に適用される制約の一覧を次に示します。

- R2101: WS-Addressing 2004/08 と WS-Addressing 1.0 の両方を WS-ReliableMessaging で使用できます。

- R2102: 特定の WS-ReliableMessaging シーケンス、または `Offer` 機構を使用して関連付けられた逆方向シーケンスのペアでは、同じバージョンの WS-Addressing を使用する必要があります。

### <a name="composition-with-soap"></a>SOAP によるコンポジション

WCF では、WS-TRUST Messaging で SOAP 1.1 と SOAP 1.2 の両方を使用できます。

### <a name="composition-with-ws-security-and-ws-secureconversation"></a>WS-Security と WS-SecureConversation によるコンポジション

WCF は、セキュリティで保護されたトランスポート (HTTPS)、WS-SECURITY によるコンポジション、および WS-SECURITY によるメッセージ交換を使用した構成を使用して、ws-reliablemessaging シーケンスを保護します。 WS-ReliableMessaging 1.1 プロトコル、WS-Security 1.1、および WS-Secure Conversation 1.3 プロトコルは一緒に使う必要があります。 WCF に適用される制約の一覧を次に示します。

- R2301: 個々のメッセージの整合性と機密性だけでなく、ws-reliablemessaging シーケンスの整合性を保護するために、WCF では、WS-SECURITY メッセージ交換を使用する必要があります。

- R2302:WS-ReliableMessaging シーケンスを確立する前に、WS-SecureConversation セッションを確立する必要があります。

- R2303: WS-ReliableMessaging シーケンスの有効期間が WS-SecureConversation セッションの有効期間よりも長い場合は、対応する WS-SecureConversation Renewal バインディングを使用して、WS-SecureConversation によって確立された `SecurityContextToken` を更新する必要があります。

- B2304:WS-ReliableMessaging シーケンスまたは相関する逆方向シーケンスのペアは、必ず同じ WS-SecureConversation セッションにバインドされます。

- R2305: WS-SECURITY メッセージ交換で構成されている場合、WCF レスポンダーでは、 `CreateSequence` メッセージに要素とヘッダーが含まれている必要があり `wsse:SecurityTokenReference` `wsrm:UsesSequenceSTR` ます。

 `UsesSequenceSTR` ヘッダーの例を次に示します。

```xml
<wsrm:UsesSequenceSTR></wsrm:UsesSequenceSTR>
```

### <a name="composition-with-ssltls-sessions"></a>SSL/TLS セッションによるコンポジション

WCF では、SSL/TLS セッションを使用した構成はサポートされません。

- B2401: WCF はヘッダーを生成 `wsrm:UsesSequenceSSL` しません。

- R2402: 信頼できるメッセージ発信側は、 `CreateSequence` ヘッダーを含むメッセージを `wsrm:UsesSequenceSSL` WCF レスポンダーに送信することはできません。

### <a name="composition-with-ws-policy"></a>WS-Policy によるコンポジション

WCF では、ws-policy 1.2 と WS-POLICY 1.5 の2つのバージョンがサポートされています。

## <a name="ws-reliablemessaging-ws-policy-assertion"></a>WS-ReliableMessaging の WS-Policy アサーション

WCF では、ws-reliablemessaging の ws-policy アサーションを使用して `wsrm:RMAssertion` 、エンドポイントの機能を記述します。 WCF に適用される制約の一覧を次に示します。

- B3001: WCF は、 `wsrmn:RMAssertion` Ws-policy アサーションを要素にアタッチ `wsdl:binding` します。 WCF では、要素および要素への添付ファイルの両方がサポートさ `wsdl:binding` `wsdl:port` れます。

- B3002: WCF はタグを生成しません `wsp:Optional` 。

- B3003: Ws-policy アサーションにアクセスすると `wsrmp:RMAssertion` 、WCF はタグを無視 `wsp:Optional` し、ws-federation ポリシーを必須として扱います。

- R3004: WCF は SSL/TLS セッションで構成されないため、WCF はを指定するポリシーを受け入れません `wsrmp:SequenceTransportSecurity` 。

- B3005: WCF は常に `wsrmp:DeliveryAssurance` 要素を生成します。

- B3006: WCF は常に `wsrmp:ExactlyOnce` 配信保証を指定します。

- B3007: WCF は、ws-reliablemessaging アサーションの次のプロパティを生成して読み取り、WCF でそれらを制御し `ReliableSessionBindingElement` ます。

  - `netrmp:InactivityTimeout`

  - `netrmp:AcknowledgementInterval`

  `RMAssertion` の例を次に示します。

  ```xml
  <wsrmp:RMAssertion>
    <wsp:Policy>
      <wsrmp:SequenceSTR/>
      <wsrmp:DeliveryAssurance>
        <wsp:Policy>
          <wsrmp:ExactlyOnce/>
          <wsrmp:InOrder/>
        </wsp:Policy>
      </wsrmp:DeliveryAssurance>
    </wsp:Policy>
    <netrmp:InactivityTimeout Milliseconds="600000"/>
    <netrmp:AcknowledgementInterval Milliseconds="200"/>
  </wsrmp:RMAssertion>
  ```

## <a name="flow-control-ws-reliablemessaging-extension"></a>WS-ReliableMessaging のフロー制御拡張

WCF では、ws-reliablemessaging 拡張機能を使用して、シーケンスメッセージフローに対してさらに厳密な制御を提供します。

フロー制御を有効にするには、 <xref:System.ServiceModel.Channels.ReliableSessionBindingElement.FlowControlEnabled?displayProperty=nameWithType> プロパティをに設定し `true` ます。 WCF に適用される制約の一覧を次に示します。

- B4001: 信頼できるメッセージングフロー制御が有効になっている場合、WCF は、 `netrm:BufferRemaining` 次の `SequenceAcknowledgement` 例に示すように、ヘッダーの要素拡張に要素を生成します。

  ```xml
  <wsrm:SequenceAcknowledgement>
    <wsrm:Identifier>urn:uuid:656652b8-9af2-4e94-9d07-2dc21c05ed27</wsrm:Identifier>
    <wsrm:AcknowledgementRange Upper="1" Lower="1"/>
    <netrm:BufferRemaining>8</netrm:BufferRemaining>
  </wsrm:SequenceAcknowledgement>
  ```

- B4002: 信頼できるメッセージングフロー制御が有効になっている場合でも、WCF ではヘッダーに要素は必要ありません `netrm:BufferRemaining` `SequenceAcknowledgement` 。

- B4003: WCF Reliable Messaging Destination は `netrm:BufferRemaining` 、を使用して、バッファーできる新しいメッセージの数を示します。

- B4004: 信頼できるメッセージングフロー制御を有効にすると、WCF Reliable Messaging ソースはの値を使用して `netrm:BufferRemaining` メッセージ転送を調整します。

- B4005: WCF は 0 ~ 4096 の範囲の `netrm:BufferRemaining` 整数値を生成し、0 ~ の値214748364を含む整数値を読み取り `xs:int` `maxInclusive` ます。

## <a name="message-exchange-patterns"></a>メッセージ交換パターン

このセクションでは、ws-reliablemessaging をさまざまなメッセージ交換パターンに使用する場合の WCF の動作について説明します。 各メッセージ交換パターンについて、次の 2 つの展開シナリオを考えます。

- アドレス不可能なイニシエーター : イニシエーターはファイアウォールの内側にあります。レスポンダーは HTTP 応答でのみイニシエーターにメッセージを配信できます。

- アドレス可能なイニシエーター : イニシエーターとレスポンダーの両方に HTTP 要求を送信できます。つまり、逆方向の 2 つの HTTP 接続を確立できます。

### <a name="one-way-non-addressable-initiator"></a>一方向 : アドレス不可能なイニシエーター

#### <a name="binding"></a>バインド

WCF は、1つの HTTP チャネルで1つのシーケンスを使用して、一方向のメッセージ交換パターンを提供します。 WCF は、HTTP 要求を使用して、発信側から応答側にすべてのメッセージを送信し、応答側から発信側にすべてのメッセージを送信します。

#### <a name="createsequence-exchange"></a>CreateSequence の交換

WCF イニシエーターは、 `CreateSequence` http 要求に要素のないメッセージを送信 `Offer` し、 `CreateSequenceResponse` http 応答でメッセージを受け取ります。 WCF レスポンダーは、シーケンスを作成し、 `CreateSequenceResponse` 要素のないメッセージを `Accept` HTTP 応答に送信します。

#### <a name="sequenceacknowledgement"></a>SequenceAcknowledgement

WCF イニシエーターは、メッセージメッセージとエラーメッセージを除くすべてのメッセージの応答で受信確認を処理し `CreateSequence` ます。 WCF レスポンダーは、すべてのシーケンスとメッセージに対して、HTTP 応答に対してスタンドアロンの受信確認を常に転送し `AckRequested` ます。

#### <a name="closesequence-exchange"></a>CloseSequence の交換

WCF イニシエーターは、 `CloseSequence` http 要求でメッセージを送信し、 `CreateSequenceResponse` http 応答でメッセージを要求します。 WCF レスポンダーは、 `CloseSequenceResponse` HTTP 応答でメッセージを送信します。

#### <a name="terminatesequence-exchange"></a>TerminateSequence の交換

WCF イニシエーターは、 `TerminateSequence` http 要求でメッセージを送信し、 `TerminateSequenceResponse` http 応答でメッセージを要求します。 WCF レスポンダーは、 `TerminateSequenceResponse` HTTP 応答でメッセージを送信します。

### <a name="one-way-addressable-initiator"></a>一方向 : アドレス可能なイニシエーター

#### <a name="binding"></a>バインド

WCF では、1つの受信と送信の HTTP チャネルを1つのシーケンスを使用して、一方向のメッセージ交換パターンを提供します。 WCF は、HTTP 要求を使用してすべてのメッセージを送信します。 すべての HTTP 応答に、空の本文と HTTP 202 ステータス コードが含まれます。

#### <a name="createsequence-exchange"></a>CreateSequence の交換

WCF イニシエーターは、 `CreateSequence` HTTP 要求に要素のないメッセージを送信し `Offer` ます。 WCF レスポンダーは、シーケンスを作成し、 `CreateSequenceResponse` 要素のないメッセージを `Accept` HTTP 要求に送信します。

### <a name="duplex-addressable-initiator"></a>双方向 : アドレス可能なイニシエーター

#### <a name="binding"></a>バインド

WCF は、1つの受信と1つの送信 HTTP チャネルに対して2つのシーケンスを使用して、完全に非同期の双方向メッセージ交換パターンを提供します。 このメッセージ交換パターンは、限定された方法で `Request/Reply`、`Addressable` イニシエーター メッセージ交換パターンに組み込むことができます。 WCF では、HTTP 要求を使用してすべてのメッセージを送信します。 すべての HTTP 応答に、空の本文と HTTP 202 ステータス コードが含まれます。

#### <a name="createsequence-exchange"></a>CreateSequence の交換

WCF イニシエーターは、 `CreateSequence` HTTP 要求の要素を使用してメッセージを送信し `Offer` ます。 WCF レスポンダーは、に要素があることを確認し、 `CreateSequence` `Offer` シーケンスを作成し、要素を使用してメッセージを送信し `CreateSequenceResponse` `Accept` ます。

#### <a name="sequence-lifetime"></a>シーケンスの有効期間

WCF では、2つのシーケンスが1つの完全な二重セッションとして扱われます。

1つのシーケンスに障害が発生したエラーが生成されると、WCF は、リモートエンドポイントが両方のシーケンスをフォールトすることを想定しています。 1つのシーケンスで障害が発生したエラーを読み取ると、WCF は両方のシーケンスをエラーにします。

WCF は、その送信シーケンスを終了し、受信シーケンスでメッセージを処理し続けることができます。 逆に、WCF では、受信シーケンスの終了を処理し、送信シーケンスでメッセージを送信し続けることができます。

### <a name="request-reply-and-one-way-non-addressable-initiator"></a>要求/応答および一方向のアドレス不可能なイニシエーター

#### <a name="binding"></a>バインド

WCF は、1つの HTTP チャネルで2つのシーケンスを使用して、一方向および要求/応答メッセージ交換パターンを提供します。 WCF は、HTTP 要求を使用して、発信側から応答側にすべてのメッセージを送信し、応答側から発信側にすべてのメッセージを送信します。

#### <a name="createsequence-exchange"></a>CreateSequence の交換

WCF イニシエーターは、 `CreateSequence` http 要求で要素を含むメッセージを送信 `Offer` し、 `CreateSequenceResponse` http 応答でメッセージを受け取ります。 WCF レスポンダーは、シーケンスを作成し、 `CreateSequenceResponse` HTTP 応答の要素を使用してメッセージを送信し `Accept` ます。

#### <a name="one-way-message"></a>一方向のメッセージ

一方向メッセージ交換を正常に完了するために、WCF イニシエーターは HTTP 要求で要求シーケンスメッセージを送信し、HTTP 応答でスタンドアロンメッセージを受信し `SequenceAcknowledgement` ます。 `SequenceAcknowledgement` は、送信されたメッセージの受信確認を行う必要があります。

WCF レスポンダーは、受信確認、エラー、または空の本文と HTTP 202 状態コードを持つ応答で要求に応答できます。

#### <a name="two-way-messages"></a>双方向のメッセージ

双方向メッセージ交換プロトコルを正常に完了するために、WCF イニシエーターは HTTP 要求で要求シーケンスメッセージを送信し、HTTP 応答で応答シーケンスメッセージを受信します。 応答では、送信された要求シーケンス メッセージの受信確認を行う `SequenceAcknowledgement` を送信する必要があります。

WCF レスポンダーは、アプリケーション応答、エラー、または空の本文と HTTP 202 状態コードを持つ応答で要求に応答できます。

一方向のメッセージが存在することと、アプリケーション応答のタイミングもあるため、要求シーケンス メッセージのシーケンス番号と応答メッセージのシーケンス番号には相関関係はありません。

#### <a name="retrying-replies"></a>応答の再試行

WCF は、双方向のメッセージ交換プロトコルの相関関係について、HTTP 要求/応答の相関関係に依存します。 このため、要求シーケンスメッセージが受信確認されたときに、HTTP 応答で `SequenceAcknowledgement` 、アプリケーション応答、またはエラーが発生した場合、WCF イニシエーターは要求シーケンスメッセージの再試行を停止しません。 WCF レスポンダーは、応答が関連付けられている要求の HTTP 応答で応答を再試行します。

#### <a name="closesequence-exchange"></a>CloseSequence の交換

WCF イニシエーターは、すべての一方向の要求シーケンスメッセージのすべての応答シーケンスメッセージと受信確認を受信した後、 `CloseSequence` http 要求で要求シーケンスのメッセージを送信し、 `CloseSequenceResponse` http 応答でを想定します。

要求シーケンスを終了すると、暗黙的に応答シーケンスが終了します。 つまり、WCF イニシエーターは、メッセージに応答シーケンスの最終的なを含め、 `SequenceAcknowledgement` `CloseSequence` 応答シーケンスには交換がありません `CloseSequence` 。

WCF レスポンダーは、すべての応答が確認され、HTTP 応答でメッセージを送信することを保証し `CloseSequenceResponse` ます。

#### <a name="terminatesequence-exchange"></a>TerminateSequence の交換

`CloseSequenceResponse`WCF イニシエーターは、メッセージを受信すると、 `TerminateSequence` http 要求で要求シーケンスのメッセージを送信し、 `TerminateSequenceResponse` http 応答でを想定します。

`CloseSequence` 交換と同じように、要求シーケンスを終了すると、暗黙的に応答シーケンスが終了します。 つまり、WCF イニシエーターは、メッセージに応答シーケンスの最終的なを含め、 `SequenceAcknowledgement` `TerminateSequence` 応答シーケンスには交換がありません `TerminateSequence` 。

WCF レスポンダーは、 `TerminateSequenceResponse` HTTP 応答でメッセージを送信します。

### <a name="requestreply-addressable-initiator"></a>要求/応答 : アドレス可能なイニシエーター

#### <a name="binding"></a>バインド

WCF は、1つの受信および1つの送信 HTTP チャネルに対して2つのシーケンスを使用して、要求/応答メッセージ交換パターンを提供します。 このメッセージ交換パターンは、限定された方法で `Duplex, Addressable` イニシエーター メッセージ交換パターンに組み込むことができます。 WCF は、HTTP 要求を使用してすべてのメッセージを送信します。 すべての HTTP 応答に、空の本文と HTTP 202 ステータス コードが含まれます。

#### <a name="createsequence-exchange"></a>CreateSequence の交換

WCF イニシエーターは、 `CreateSequence` HTTP 要求の要素を使用してメッセージを送信し `Offer` ます。 WCF レスポンダーは、に要素があることを確認し、 `CreateSequence` `Offer` シーケンスを作成し、要素を使用してメッセージを送信し `CreateSequenceResponse` `Accept` ます。

#### <a name="requestreply-correlation"></a>要求/応答の相関関係

次の状況は、すべての相関関係にある要求/応答で発生します。

- WCF は、すべてのアプリケーション要求メッセージに `ReplyTo` エンドポイント参照とがあることを保証し `MessageId` ます。

- WCF は、各アプリケーション要求メッセージのとしてローカルエンドポイント参照を適用し `ReplyTo` ます。 ローカル エンドポイント参照は、イニシエーターの `CreateSequence` メッセージの `ReplyTo` であり、レスポンダーの `CreateSequence` メッセージの `To` です。

- WCF では、受信要求メッセージにとが確実に送信さ `MessageId` `ReplyTo` れます。

- WCF は、 `ReplyTo` すべてのアプリケーション要求メッセージのエンドポイント参照の URI が、前に定義したローカルエンドポイント参照と一致することを保証します。

- WCF では、 `RelatesTo` `To` 要求/応答の相関関係規則に従って、すべての応答が正しいとヘッダーを持つことが保証さ `wsa` れます。
