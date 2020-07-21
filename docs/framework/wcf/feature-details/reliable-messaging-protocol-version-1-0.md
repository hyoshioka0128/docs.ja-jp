---
title: 信頼できるメッセージング プロトコル バージョン 1.0
ms.date: 03/30/2017
ms.assetid: a5509a5c-de24-4bc2-9a48-19138055dcce
ms.openlocfilehash: 8d192afcffca52136d6d71de49770c5a5ad13895
ms.sourcegitcommit: 71b8f5a2108a0f1a4ef1d8d75c5b3e129ec5ca1e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2020
ms.locfileid: "84202303"
---
# <a name="reliable-messaging-protocol-version-10"></a>信頼できるメッセージング プロトコル バージョン 1.0

このトピックでは、HTTP トランスポートを使用した相互運用に必要な WS-RELIABLEMESSAGING 2005 (バージョン 1.0) プロトコルの Windows Communication Foundation (WCF) 実装の詳細について説明します。 WCF は、このトピックで説明する制約と説明を使用して、WS-RELIABLEMESSAGING 仕様に従います。 Ws-reliablemessaging バージョン1.0 プロトコルは、WinFX 以降で実装されることに注意してください。

WS-TRUST Messaging 2005 年2月プロトコルは、によって WCF に実装され <xref:System.ServiceModel.Channels.ReliableSessionBindingElement> ます。

便宜上、ここでは次のロールを使用します。

- イニシエーター : WS-Reliable メッセージ シーケンスの作成を開始するクライアント

- レスポンダー : イニシエーターの要求を受け取るサービス

このドキュメントでは、次の表に示すプレフィックスと名前空間を使用します。

|Prefix|名前空間|
|------------|---------------|
|wsrm|`http://schemas.xmlsoap.org/ws/2005/02/rm`|
|netrm|`http://schemas.microsoft.com/ws/2006/05/rm`|
|s|`http://www.w3.org/2003/05/soap-envelope`|
|wsa|`http://schemas.xmlsoap.org/ws/2005/08/addressing`|
|wsse|`http://docs.oasis-open.org/wss/2004/01/oasis-200401-wssecurity-secext-1.0.xsd`|

## <a name="messaging"></a>メッセージング

### <a name="sequence-establishment-messages"></a>シーケンス確立メッセージ

WCF `CreateSequence` では、メッセージとメッセージを実装して、 `CreateSequenceResponse` 信頼性の高いメッセージシーケンスを確立します。 以下の制約が適用されます。

- B1101: WCF イニシエーターは、メッセージ内にオプションの Expires 要素を生成しません `CreateSequence` 。また、メッセージに要素が含まれている場合は、 `CreateSequence` `Offer` 要素内の省略可能な要素を生成 `Expires` しません `Offer` 。

- B1102: メッセージにアクセスするときに、 `CreateSequence` WCF は `Responder` 両方の `Expires` 要素を送受信しますが、これらの要素の値は使用しません。

WS-ReliableMessaging では、セッションを形成する、相関する 2 つの逆方向シーケンスを確立するために、`Offer` 機構が導入されています。

- R1103 : `CreateSequence` に `Offer` 要素が含まれている場合、Reliable メッセージング レスポンダーは、シーケンスを受け入れ、`CreateSequenceResponse` 要素を含む `wsrm:Accept` で応答して、相関する 2 つの逆方向シーケンスを形成するか、`CreateSequence` 要求を拒否する必要があります。

- R1104 : 逆方向シーケンスでフローする `SequenceAcknowledgement` およびアプリケーション メッセージは、`ReplyTo` の `CreateSequence` エンドポイント参照に送信される必要があります。

- R1105 : `AcksTo` の `ReplyTo` エンドポイント参照と `CreateSequence` エンドポイント参照には、オクテット単位で一致するアドレス値が必要です。

  WCF レスポンダーは、 `AcksTo` `ReplyTo` シーケンスを作成する前に、と EPR の URI 部分が同一であることを確認します。

- R1106 : `AcksTo` の `ReplyTo` および `CreateSequence` の各エンドポイント参照は、参照パラメーターの同じセットを持つ必要があります。

  WCF では、との [参照パラメーター] が同じであることを前提としていますが、 `AcksTo` `ReplyTo` 受信確認 `CreateSequence` `ReplyTo` と逆方向シーケンスメッセージのエンドポイント参照から [参照パラメーター] を使用していることを前提としています。

- R1107 : `Offer` 機構を使用して 2 つの逆方向シーケンスを確立した場合、逆方向シーケンスでフローする `SequenceAcknowledgement` およびアプリケーション メッセージは、`ReplyTo` の `CreateSequence` エンドポイント参照に送信される必要があります。

- R1108 : Offer 機構を使用して 2 つの逆方向シーケンスを確立した場合、`[address]` の `wsrm:AcksTo` 要素の `wsrm:Accept` エンドポイント参照子要素の `CreateSequenceResponse` プロパティは、`CreateSequence` の送信先 URI とバイト単位で一致する必要があります。

- R1109 : `Offer` 機構を使用して 2 つの逆方向シーケンスを確立した場合、イニシエーターによって送信されたメッセージとレスポンダーによるメッセージの受信確認は、同じエンドポイント参照に送信される必要があります。

  WCF では、WS-RELIABLEMESSAGING を使用して、イニシエーターとレスポンダーの間に信頼できるセッションを確立します。 WCF の WS-RELIABLEMESSAGING 実装は、一方向、要求/応答、および全二重のメッセージングパターンに対して信頼できるセッションを提供します。 `Offer`の ws-reliablemessaging 機構を `CreateSequence` / `CreateSequenceResponse` 使用すると、関連する2つの逆方向シーケンスを確立し、すべてのメッセージエンドポイントに適したセッションプロトコルを提供できます。 WCF では、セッション整合性に対するエンドツーエンドの保護を含むこのようなセッションに対してセキュリティ保証が提供されるため、同じパーティを対象としたメッセージが同じ送信先に到着することを確認することが実用的です。 また、これにより、アプリケーション メッセージにシーケンス受信確認を抱き合わせることができます。 したがって、制約 R1104、R1105、および R1108 は WCF に適用されます。

`CreateSequence` メッセージの例を次に示します。

```xml
<s:Envelope>
  <s:Header>
    <a:Action s:mustUnderstand="1">
      http://schemas.xmlsoap.org/ws/2005/02/rm/CreateSequence
    </a:Action>
    <a:ReplyTo>
      <a:Address>
         http://Business456.com/clientA
      </a:Address>
    </a:ReplyTo>
    <a:MessageID>
      urn:uuid:addabbbf-60cb-44d3-8c5b-9e0841629a36
    </a:MessageID>
    <a:To s:mustUnderstand="1">
      http://Business456.com/clientA
    </a:To>
  </s:Header>
  <s:Body>
    <wsrm:CreateSequence>
      <wsrm:AcksTo>
       <wsa:Address>
         http://Business456.com/clientA
       </wsa:Address>
     </wsrm:AcksTo>
     <wsrm:Offer>
      <wsrm:Identifier>
        urn:uuid:0afb8d36-bf26-4776-b8cf-8c91fddb5496
      </wsrm:Identifier>
     </wsrm:Offer>
   </wsrm:CreateSequence>
  </s:Body>
</s:Envelope>
```

 `CreateSequenceResponse` メッセージの例を次に示します。

```xml
<s:Envelope>
  <s:Header>
    <a:Action s:mustUnderstand="1">
      http://schemas.xmlsoap.org/ws/2005/02/rm/CreateSequenceResponse
    </a:Action>
    <a:RelatesTo>
      urn:uuid:addabbbf-60cb-44d3-8c5b-9e0841629a36
    </a:RelatesTo>
    <a:To s:mustUnderstand="1">
      http://Business456.com/clientA
    </a:To>
  </s:Header>
  <s:Body>
   <wsrm:CreateSequenceResponse>
    <Identifier>
     urn:uuid:eea0a36c-b38a-43e8-8c76-2fabe2d76386
    </Identifier>
    <Accept>
    <AcksTo>
      <a:Address>
        http://BusinessABC.com/serviceA
      </a:Address>
    </AcksTo>
    </Accept>
   </wsrm:CreateSequenceResponse>
  </s:Body>
</s:Envelope>
```

### <a name="sequence"></a>シーケンス

シーケンスに適用される制約を以下に示します。

- B1201: WCF は `xs:long` 、最大値である9223372036854775807を超えるシーケンス番号を生成してアクセスします。

- B1202: WCF は、アクション URI がである空の最後のメッセージを常に生成 `http://schemas.xmlsoap.org/ws/2005/02/rm/LastMessage` します。

- B1203: WCF は `LastMessage` 、アクション URI がでない限り、要素を含むシーケンスヘッダーを含むメッセージを受信して配信し `http://schemas.xmlsoap.org/ws/2005/02/rm/LastMessage` ます。

シーケンス ヘッダーのサンプル

```xml
<wsrm:Sequence>
  <wsrm:Identifier>
    urn:uuid:addabbbf-60cb-44d3-8c5b-9e0841629a36
  </wsrm:Identifier>
  <wsrm:MessageNumber>
    10
  </wsrm:MessageNumber>
  <wsrm:LastMessage/>
 </wsrm:Sequence>
```

### <a name="ackrequested-header"></a>AckRequested ヘッダー

WCF は `AckRequested` 、キープアライブメカニズムとしてヘッダーを使用します。 WCF では、省略可能な要素は生成されません `MessageNumber` 。 要素を含むヘッダーを含むメッセージを受信すると `AckRequested` `MessageNumber` 、 `MessageNumber` 次の例に示すように、WCF は要素の値を無視します。

```xml
<wsrm:AckRequested>
  <wsrm:Identifier>
    urn:uuid:addabbbf-60cb-44d3-8c5b-9e0841629a36
  </wsrm:Identifier>
</wsrm:AckRequested>
```

### <a name="sequenceacknowledgement-header"></a>SequenceAcknowledgement ヘッダー

WCF では、WS-RELIABLEMESSAGING で提供されるシーケンス受信確認に豚メカニズムを使用します。

- R1401 : `Offer` 機構を使用して 2 つの逆方向シーケンスを確立した場合、目的の受信者に送信されるアプリケーション メッセージに、`SequenceAcknowledgement` ヘッダーを含めることができます。

- B1402: WCF は、シーケンスメッセージを受信する前に受信確認を生成する必要があります (たとえば、メッセージを満たすには、 `AckRequested` `SequenceAcknowledgement` 次の例に示すように、wcf は範囲0-0 を含むヘッダーを生成します。

  ```xml
  <wsrm:SequenceAcknowledgement>
    <wsrm:Identifier>
      urn:uuid:addabbbf-60cb-44d3-8c5b-9e0841629a36
    </wsrm:Identifier>
    <wsrm:AcknowledgementRange Upper="0" Lower="0"/>
  </wsrm:SequenceAcknowledgement>
  ```

- B1403: WCF は `SequenceAcknowledgement` 要素を含むヘッダーを生成 `Nack` しませんが、要素をサポート `Nack` します。

### <a name="ws-reliablemessaging-faults"></a>WS-ReliableMessaging エラー

次に、WS-RELIABLEMESSAGING エラーの WCF 実装に適用される制約の一覧を示します。

- B1501: WCF ではエラーは生成されません `MessageNumberRollover` 。

- B1502: WCF エンドポイントは `CreateSequenceRefused` 、仕様で説明されているようにエラーを生成する場合があります。

- B1503: サービスエンドポイントが接続制限に達し、新しい接続を処理できない場合、WCF は `CreateSequenceRefused` 次の `netrm:ConnectionLimitReached` 例に示すように、追加のエラーサブコードを生成します。

  ```xml
  <s:Envelope>
    <s:Header>
      <wsa:Action>
        http://schemas.xmlsoap.org/ws/2005/08/addressing/fault
      </wsa:Action>
    </s:Header>
    <s:Body>
      <s:Fault>
        <s:Code>
          <s:Value>
            s:Receiver
          </s:Value>
          <s:Subcode>
            <s:Value>
              wsrm:CreateSequenceRefused
            </s:Value>
            <s:Subcode>
              <s:Value>
                netrm:ConnectionLimitReached
              </s:Value>
            </s:Subcode>
          </s:Subcode>
        </s:Code>
        <s:Reason>
          <s:Text xml:lang="en">
            [Reason]
          </s:Text>
        </s:Reason>
      </s:Fault>
    </s:Body>
  </s:Envelope>
  ```

### <a name="ws-addressing-faults"></a>WS-Addressing エラー

WS-ATOMICTRANSACTION では ws-addressing を使用するため、WCF の WS-RELIABLEMESSAGING 実装で WS-ADDRESSING エラーが発生する可能性があります。 ここでは、WCF が WS-TRUST メッセージングレイヤーで明示的に生成する WS-ADDRESSING エラーについて説明します。

- B1601: WCF では、次のいずれかに該当する場合に、必要なエラーメッセージのアドレス指定ヘッダーが生成されます。

  - メッセージに `Sequence` ヘッダーと `Action` ヘッダーがない。

  - `CreateSequence` メッセージに `MessageId` ヘッダーがない。

  - `CreateSequence` メッセージに `ReplyTo` ヘッダーがない。

- B1602: WCF は、ヘッダーが欠落していて、 `Sequence` `Action` ws-reliablemessaging 仕様で認識されていないヘッダーを持つメッセージに対して、応答でサポートされていないエラーアクションを生成します。

- B1603: WCF は、 `CreateSequence` メッセージのアドレス指定ヘッダーの検査に基づいて、エンドポイントがシーケンスを処理しないことを示すために、使用できない障害エンドポイントを生成します。

## <a name="protocol-composition"></a>プロトコル コンポジション

### <a name="composition-with-ws-addressing"></a>WS-Addressing によるコンポジション

WCF は、ws-addressing の2つのバージョンをサポートしています。 ws-addressing 2004/08 [WS-ADDRESSING] と W3C WS-ADDRESSING 1.0 の推奨事項 [WS-FEDERATION-CORE] と [WS-FEDERATION-SOAP]。

WS-ReliableMessaging 仕様に記載されているのは、WS-Addressing 2004/08 だけですが、使用する WS-Addressing のバージョンが制限されているわけではありません。 WCF に適用される制約の一覧を次に示します。

- R2101 :WS-Addressing 2004/08 と WS-Addressing 1.0 の両方を WS-ReliableMessaging で使用できます。

- R2102: ws-addressing の1つのバージョンは、特定の WS-RELIABLEMESSAGING シーケンス、またはメカニズムを使用して関連付けられた逆方向シーケンスのペア全体で使用する必要があり `wsrm:Offer` ます。

### <a name="composition-with-soap"></a>SOAP によるコンポジション

WCF では、WS-TRUST Messaging で SOAP 1.1 と SOAP 1.2 の両方を使用できます。

### <a name="composition-with-ws-security-and-ws-secureconversation"></a>WS-Security と WS-SecureConversation によるコンポジション

WCF は、セキュリティで保護されたトランスポート (HTTPS)、WS-SECURITY によるコンポジション、および WS-SECURITY によるメッセージ交換を使用した構成を使用して、WS-RELIABLEMESSAGING シーケンスを保護します。 WCF に適用される制約の一覧を次に示します。

- R2301: 個々のメッセージの整合性と機密性だけでなく、WS-RELIABLEMESSAGING シーケンスの整合性を保護するために、WCF では、WS-SECURITY メッセージ交換を使用する必要があります。

- R2302 :WS-ReliableMessaging シーケンスを確立する前に、WS-SecureConversation セッションを確立する必要があります。

- R2303 : WS-ReliableMessaging シーケンスの有効期間が WS-SecureConversation セッションの有効期間よりも長い場合は、対応する WS-SecureConversation Renewal バインディングを使用して、WS-SecureConversation によって確立された `SecurityContextToken` を更新する必要があります。

- B2304 :WS-ReliableMessaging シーケンスまたは相関する逆方向シーケンスのペアは、必ず同じ WS-SecureConversation セッションにバインドされます。

  WCF ソースによって、 `wsse:SecurityTokenReference` メッセージの要素拡張セクションに要素が生成され `CreateSequence` ます。

- R2305: セキュリティで保護されたメッセージ交換で構成される場合、メッセージには `CreateSequence` 要素が含まれている必要があり `wsse:SecurityTokenReference` ます。

## <a name="ws-reliable-messaging-ws-policy-assertion"></a>WS-ReliableMessaging の WS-Policy アサーション

WCF では、WS-RELIABLEMESSAGING を使用して、 `wsrm:RMAssertion` エンドポイントの機能を記述します。 WCF に適用される制約の一覧を次に示します。

- B3001: WCF は、 `wsrm:RMAssertion` Ws-policy アサーションを要素にアタッチ `wsdl:binding` します。 WCF では、要素および要素への添付ファイルの両方がサポートさ `wsdl:binding` `wsdl:port` れます。

- B3002: WCF では、WS-RELIABLEMESSAGING アサーションの次のオプションプロパティがサポートされており、WCF でそれらを制御でき `ReliableMessagingBindingElement` ます。

  - `wsrm:InactivityTimeout`

  - `wsrm:AcknowledgementInterval`

  以下に例を示します。

  ```xml
  <wsrm:RMAssertion>
    <wsrm:InactivityTimeout Milliseconds="600000" />
    <wsrm:AcknowledgementInterval Milliseconds="200" />
  </wsrm:RMAssertion>
  ```

## <a name="flow-control-ws-reliable-messaging-extension"></a>WS-ReliableMessaging のフロー制御拡張

WCF では、WS-RELIABLEMESSAGING の拡張機能を使用して、シーケンスメッセージフローに対してさらに厳密な制御を提供します。

フロー制御を有効にするには、 <xref:System.ServiceModel.Channels.ReliableSessionBindingElement.FlowControlEnabled?displayProperty=nameWithType> プロパティをに設定し `true` ます。 WCF に適用される制約の一覧を次に示します。

- B4001: 信頼できるメッセージングフロー制御を有効にすると、WCF は `netrm:BufferRemaining` ヘッダーの要素拡張に要素を生成し `SequenceAcknowledgement` ます。

- B4002: 信頼できるメッセージングフロー制御を有効にすると、次の `netrm:BufferRemaining` `SequenceAcknowledgement` 例に示すように、WCF では要素がヘッダーに存在する必要がありません。

  ```xml
  <wsrm:SequenceAcknowledgement>
    <wsrm:Identifier>
      http://fabrikam123.com/abc
    </wsrm:Identifier>
    <wsrm:AcknowledgementRange Upper="1" Lower="1"/>
    <netrm:BufferRemaining>
      8
    </netrm:BufferRemaining>
  </wsrm:SequenceAcknowledgement>
  ```

- B4003: WCF では `netrm:BufferRemaining` 、を使用して、信頼できるメッセージの送信先がバッファーできる新しいメッセージの数を示します。

- B4004: WCF Reliable Messaging サービスは、信頼できるメッセージングの送信先アプリケーションがメッセージを迅速に受信できない場合に送信されるメッセージの数を調整します。 信頼できるメッセージングの送信先がメッセージをバッファーに保持する場合、要素の値が 0 になります。

- B4005: WCF は 0 ~ 4096 の範囲の `netrm:BufferRemaining` 整数値を生成し、0 ~ の値214748364を含む整数値を読み取り `xs:int` `maxInclusive` ます。

## <a name="message-exchange-patterns"></a>メッセージ交換パターン

このセクションでは、WS-RELIABLEMESSAGING がさまざまなメッセージ交換パターンに使用される場合の WCF の動作について説明します。 各メッセージ交換パターンについて、次の 2 つの展開シナリオを考えます。

- アドレス不可能なイニシエーター : イニシエーターはファイアウォールの内側にあります。レスポンダーは HTTP 応答でのみイニシエーターにメッセージを配信できます。

- アドレス可能なイニシエーター : イニシエーターとレスポンダーの両方に HTTP 要求を送信できます。つまり、逆方向の 2 つの HTTP 接続を確立できます。

### <a name="one-way-non-addressable-initiator"></a>一方向 : アドレス不可能なイニシエーター

#### <a name="binding"></a>バインド

WCF は、1つの HTTP チャネルで1つのシーケンスを使用して、一方向のメッセージ交換パターンを提供します。 WCF は、HTTP 要求を使用して RMS から RMD にすべてのメッセージを転送し、HTTP 応答を使用して、RMD から RMS にすべてのメッセージを送信します。

#### <a name="createsequence-exchange"></a>CreateSequence の交換

WCF イニシエーターは、オファーのないメッセージを生成し `CreateSequence` ます。 WCF レスポンダーは、 `CreateSequence` シーケンスを作成する前に、にオファーがないことを確認します。 WCF レスポンダーは、 `CreateSequence` メッセージと共に要求に応答し `CreateSequenceResponse` ます。

#### <a name="sequenceacknowledgement"></a>SequenceAcknowledgement

WCF イニシエーターは、メッセージメッセージとエラーメッセージを除くすべてのメッセージの応答で受信確認を処理し `CreateSequence` ます。 WCF レスポンダーは、シーケンスとメッセージの両方に対する応答で、スタンドアロンの受信確認を常に生成し `AckRequested` ます。

#### <a name="terminatesequence-message"></a>TerminateSequence メッセージ

WCF は、 `TerminateSequence` 一方向の操作として処理します。つまり、http 応答には、空の本文と http 202 ステータスコードが含まれます。

### <a name="one-way-addressable-initiator"></a>一方向 : アドレス可能なイニシエーター

#### <a name="binding"></a>バインド

WCF は、受信および送信 Http チャネルで1つのシーケンスを使用して、一方向のメッセージ交換パターンを提供します。 WCF は、HTTP 要求を使用してすべてのメッセージを送信します。 すべての HTTP 応答に、空の本文と HTTP 202 ステータス コードが含まれます。

#### <a name="createsequence-exchange"></a>CreateSequence の交換

WCF イニシエーターは、オファーのないメッセージを生成し `CreateSequence` ます。 WCF レスポンダーは、 `CreateSequence` シーケンスを作成する前に、にオファーがないことを確認します。 WCF レスポンダーは、 `CreateSequenceResponse` エンドポイント参照でアドレス指定された HTTP 要求でメッセージを送信し `ReplyTo` ます。

### <a name="duplex-addressable-initiator"></a>双方向 : アドレス可能なイニシエーター

#### <a name="binding"></a>バインド

WCF は、受信と送信の HTTP チャネルで2つのシーケンスを使用して、完全に非同期の双方向メッセージ交換パターンを提供します。 WCF は、HTTP 要求を使用してすべてのメッセージを送信します。 すべての HTTP 応答に、空の本文と HTTP 202 ステータス コードが含まれます。

#### <a name="createsequence-exchange"></a>CreateSequence の交換

WCF イニシエーターは、オファーを使用してメッセージを生成し `CreateSequence` ます。 WCF レスポンダーは、 `CreateSequence` シーケンスを作成する前に、にオファーがあることを確認します。 WCF は、 `CreateSequenceResponse` `CreateSequence` のエンドポイント参照にアドレス指定された HTTP 要求でを送信し `ReplyTo` ます。

#### <a name="sequence-lifetime"></a>シーケンスの有効期間

WCF では、2つのシーケンスが1つの完全な二重セッションとして扱われます。

1つのシーケンスに障害が発生したエラーが生成されると、WCF は、リモートエンドポイントが両方のシーケンスをフォールトすることを想定しています。 1つのシーケンスで障害が発生したエラーを読み取ると、WCF は両方のシーケンスをエラーにします。

WCF は、その送信シーケンスを終了し、受信シーケンスでメッセージを処理し続けることができます。 逆に、WCF では、受信シーケンスの終了を処理し、送信シーケンスでメッセージを送信し続けることができます。

### <a name="request-reply-non-addressable-initiator"></a>要求/応答 : アドレス不可能なイニシエーター

#### <a name="binding"></a>バインド

WCF は、1つの HTTP チャネルで2つのシーケンスを使用して、一方向および要求/応答メッセージ交換パターンを提供します。 WCF は、HTTP 要求を使用して要求シーケンスのメッセージを送信し、HTTP 応答を使用して応答シーケンスのメッセージを送信します。

#### <a name="createsequence-exchange"></a>CreateSequence の交換

WCF イニシエーターは、オファーを使用してメッセージを生成し `CreateSequence` ます。 WCF レスポンダーは、 `CreateSequence` シーケンスを作成する前に、にオファーがあることを確認します。 WCF レスポンダーは、 `CreateSequence` メッセージと共に要求に応答し `CreateSequenceResponse` ます。

#### <a name="one-way-message"></a>一方向のメッセージ

一方向メッセージ交換プロトコルを正常に完了するために、WCF イニシエーターは HTTP 要求で要求シーケンスメッセージを送信し、HTTP 応答でスタンドアロンメッセージを受信し `SequenceAcknowledgement` ます。 `SequenceAcknowledgement` は、送信されたメッセージの受信確認を行う必要があります。

WCF レスポンダーは、受信確認、エラー、または空の本文と HTTP 202 ステータスコードを持つ応答を使用して、要求に応答できます。

#### <a name="two-way-messages"></a>双方向のメッセージ

双方向メッセージ交換プロトコルを正常に完了するために、WCF イニシエーターは HTTP 要求で要求シーケンスメッセージを送信し、HTTP 応答で応答シーケンスメッセージを受信します。 応答では、送信された要求シーケンス メッセージの受信確認を行う `SequenceAcknowledgement` を送信する必要があります。

WCF レスポンダーは、アプリケーション応答、エラー、または空の本文と HTTP 202 ステータスコードを含む応答を使用して、要求に応答できます。

一方向のメッセージが存在することと、アプリケーション応答のタイミングもあるため、要求シーケンス メッセージのシーケンス番号と応答メッセージのシーケンス番号には相関関係はありません。

#### <a name="retrying-replies"></a>応答の再試行

WCF は、双方向のメッセージ交換プロトコルの相関関係について、HTTP 要求/応答の相関関係に依存します。 このため、要求シーケンスメッセージが受信確認された場合でも、HTTP 応答が受信確認、ユーザーメッセージ、またはエラーを受信する場合、WCF イニシエーターは要求シーケンスメッセージの再試行を停止しません。 WCF レスポンダーは、応答が関連付けられている要求の HTTP 要求レッグで応答を再試行します。

#### <a name="lastmessage-exchange"></a>LastMessage の交換

WCF イニシエーターは、HTTP 要求レッグで空の本文の最後のメッセージを生成して送信します。 WCF には応答が必要ですが、実際の応答メッセージは無視されます。 WCF レスポンダーは、応答シーケンスの空の最後のメッセージと共に、要求シーケンスの空のメッセージに応答します。

WCF レスポンダーが、アクション URI がではない最後のメッセージを受信すると `http://schemas.xmlsoap.org/ws/2005/02/rm/LastMessage` 、wcf は最後のメッセージを返します。 双方向メッセージ交換プロトコルの場合、最後のメッセージでアプリケーション メッセージが送信されます。一方向メッセージ交換プロトコルの場合、最後のメッセージは空です。

WCF レスポンダーは、応答シーケンスの空の最後のメッセージに対する受信確認を必要としません。

#### <a name="terminatesequence-exchange"></a>TerminateSequence の交換

すべての要求が有効な応答を受信すると、WCF イニシエーターは、HTTP 要求レッグで要求シーケンスのメッセージを生成して送信し `TerminateSequence` ます。 WCF には応答が必要ですが、実際の応答メッセージは無視されます。 WCF レスポンダーは、 `TerminateSequence` 応答シーケンスのメッセージと共に、要求シーケンスのメッセージに応答し `TerminateSequence` ます。

通常のシャットダウン シーケンスでは、両方の `TerminateSequence` メッセージで完全な `SequenceAcknowledgement` を送信します。

### <a name="requestreply-addressable-initiator"></a>要求/応答 : アドレス可能なイニシエーター

#### <a name="binding"></a>バインド

WCF は、受信と送信の HTTP チャネルで2つのシーケンスを使用して、要求/応答メッセージ交換パターンを提供します。 WCF は、HTTP 要求を使用してすべてのメッセージを送信します。 すべての HTTP 応答に、空の本文と HTTP 202 ステータス コードが含まれます。

#### <a name="createsequence-exchange"></a>CreateSequence の交換

WCF イニシエーターは、オファーを使用してメッセージを生成し `CreateSequence` ます。 WCF レスポンダーは、 `CreateSequence` シーケンスを作成する前に、にオファーがあることを確認します。 WCF は、 `CreateSequenceResponse` `CreateSequence` のエンドポイント参照にアドレス指定された HTTP 要求でを送信し `ReplyTo` ます。

#### <a name="requestreply-correlation"></a>要求/応答の相関関係

WCF イニシエーターは、すべてのアプリケーション要求メッセージに `MessageId` およびエンドポイント参照を保持することを保証し `ReplyTo` ます。 WCF イニシエーターは、 `CreateSequence` `ReplyTo` 各アプリケーション要求メッセージに対してメッセージのエンドポイント参照を適用します。 WCF レスポンダーでは、受信要求メッセージにとがあることが必要です `MessageId` `ReplyTo` 。 WCF レスポンダーは、とすべてのアプリケーション要求メッセージのエンドポイント参照の URI が同一であることを保証し `CreateSequence` ます。
