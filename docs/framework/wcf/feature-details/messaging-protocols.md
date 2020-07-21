---
title: メッセージング プロトコル
ms.date: 03/30/2017
ms.assetid: 5b20bca7-87b3-4c8f-811b-f215b5987104
ms.openlocfilehash: 814347c77b54c4450aabf0a4f3966df223360663
ms.sourcegitcommit: 927b7ea6b2ea5a440c8f23e3e66503152eb85591
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/16/2020
ms.locfileid: "81463832"
---
# <a name="messaging-protocols"></a>メッセージング プロトコル

Windows 通信基盤 (WCF) チャネル スタックでは、内部メッセージ表現をそのワイヤ形式に変換し、特定のトランスポートを使用して送信するエンコード チャネルとトランスポート チャネルを使用します。 Web サービスの相互運用性を確保するために、最も一般的に使用されるトランスポートは HTTP です。また、Web サービスが使用する最も一般的なエンコーディングは、XML ベースの SOAP 1.1、SOAP 1.2、および MTOM (Message Transmission Optimization Mechanism) です。

このトピックでは、 で<xref:System.ServiceModel.Channels.HttpTransportBindingElement>使用される次のプロトコルの WCF 実装の詳細について説明します。

仕様/ドキュメント:

- [HTTP 1.1](https://www.ietf.org/rfc/rfc2616.txt)
- [SOAP 1.1 HTTP バインディング](https://www.w3.org/TR/2000/NOTE-SOAP-20000508)、セクション 7
- [SOAP 1.2 HTTP バインディング](https://www.w3.org/TR/soap12-part2)セクション 7

このトピックでは、次のプロトコルと<xref:System.ServiceModel.Channels.TextMessageEncodingBindingElement><xref:System.ServiceModel.Channels.MtomMessageEncodingBindingElement>使用する WCF 実装の詳細について説明します。

仕様/ドキュメント:

- [XML](https://www.w3.org/TR/REC-xml)
- [SOAP 1.1](https://www.w3.org/TR/2000/NOTE-SOAP-20000508/)
- [SOAP 1.2 コア](https://www.w3.org/TR/soap12-part1/)
- [WS-Addressing 2004/08](https://www.w3.org/Submission/2004/SUBM-ws-addressing-20040810/)
- [W3C Web Services Addressing 1.0 - コア](https://www.w3.org/TR/2006/REC-ws-addr-core-20060509)
- [W3C Web Services Addressing 1.0 - SOAP バインディング](https://www.w3.org/TR/2006/REC-ws-addr-soap-20060509)
- [W3C Web サービス アドレス指定 1.0 - WSDL バインディング](https://www.w3.org/TR/2006/CR-ws-addr-wsdl-20060529/)
- [W3C Web Services Addressing 1.0 - メタデータ](https://www.w3.org/TR/ws-addr-metadata/)
- [WSDL SOAP1.1 バインディング](https://www.w3.org/TR/wsdl/)
- [WSDL SOAP1.2 バインディング](https://www.w3.org/Submission/wsdl11soap12/)

このトピックでは、使用する次のプロトコルの WCF<xref:System.ServiceModel.Channels.MtomMessageEncodingBindingElement>実装の詳細について説明します。

仕様/ドキュメント:

- [XOP](https://www.w3.org/TR/xop10/)
- [MTOM および SOAP 1.2 バインディング](https://www.w3.org/TR/soap12-mtom/)
- [MTOM SOAP 1.1 バインディング](https://www.w3.org/Submission/soap11mtom10/)
- [MTOM WS-Policy アサーション](https://www.w3.org/Submission/2006/SUBM-WS-MTOMPolicy-20061101/)

このトピックでは、次の XML 名前空間と関連付けられたプレフィックスが使用されます。

| Prefix | 名前空間 URI (Uniform Resource Identifier) |
|------------|---------------------------------------------------|
| s11 | `http://schemas.xmlsoap.org/soap/envelope` |
| s12 |`http://www.w3.org/2003/05/soap-envelope` |
| wsa |`http://www.w3.org/2004/08/addressing` |
| wsam |`http://www.w3.org/2007/05/addressing/metadata` |
| wsap |`http://schemas.xmlsoap.org/ws/2004/09/policy/addressing` |
| wsa10 |`http://www.w3.org/2005/08/addressing` |
| wsaw10 |`http://www.w3.org/2006/05/addressing/wsdl` |
| xop |`http://www.w3.org/2004/08/xop/include` |
| xmime |`http://www.w3.org/2004/06/xmlmime`<br /><br /> `http://www.w3.org/2005/05/xmlmime` |
| Dp |`http://schemas.microsoft.com/net/2006/06/duplex` |

## <a name="soap-11-and-soap-12"></a>SOAP 1.1 と SOAP 1.2

### <a name="envelope-and-processing-model"></a>エンベロープと処理モデル
WCF は、基本プロファイル 1.1 (BP11) と基本プロファイル 1.0 (SSBP10) に続く SOAP 1.1 エンベロープ処理を実装します。 SOAP 1.2 エンベロープの処理は、SOAP12-Part1 に従って実装されます。

このセクションでは、BP11 と SOAP12-Part1 に関して、WCF によって取得される特定の実装の選択肢について説明します。

#### <a name="mandatory-header-processing"></a>必須のヘッダー処理
WCF は、SOAP 1.1`mustUnderstand`および SOAP 1.2 仕様で示されているヘッダーを処理するための規則に従い、次のバリエーションがあります。

WCF チャネル スタックに入るメッセージは、関連付けられたバインド要素によって構成された個々 のチャネルによって処理されます。たとえば、テキスト メッセージ エンコード、セキュリティ、信頼できるメッセージング、トランザクションなどです。 各チャネルは、関連付けられた名前空間からヘッダーを認識し、認識済みとしてマークします。 メッセージがディスパッチャーに入ると、操作フォーマッタは対応するメッセージ コントラクトと操作コントラクトで想定されたヘッダーを読み取り、認識済みとしてマークします。 次に、ディスパッチャーは、`mustUnderstand` としてマークされているにもかかわらず、認識されていないヘッダーが残っていないかどうかを検証し、例外をスローします。 受信者を対象とする `mustUnderstand` ヘッダーが含まれたメッセージが、受信者のアプリケーション コードで処理されることはありません。

このようなレイヤー化された処理により、SOAP ノードのインフラストラクチャ レイヤーとアプリケーション レイヤーを次のように分離することが可能になります。

- B1111: メッセージが WCF インフラストラクチャ チャネル スタックによって処理された後、アプリケーションによって処理される前に、認識されないヘッダーが検出されます。

     `mustUnderstand` ヘッダーの値は、SOAP 1.1 と SOAP 1.2 で異なります。 Basic Profile 1.1 では、SOAP 1.1 メッセージの `mustUnderstand` の値が 0 または 1 である必要があります。 SOAP 1.2 では、値として 0、1、`false`、および `true` を使用できますが、`xs:boolean` 値の正規表現 (`false`、`true`) を出力することをお勧めします。

- B1112: WCF`mustUnderstand`は SOAP 1.1 と SOAP 1.2 の両方のバージョンの SOAP エンベロープの値 0 と 1 を出力します。 WCF は、ヘッダーの値空間`xs:boolean`全体を`mustUnderstand`受け入れます (0, 1, `false`、 ) `true`

#### <a name="soap-faults"></a>SOAP エラー
WCF 固有の SOAP エラーの実装の一覧を次に示します。

- B2121: WCF は、次の SOAP 1.1 障害コードを返します: `s11:mustUnderstand`、、`s11:Client`および`s11:Server`.

- B2122: WCF は、次の SOAP 1.2 障害コードを返します: `s12:MustUnderstand`、、`s12:Sender`および`s12:Receiver`.

### <a name="http-binding"></a>HTTP バインディング

#### <a name="soap-11-http-binding"></a>SOAP 1.1 HTTP バインディング
WCF は、基本プロファイル 1.1 仕様セクション 3.4 に続いて SOAP1.1 HTTP バインディングを実装し、次の説明を示します。

- B2211: WCF サービスは、HTTP POST 要求のリダイレクトを実装しません。

- B2212: WCF クライアントは、HTTP クッキーを 3.4.8 に準拠してサポートしています。

#### <a name="soap-12-http-binding"></a>SOAP 1.2 HTTP バインディング
WCF は、SOAP 1.2 パート 2 (SOAP12Part2) 仕様で説明されているように、SOAP 1.2 HTTP バインディングを実装し、次の説明を使用します。

SOAP 1.2 では、`application/soap+xml` メディア タイプの省略可能なアクション パラメーターが導入されました。 このパラメーターは、WS-Addressing を使用していない場合に、SOAP メッセージの本文を解析する必要なく、メッセージ ディスパッチを最適化する際に役立ちます。

- R2221 : `application/soap+xml` のアクション パラメーターが SOAP 1.2 要求に含まれている場合、対応する WSDL バインディング内の `soapAction` 要素の `wsoap12:operation` 属性と一致する必要があります。

- R2222 : WS-Addressing 2004/08 または WS-Addressing 1.0 を使用しているときに、`application/soap+xml` のアクション パラメーターが SOAP 1.2 メッセージに含まれている場合、`wsa:Action` と一致する必要があります。

WS-Addressing が無効になっているときに、受信要求にアクション パラメーターが含まれていない場合、メッセージの `Action` は指定されていないものと見なされます。

## <a name="ws-addressing"></a>WS-Addressing
WCF では、WS アドレスの 3 つのバージョンを実装します。

- WS-Addressing 2004/08

- W3C Web Services Addressing 1.0 コア (ADDR10-CORE) - SOAP バインディング (ADDR10-SOAP)

- WS-Addressing 1.0 - メタデータ

### <a name="endpoint-references"></a>エンドポイント参照
WCF が実装する WS-Addressing のすべてのバージョンでは、エンドポイントを記述するためにエンドポイント参照を使用します。

#### <a name="endpoint-references-and-ws-addressing-versions"></a>エンドポイント参照と WS-Addressing のバージョン
WCF では、WS アドレス指定、特に`EndpointReference`要素と`W3C.WsAddressing.EndpointReferenceType`クラス (WS-ReliableMessaging、WS-SecureConversation、WS-Trust など) を使用するインフラストラクチャ プロトコルが多数実装されています。 WCF では、他のインフラストラクチャ プロトコルとの WS-Addressing のいずれかのバージョンの使用をサポートしています。 WCF エンドポイントは、エンドポイントごとに 1 つのバージョンの WS-Addressing をサポートします。

R3111 の場合、WCF`EndpointReference`エンドポイントと交換されるメッセージで使用される要素または型の名前空間は、このエンドポイントによって実装される WS-Addressing のバージョンと一致する必要があります。

たとえば、WCF エンドポイントが WS-ReliableMessaging を実装している`AcksTo`場合、内部`CreateSequenceResponse`のこのようなエンドポイントによって返されるヘッダーは、要素がこのエンドポイントに`EncodingBinding`指定されている WS-Addressing バージョンを使用します。

#### <a name="endpoint-references-and-metadata"></a>エンドポイント参照とメタデータ
多くのシナリオでは、指定されたエンドポイントのメタデータまたはメタデータへの参照を伝達する必要があります。

B3121: WCF では、値または参照によってエンドポイント参照のメタデータを含める WS-MetadataExchange (MEX) 仕様セクション 6 で説明されているメカニズムを採用します。

WCF サービスが、 の`http://sts.fabrikam123.com`トークン発行者によって発行されたセキュリティ アサーション マークアップ言語 (SAML) トークンを使用して認証を必要とするシナリオを考えてみます。 WCF エンドポイントは、トークン発行者を指す`sp:IssuedToken`入れ子になった`sp:Issuer`アサーションを使用して、この認証要件を記述します。 `sp:Issuer` アサーションにアクセスするクライアント アプリケーションは、トークン発行者のエンドポイントとの通信方法を知る必要があります。 クライアントは、トークン発行者に関するメタデータを知る必要があります。 MEX で定義されているエンドポイント参照メタデータ拡張機能を使用して、WCF はトークン発行者のメタデータへの参照を提供します。

```xml
<sp:IssuedToken>
  <sp:Issuer>
    <wsa10:Address>
      http://sts.fabrikam123.com
    </wsa10:Address>
    <wsa10:Metadata>
      <mex:Metadata>
        <mex:MetadataSection>
          <mex:MetadataReference>
            <wsa10:Address>
              http://sts.fabrikam123.com/mex
            </wsa10:Address>
          </mex:MetadataReference>
        </mex:MetadataSection>
      </mex:Metadata>
    </wsa10:Metadata>
  </sp:Issuer>
</sp:IssuedToken>
```

### <a name="message-addressing-headers"></a>メッセージのアドレス指定ヘッダー

#### <a name="message-headers"></a>メッセージ ヘッダー
どちらの WS-Addressing バージョンでも`wsa:To`、WCF では、仕様、、、、、`wsa:ReplyTo``wsa:Action`および`wsa:MessageID`に規定されているとおり`wsa:RelatesTo`に、次のメッセージ ヘッダーが使用されます。

B3211: すべての WS-アドレス指定バージョンでは、WCF は、使用されますが、WS-Addressing メッセージ ヘッダー`wsa:FaultTo`と`wsa:From`.

WCF アプリケーションと対話するアプリケーションは、これらのメッセージ ヘッダーを追加でき、WCF は、それに応じてそれらを処理します。

#### <a name="reference-parameters-and-properties"></a>参照パラメーターと参照プロパティ

WCF は、エンドポイント参照パラメーターと参照プロパティの処理をそれぞれの仕様に従って実装します。

B3221: WS-Addressing 2004/08 を使用するように構成されている場合、WCF エンドポイントは、参照プロパティと参照パラメーターの処理を区別しません。

### <a name="message-exchange-patterns"></a>メッセージ交換パターン
Web サービス操作の呼び出しに関連するメッセージのシーケンスは、*メッセージ交換パターン*と呼ばれます。 WCF は、一方向、要求/応答、および双方向のメッセージ交換パターンをサポートします。 このセクションでは、使用するメッセージ交換パターンによって異なるメッセージ処理に関する WS-Addressing の要件について説明します。

このセクション全体を通して、リクエスターが最初のメッセージを送信し、レスポンダーが最初のメッセージを受信します。

#### <a name="one-way-message"></a>一方向のメッセージ
一方向パターンに従うように指定された`Action`メッセージをサポートするように WCF エンドポイントが構成されている場合、WCF エンドポイントは次の動作と要件に従います。 特に指定がない限り、WCF でサポートされている WS-Addressing の両方のバージョンに対して、動作と規則が適用されます。

- R3311 : リクエスターは、`wsa:To`、`wsa:Action`、およびエンドポイント参照によって指定されたすべての参照パラメーターのヘッダーを含める必要があります。 WS-Addressing 2004/08 を使用し、エンドポイント参照によって参照プロパティが指定されている場合、対応するヘッダーもメッセージに追加する必要があります。

- B3312 : リクエスターは、`MessageID`、`ReplyTo`、および `FaultTo` の各ヘッダーを含めることができます。 受信側のインフラストラクチャはこれらのヘッダーを無視し、ヘッダーはアプリケーションに渡されます。

- R3313 : HTTP を使用し、HTTP 応答レッグで送信するメッセージがない場合、レスポンダーは空の本文と HTTP 202 ステータス コードを含む HTTP 応答を送信する必要があります。

     HTTP トランスポートを使用しており、操作コントラクトで一方向のメッセージが宣言されている場合でも、HTTP 応答を使用してインフラストラクチャ メッセージを送信できます。たとえば、信頼できるメッセージングでは、HTTP 応答で `SequenceAcknowledgement` メッセージを送信できます。

- B3314: WCF レスポンダーは、一方向メッセージに応答してエラー メッセージを送信しません。

#### <a name="request-reply"></a>要求/応答
WCF エンドポイントが、要求/応答パターンに従うように`Action`指定されたメッセージ用に構成されている場合、WCF エンドポイントは、次の動作と要件に従います。 特に指定しない限り、WCF でサポートされている WS-Addressing の両方のバージョンに対して、動作と規則が適用されます。

- R3321: 要求者は、`wsa:To``wsa:Action`エンドポイント参照で指定されたすべての`wsa:MessageID`参照パラメーターまたは参照プロパティ (またはその両方) の要求 、、、およびヘッダーに含める必要があります。

- R3322 : WS-Addressing 2004/08 を使用する場合、`ReplyTo` も要求に含める必要があります。

- R3323: WS-Addressing 1.0 が`ReplyTo`使用され、要求に存在しない場合は、[address] プロパティが次の値に`http://www.w3.org/2005/08/addressing/anonymous`等しい既定のエンドポイント参照が使用されます。

- R3324: 要求側は、`wsa:To`応答`wsa:Action`メッセージに`wsa:RelatesTo`、 、 、 、 およびヘッダーを含める必要があります`ReplyTo`。

### <a name="web-services-addressing-faults"></a>Web Services Addressing エラー
R3411: WCF は、WS アドレス 2004/08 で定義された次のエラーを生成します。

| コード | 原因 |
|----------|-----------|
| `wsa:DestinationUnreachable` | このチャネル用に確立された応答アドレスとは異なる `ReplyTo` を使用してメッセージが到着しました。To ヘッダーに指定されたアドレスをリッスンしているエンドポイントはありません。 |
| `wsa:ActionNotSupported` | `Action` ヘッダーに指定されたアクションは、エンドポイントに関連付けられたインフラストラクチャ チャネルまたはディスパッチャーによって認識されません。 |

R3412: WCF は WS-Addressing 1.0 で定義された次のエラーを生成します。

| コード | 原因 |
|----------|-----------|
| `wsa10:InvalidAddressingHeader` | 複製`wsa:To` `wsa:ReplyTo`、 `wsa:From` `wsa:MessageID`、または 。 `wsa:RelatesTo`同じ`RelationshipType`. |
| `wsa10:MessageAddressingHeaderRequired` | 必須の Addressing ヘッダーがありません。 |
| `wsa10:DestinationUnreachable` | このチャネル用に確立された応答アドレスとは異なる `ReplyTo` を使用してメッセージが到着しました。 To ヘッダーに指定されたアドレスをリッスンしているエンドポイントはありません。 |
| `wsa10:ActionNotSupported` | `Action` ヘッダーに指定されたアクションは、エンドポイントに関連付けられたインフラストラクチャ チャネルまたはディスパッチャーによって認識されません。 |
| `wsa10:EndpointUnavailable` | RM チャネルは、`CreateSequence` メッセージのアドレス指定ヘッダーの検査に基づいて、エンドポイントでシーケンスが処理されないことを示すために、このエラーを返しました。 |

上記の 2 つの表に示すコードは、SOAP 1.1 の `FaultCode`、および SOAP 1.2 の `SubCode` (Code=Sender) に対応付けられています。

### <a name="wsdl-11-binding-and-ws-policy-assertions"></a>WSDL 1.1 バインディングと WS-Policy アサーション

#### <a name="indicating-use-of-ws-addressing"></a>WS-Addressing の使用の提示
WCF では、ポリシー アサーションを使用して、特定の WS-Addressing バージョンのエンドポイント サポートを示します。

次のポリシー アサーションには、エンドポイント ポリシー サブジェクト [WS-PA] が含まれており、そのエンドポイントで送受信されるメッセージでは WS-Addressing 2004/08 を使用する必要があることを示しています。

```xml
<wsap:UsingAddressing />
```

このポリシー アサーションは、WS-Addressing 2004/08 仕様を補うものです。

次のポリシー アサーションは、送受信されるメッセージでは WS-Addressing 1.0 を使用する必要があることを示しています。

```xml
<wsam:Addressing/>
```

次のポリシー アサーションには、エンドポイント ポリシー サブジェクト [WS-PA] が含まれており、そのエンドポイントで送受信されるメッセージでは WS-Addressing 2004/08 を使用する必要があることを示しています。

```xml
<wsaw10:UsingAddressing />
```

`wsaw10:UsingAddressing` 要素は、WS-Addressing-WSDL から借用したものです。この要素は、この仕様のセクション 3.1.2 に従って、WS-Policy のコンテキストで使用されます。

Addressing を使用しても、WSDL 1.1、SOAP 1.1、および SOAP 1.2 HTTP バインディングのセマンティクスが変更されるわけではありません。 たとえば、Addressing と WSDL SOAP 1.x HTTP バインディングを使用するエンドポイントに送信する要求に対して応答が求められている場合、この応答は HTTP 応答を使用して送信する必要があります。

HTTP 応答を使用して送信された応答の場合、WS-AM アサーションは次のようになります。

```xml
<wsam:AnonymousResponses/>
```

完全なポリシー アサーションは次のようになる場合があります。

```xml
<wsam:Addressing>
    <wsp:Policy>
        <wsam:AnonymousResponses />
    </wsp:Policy>
</wsam:Addressing>
```

ただし、リクエスターとレスポンダー間で 2 つの独立した逆方向の HTTP 接続を確立することによってメリットのあるメッセージ交換パターンがあります。たとえば、レスポンダーによって送信される要求されていない一方向のメッセージなどです。

WCF には、2 つの基になるトランスポート チャネルが複合二重チャネルを形成できる機能が用意されており、一方のチャネルは入力メッセージに使用され、もう 1 つは出力メッセージに使用されます。 HTTP トランスポートの場合、複合二重によって 2 つの逆方向の HTTP 接続が実現します。 一方の接続はリクエスターがレスポンダーにメッセージを送信するために使用し、もう一方はレスポンダーがリクエスターにメッセージを返すために使用します。

個別の HTTP 要求を使用して送信された応答の場合、WS-AM アサーションは次のようになります。

```xml
<wsam:NonAnonymousResponses/>
```

完全なポリシー アサーションは次のようになる場合があります。

```xml
<wsam:Addressing>
    <wsp:Policy>
        <wsam:NonAnonymousResponses />
    </wsp:Policy>
</wsam:Addressing>
```

WSDL 1.1 SOAP 1.x HTTP バインディングを使用するエンドポイントで、エンドポイント ポリシー サブジェクト [WS-PA] を含む次のアサーションを使用する場合、リクエスターからレスポンダーおよびレスポンダーからリクエスターへのメッセージ フローにそれぞれ別の逆方向の HTTP 接続を使用する必要があります。

```xml
<cdp:CompositeDuplex/>
```

上記のステートメントにより、要求メッセージの `wsa:ReplyTo` ヘッダーに関する以下の要件が発生します。

- R3514: エンドポイントに送信される要求メッセージは、WSDL 1.1 SOAP `http://www.w3.org/2005/08/addressing/anonymous` 1.x HTTP バインディングを使用し、アタッチされた`wsap10:UsingAddressing`または`wsap:UsingAddressing`アサーションを組み合わせたポリシー代替手段を持つ`cdp:CompositeDuplex`場合に、`ReplyTo``[address]`プロパティーが等しくないヘッダーを持つ必要があります。

- R3515: エンドポイントに送信`ReplyTo`される要求メッセージは`[address]`、WSDL 1.1 `http://www.w3.org/2005/08/addressing/anonymous`SOAP 1.x `ReplyTo` HTTP バインディングを使用し、`wsap10:UsingAddressing`アサーションとアサーションがアタッチされていないポリシー代替手段を持つ場合、プロパティが に等しい`cdp:CompositeDuplex`か、ヘッダーをまったく持たない必要があります。

- R3516: エンドポイントに送信される要求メッセージは、`ReplyTo`エンドポイントが`[address]`WSDL 1.1 SOAP 1.x HTTP バインディングを使用し、アサーションとアサーションが`http://www.w3.org/2005/08/addressing/anonymous``wsap:UsingAddressing``cdp:CompositeDuplex`アタッチされていないポリシー代替手段を持つ場合に等しいプロパティーを持つヘッダーを持つ必要があります。

WS-Addressing の WSDL 仕様では、`<wsaw:Anonymous/>` ヘッダーの要件を示す 3 つのテキスト値 (required、optional、および prohibited) を持つ `wsa:ReplyTo` 要素を導入することにより、同様のプロトコル バインディングを記述することを試みています (セクション 3.2)。 残念ながら、このような要素の定義では、要素をアサーションとして使用する代替手段の共通部分をサポートするために、ドメイン固有の拡張を必要とするため、特に WS-Policy のコンテキストではアサーションとして使用することはできません。 また、このような要素の定義は、ネットワーク上のエンドポイントの動作に相反する `ReplyTo` ヘッダーの値を示すため、HTTP トランスポートに固有のものになります。

#### <a name="action-definition"></a>アクション定義
WS-Addressing 2004/08 では、`wsa:Action` 要素の `wsdl:portType/wsdl:operation/[wsdl:input | wsdl:output | wsdl:fault]` 属性が定義されています。 WS-Addressing 1.0 WSDL バインディング (WS-ADDR10-WSDL) では、同様の属性として `wsaw10:Action` が定義されています。

この 2 つの属性の唯一の違いは、既定の Action パターンのセマンティクスです。これは、WS-ADDR のセクション 3.3.2 および WS-ADDR10-WSDL のセクション 4.4.4 にそれぞれ記載されています。

同じ`portType`(または WCF の用語ではコントラクト) を共有するが、WS-Addressing の異なるバージョンを使用する 2 つのエンドポイントを持つことは合理的です。 しかし、Action は `portType` によって定義され、`portType` を実装するエンドポイント間で変更できないことを考えると、両方の既定のアクション パターンをサポートすることは不可能になります。

この論争を解決するために、WCF は属性の単一`Action`のバージョンをサポートします。

B3521: WCF`wsaw10:Action`では、WS-ADDR10-WSDL で定義されている要素の`wsdl:portType/wsdl:operation/[wsdl:input | wsdl:output | wsdl:fault]`属性`Action`を使用して、エンドポイントで使用される WS-Addressing バージョンに関係なく、対応するメッセージの URI を決定します。

#### <a name="use-endpoint-reference-inside-wsdl-port"></a>WSDL ポート内でのエンドポイント参照の使用
WS-ADDR10-WSDL のセクション 4.1 では、`wsdl:port` 要素を拡張して、WS-Addressing の観点でエンドポイントを記述する `<wsa10:EndpointReference…/>` 子要素を含めています。 WCF では、WS-Addressing 2004/08 でこのユーティリティ`<wsa:EndpointReference…/>`が拡張され、 の`wsdl:port`子要素として表示されます。

- R3531 : エンドポイントが `<wsaw10:UsingAddressing/>` ポリシー アサーションに関連付けられたポリシー代替手段を持つ場合、対応する `wsdl:port` 要素に `<wsa10:EndpointReference …/>` 子要素を含めることができます。

- R3532: 子`wsdl:port``<wsa10:EndpointReference …/>`要素が含まれている場合、`wsa10:EndpointReference/wsa10:Address`子要素`@address`の値は兄弟`wsdl:port`/`wsdl:location`要素の属性の値と一致する必要があります。

- R3533 : エンドポイントが `<wsap:UsingAddressing/>` ポリシー アサーションに関連付けられたポリシー代替手段を持つ場合、対応する `wsdl:port` 要素に `<wsa:EndpointReference …/>` 子要素を含めることができます。

- R3534: 子`wsdl:port``<wsa:EndpointReference …/>`要素が含まれている場合、`wsa:EndpointReference/wsa:Address`子要素`@address`の値は兄弟`wsdl:port`/`wsdl:location`要素の属性の値と一致する必要があります。

### <a name="composition-with-ws-security"></a>WS-Security によるコンポジション
WS-ADDR および WS-ADDR10 のセキュリティに関する考慮事項のセクションに従って、メッセージ本文と共にすべてのアドレス指定メッセージ ヘッダーに署名し、これらをバインドすることをお勧めします。

メッセージの整合性を保護するために WS-Security を使用する場合は、メッセージの本文と共に、WS-Addressing メッセージ ヘッダーと、参照パラメーターまたは参照プロパティ (または両方) によって生成されたヘッダーに署名する必要があります。

### <a name="examples"></a>例

#### <a name="one-way-message"></a>一方向のメッセージ
このシナリオでは、送信者は一方向のメッセージを受信者に送信します。 SOAP 1.2、HTTP 1.1、および W3C WS-Addressing 1.0 を使用します。

要求メッセージの構造 : メッセージ ヘッダーには、`wsa10:To` 要素と `wsa10:Action` 要素が含まれます。 メッセージ本文には、アプリケーション名前空間の特定の `<app:Ping>` 要素が含まれます。

HTTP ヘッダー: POST の宛先が要素の`wsa10:To`URI と一致します。

Content-Type ヘッダーには、SOAP 1.2 で必要とされる値 `application/soap+xml` が含まれます。 また、`charset` パラメーターと `action` パラメーターも含まれます。 Content-Type ヘッダーの `action` パラメーターは、`wsa10:Action` メッセージ ヘッダーの値に一致します。

```
POST http://fabrikam123.com/Service HTTP/1.1
Content-Type: application/soap+xml; charset=utf-8;  
              action="http://fabrikam123.com/Service/OneWay"
Host: 131.107.72.15
Content-Length: 1501
Expect: 100-continue
Proxy-Connection: Keep-Alive
<s12:Envelope>
  <s12:Header>
    <wsa10:To s12:mustUnderstand="1">
        http://fabrikam123.com/Service
    </wsa10:To>
    <wsa10:Action s12:mustUnderstand="1">
        http://fabrikam123.com/Service/OneWay
    </wsa10:Action>
  </s12:Header>
  <s12:Body>
    <Ping xmlns="http://fabrikam123.com/Service/">
      <Text>Hello World</Text>
    </Ping>
  </s12:Body>
</s12:Envelope>
```

受信側は、空の HTTP 応答と 202 ステータスで応答します。 HTTP 応答の一例を次に示します。

```
HTTP/1.1 202 Accepted
Date: Fri, 15 Jul 2005 08:56:07 GMT
Server: Microsoft-IIS/6.0
MicrosoftOfficeWebServer: 5.0_Pub
X-Powered-By: ASP.NET
X-AspNet-Version: 2.0.50215
Cache-Control: private
Content-Length: 0
```

## <a name="soap-message-transmission-optimization-mechanism"></a>SOAP Message Transmission Optimization Mechanism
このセクションでは、HTTP SOAP MTOM の WCF 実装の詳細について説明します。 MTOM テクノロジは、従来のテキスト/XML エンコーディングまたは WCF バイナリ エンコーディングと同じクラスの SOAP メッセージ エンコーディング メカニズムです。 MTOM には、次のような機能があります。

- XOP によって記述された XML エンコーディングおよびパッケージング機構。XOP は、Base64 で個別のバイナリ部分にエンコードされたバイナリ データを含む XML 情報項目を最適化します。

- XML Infoset と XOP パッケージの各バイナリ部分を個別の MIME パートにシリアル化する、XOP パッケージの MIME カプセル化。

- SOAP 1.x エンベロープに適用される MIME XOP エンコーディング。

- HTTP トランスポート バインディング。

WCF では、非 HTTP トランスポートで MTOM を使用できます。 しかし、ここでは HTTP に焦点を合わせます。

MTOM 形式では、MTOM 自体、XOP、および MIME に適用されるさまざまな仕様を利用します。 この仕様セットのモジュール性により、形式と処理のセマンティクスの要件を正確に再構築することが若干難しくなります。 このセクションでは、MTOM HTTP バインディングの形式と処理の要件について説明します。

### <a name="mtom-message-encoding"></a>MTOM メッセージ エンコーディング

#### <a name="generating-mtom-messages"></a>MTOM メッセージの生成
XOP のセクション 3.1 には、Base64 値を抽象的に定義された XOP パッケージに格納する要素情報項目を使用して、XML をエンコーディングするプロセスが記載されています。

次の一連の手順は、MTOM 固有のエンコーディング プロセスを示しています。

1. エンコードされる SOAP エンベロープ`[namespace name]`に、 および の`http://www.w3.org/2004/08/xop/include`を持つ要素情報項目`[local name]`が`Include`含まれないようにします。

2. 空の MIME パッケージを作成します。

3. 元の XML Infoset 内で、最適化する要素情報項目を特定します。 最適化する項目の場合、エレメント情報項目`[children]`を構成する文字は正規形式である`xs:base64Binary`必要があります (XSD-2、 3.2.16 base64Binary を参照) および非空白の内容の前後に空白文字を含めることはできません。

4. 元の SOAP エンベロープのコピーである XOP SOAP エンベロープを作成します。ただし、このコピーには、前の手順で特定した各要素情報項目の子が含まれます。これらの子は、以下の手順に従って構築された `xop:Include` 要素情報項目に置き換えられています。

    1. 置換対象の文字を Base64 でエンコードされたデータとして処理することにより、バイナリ データに変換します。

    2. R3133 および R3134 の各要件を満たす Content-ID ヘッダーの一意の値を生成します。

    3. バイナリ値を使用して、Content-Transfer-Encoding MIME ヘッダーを生成します。

    4. 最適化する要素情報項目 (新しく挿入する `xop:Include` 要素情報項目の [parent]) に、`xmime:contentType` 属性情報項目が含まれている場合、`xmime:contentType` 属性の値を使用して Content-Type MIME ヘッダーを生成します。

    5. Base64 として処理された置換対象文字からデコードされたバイナリ データ、Content-ID ヘッダー (手順 4b. で生成)、Content- Transfer-Encoding ヘッダー (手順 4c. で生成)、および Content-Type ヘッダー (手順 4d. で生成した場合) で構成されたコンテンツを含む、新しいバイナリ MIME パートを生成します。

    6. 値 cid: uri を持つ `href` 要素に `xop:Include` 属性を追加します。uri は、手順 4b. で生成した Content-ID ヘッダーの値から派生したものです。 囲む "\<" と " >文字を削除し、残りの文字列を URL`cid:`エスケープして、プレフィックスを追加します。 RFC1738 と RFC2396 に従って、次の最小限の文字セットをエスケープする必要があります。 その他の文字もエスケープすることができます。

        ```
        Hexadecimal 00-1F , 7F, 20, "<" | ">" | "#" | "%" | <">
        "{" | "}" | "|" | "\" | "^" | "[" | "]" | "`" | "~" | "^"
        ```

5. 手順 4. の XOP SOAP エンベロープを含むルート MIME パートを作成します。

6. HTTP Content-Type ヘッダーなどの HTTP ヘッダーを書き込みます。

7. MIME パッケージを書き込みます。

#### <a name="processing-mtom-messages"></a>MTOM メッセージの処理
MTOM メッセージの処理は、前述の「MTOM メッセージの生成」で説明したプロセスと正反対のプロセスになります。

1. ルート MIME パートに Content-Type `application/xop+xml` が含まれていることを確認します。

2. パッケージのルート MIME パートを XML ドキュメントとして解析して、SOAP エンベロープを作成します。 文字エンコーディングは、ルート MIME パートの Content-Type の `charset` パラメーターによって決まります。

3. 作成した SOAP エンベロープ内の各要素情報項目について、以下の処理を行います。これらの要素情報項目には、[children] プロパティの唯一のメンバーとして、`xop:Include` 要素情報項目が含まれています。

    1. プレフィックス `cid:` を削除し、`@href` 要素の `xop:Include` 属性の値に含まれるすべての URI エスケープ シーケンスのエスケープを解除します (RFC 2396)。 結果文字列を ",\<">" で囲みます。

    2. Content-ID ヘッダーの値が手順 3a. で取得した文字列に一致する MIME パートを検索します。

    3. 各項目の `xop:Include` プロパティに出現する `children` 要素情報項目を、手順 3b. で特定した MIME パートのエンティティ本体の正規 Base64 エンコーディング (XSD-2 セクション 3.2.16 の base64Binary を参照) を表す文字情報項目に置き換えます (`xop:Include` 要素情報項目をパッケージ パーツから再構築したデータに効率的に置き換えます)。

#### <a name="http-content-type-header"></a>HTTP Content-Type ヘッダー
次に示す WCF の明確化の一覧は、SOAP 1.x MTOM エンコード メッセージの HTTP コンテンツの種類ヘッダーの形式の MTOM 仕様自体に記載され、MTOM と RFC 2387 から派生します。

- R4131 : HTTP Content-Type ヘッダーには、multipart/related (大文字と小文字は区別されません) とそのパラメーターの値が必要です。 パラメーター名では、大文字と小文字は区別されません。 パラメーターの順序は重要ではありません。

- MIME メッセージの Content-Type ヘッダーのすべての Backus-Naur Form (BNF) については、RFC 2045 のセクション 5.1 に記載されています。

- R4132 : HTTP Content-Type ヘッダーには、二重引用符で囲まれた値 `application/xop+xml` が指定された型パラメーターが必要です。

RFC 2387 では二重引用符を使用する要件は明示的ではありませんが、テキストでは、マルチパート/関連メディアタイプのパラメータのすべてが、ほとんどの場合、" "\@や "/" などの予約文字を含んでいるため、二重引用符が必要であることを確認します。

- R4133 : HTTP Content-Type ヘッダーには、start パラメーターを含める必要があります。このパラメーターには、SOAP 1.x エンベロープを含む MIME パートの Content-ID ヘッダーの値を二重引用符で囲んで指定します。 start パラメーターを省略する場合は、最初の MIME パートに SOAP 1.x エンベロープを含める必要があります。

- R4134 : SOAP 1.1 MTOM でエンコードされたメッセージの HTTP Content-Type ヘッダーには、start-info パラメーターを含める必要があります。このパラメーターには、値 text/xml を二重引用符で囲んで指定します。

- R4135 : SOAP 1.2 MTOM でエンコードされたメッセージの HTTP Content-Type ヘッダーには、start-info パラメーターを含める必要があります。このパラメーターには、値 `application/soap+xml` を二重引用符で囲んで指定します。

- R4136 : SOAP 1.x MTOM でエンコードされたメッセージの HTTP Content-Type ヘッダーには、boundary パラメーターを含める必要があります。このパラメーターには、RFC 2046 のセクション 5.1.1 で定義された MIME 境界の BNF に一致する (二重引用符で囲まれた) 値を指定します。

    ```
    boundary := 0*69<bchars> bcharsnospace
    bchars := bcharsnospace / " "
    bcharsnospace :=    DIGIT / ALPHA / "'" / "(" / ")" / "+"
                        / "_" / "," / "-" / "." / "/" / ":" / "=" / "?"
    ```

     例 :

     正

    ```
    Content-Type: multipart/related; type="application/xop+xml";start=" <part0@tempuri.org>";boundary="uuid:0ca0e16e-feb1-426c-97d8-c4508ada5e82+id=1";start-info="text/xml"
    ```

     正

    ```
    Content-Type: Multipart/Related; type="application/xop+xml";start-info="text/xml";boundary="uuid:0ca0e16e-feb1-426c-97d8-c4508ada5e82+id=1"
    ```

     誤

    ```
    Content-Type: Multipart/Related; type=application/xop+xml;start=" <part0@tempuri.org>";start-info="text/xml";boundary="uuid:0ca0e16e-feb1-426c-97d8-c4508ada5e82+id=1"
    ```

#### <a name="infoset-mime-part"></a>Infoset MIME パート
SOAP 1.x エンベロープは、XOP MIME パッケージのルート部分としてカプセル化され、多くの場合、`infoset` パートと呼ばれます。

- R4141 : SOAP 1.x エンベロープは、XOP MIME パッケージのルート部分としてカプセル化する必要があります。これは `infoset` パートと呼ばれ、HTTP Content-Type から参照されます。

- R4142 : SOAP `Infoset` パートには、`Content-ID`、`Content-Transfer-Encoding`、および `Content-Type` の各 MIME ヘッダーを含める必要があります。

Content-ID ヘッダーの形式は、RFC 2045 で次のように定義されています。

```
"Content-ID" ":" msg-id
```

ここで、`msg-id` は、RFC 2822 で次のように定義されています (RFC 2045 で参照されている RFC 822 は、RFC 2822 に置き換えられています)。

```
msg-id    =       [CFWS] "<" id-left "@" id-right ">" [CFWS]
```

電子メール アドレスは、事実上 ""\<と ">" で囲まれています。 `[CFWS]` プレフィックスとサフィックスは、コメントを伝達するために RFC 2822 で追加されたものですが、相互運用性を維持する場合は、使用しないことをお勧めします。

R4143 : Infoset MIME パートの Content-ID ヘッダーの値は、RFC 2822 の `msg-id` の定義内容から `[CFWS]` プレフィックスとサフィックスの部分を省略した形式に従う必要があります。

MIME 実装の多くは、""\<と > " " で囲まれた値を電子メール`absoluteURI`アドレスにする\<要件を緩和し、電子メール アドレスに加えて "" ""、">" で囲んで使用しました。 このバージョンの WCF では、フォームのコンテンツ ID MIME ヘッダーの値を使用します。

```
Content-ID: <http://tempuri.org/0>
```

R4144 : MTOM プロセッサは、次の厳密でない `msg-id` に一致する Content-ID ヘッダーの値を受け入れる必要があります。

```
msg-id-relaxed =     [CFWS] "<" (absoluteURI | mail-address) ">" [CFWS]
mail-address   =     id-left "@" id-right
```

MIME (RFC 2045) では、MIME パートのコンテンツのエンコーディングを伝達する Content-Transfer-Encoding ヘッダーを使用できます。 Content-Transfer-Encoding に定義されている既定値は 7 ビットですが、これはほとんどの SOAP メッセージに適していません。そのため、Content-Transfer-Encoding ヘッダーの相互運用性を高めるために、以下を行う必要があります。

- R4145 : SOAP Infoset パートに、Content-Transfer-Encoding ヘッダーを含める必要があります。

- R4146 : SOAP エンベロープの文字エンコーディングが UTF-8 の場合、Content-Transfer-Encoding ヘッダーの値は 8 ビットであることが必要です。

- R4147 : SOAP エンベロープの文字エンコーディングが UTF-16 の場合、Content-Transfer-Encoding ヘッダーの値はバイナリであることが必要です。

- 以下の要件は、XOP のセクション 5 に基づいています。

- R4148: SOAP1.1 インフォセットパーツには、メディアタイプのアプリケーション/xop+xml とパラメータタイプ="text/xml"と文字セットを持つコンテンツタイプヘッダーが含まれている必要があります

    ```
    Content-Type: application/xop+xml;
                  charset=utf-8;type="text/xml"
    ```

- R4149: SOAP 1.2 インフォセットパーツには、メディアタイプ`application/xop+xml`とパラメータタイプ=" と .`application/soap+xml` `charset`

    ```
    Content-Type: application/xop+xml;
                  charset=utf-8;type="application/soap+xml"
    ```

     XOP では、`charset` の `application/xop+xml` パラメーターは省略可能と定義されていますが、`charset` メディア タイプの `text/xml` パラメーターについては、BP 1.1 の要件と同様の相互運用性が必要とされます。

- R41410 : `type` パラメーターと `charset` パラメーターは、SOAP 1.x Infoset パートの Content-Type ヘッダーに含まれている必要があります。

#### <a name="wcf-endpoint-support-for-mtom"></a>WCF エンドポイントによる MTOM のサポート
MTOM の目的は、SOAP メッセージをエンコードして、Base64 でエンコードされたデータを最適化することです。 制約は次のとおりです。

- R4151 : Base64 でエンコードされたデータを含むすべての要素情報項目を最適化できます。

- B4152: WCF は、Base64 エンコードされたデータを含み、長さが 1024 バイトを超える要素情報項目を最適化します。

MTOM を使用するように構成された WCF エンドポイントは、常に MTOM エンコードされたメッセージを送信します。 必要な条件を満たすパートがない場合でも、メッセージは MTOM でエンコードされます (SOAP エンベロープを含む単一の MIME パートを持つ MIME パッケージとしてシリアル化されます)。

### <a name="ws-policy-assertion-for-mtom"></a>MTOM の WS-Policy アサーション
WCF では、次のポリシー アサーションを使用して、エンドポイントによる MTOM の使用状況を示します。

```xml
<wsoma:OptimizedMimeSerialization />
```

- R4211 : 上記のポリシー アサーションには、エンドポイント ポリシー サブジェクトが含まれており、MTOM を使用して、エンドポイントで送受信されるすべてのメッセージを最適化する必要があることを示しています。

- B4212: MTOM 最適化を使用するように構成すると、WCF エンドポイントは、対応する`wsdl:binding`にアタッチされたポリシーに MTOM ポリシー アサーションを追加します。

### <a name="composition-with-ws-security"></a>WS-Security によるコンポジション
MTOM は、WCF バイナリ XML`text/xml`と同様のエンコーディング メカニズムです。 MTOM は、WS-Security とその他の WS-* プロトコルによる自然なコンポジションを提供します。WS-Security を使用してセキュリティ保護されたメッセージは、MTOM を使用して最適化できます。

### <a name="examples"></a>例

#### <a name="wcf-soap-11-message-encoded-using-mtom"></a>MTOM を使用してエンコードされた WCF SOAP 1.1 メッセージ

```
POST http://131.107.72.15/Mtom/svc/service.svc/Soap11MtomUTF8 HTTP/1.1
SOAPAction: "http://xmlsoap.org/echoBinaryAsString"
Content-Type: multipart/related;type="application/xop+xml";
              start="<http://tempuri.org/0>";start-info="text/xml";
       boundary="uuid:0ca0e16e-feb1-426c-97d8-c4508ada5e82+id=1"
Host: 131.107.72.15
Content-Length: 1501
--uuid:0ca0e16e-feb1-426c-97d8-c4508ada5e82+id=1
Content-ID: <http://tempuri.org/0>
Content-Transfer-Encoding: 8bit
Content-Type: application/xop+xml;charset=utf-8;type="text/xml"
<s:Envelope xmlns:s="http://schemas.xmlsoap.org/soap/envelope/">
  <s:Body>
    <EchoBinaryAsString xmlns="http://xmlsoap.org/Ping">
      <array>
        <xop:Include
         href="cid:http%3A%2F%2Ftempuri.org%2F1%2F632618206521093670"
         xmlns:xop="http://www.w3.org/2004/08/xop/include"/>
      </array>
    </EchoBinaryAsString>
  </s:Body>
</s:Envelope>
--uuid:0ca0e16e-feb1-426c-97d8-c4508ada5e82+id=1
Content-ID: <http://tempuri.org/1/632618206521093670>
Content-Transfer-Encoding: binary
Content-Type: application/octet-stream
…Binary Content..
--uuid:0ca0e16e-feb1-426c-97d8-c4508ada5e82+id=1
```

#### <a name="wcf-secure-soap-12-message-encoded-using-mtom"></a>MTOM を使用してエンコードされた WCF Secure SOAP 1.2 メッセージ
この例では、WS-Security を使用して保護されたメッセージを MTOM と SOAP 1.2 を使用してエンコードします。 エンコーディングの対象として特定されたバイナリ部分は、`BinarySecurityToken`、暗号化された署名に対応する `CipherValue` の `EncryptedData`、および暗号化された本文の内容です。 `CipherValue`の長さが 1024 バイト未満であるため、WCF によって最適化のために識別`EncryptedKey`されなかったことに注意してください。

```
POST http://131.107.72.15/Mtom/service.svc/Soap12MtomSecureSignEncrypt HTTP/1.1
Content-Type: multipart/related; type="application/xop+xml";
              start="<http://tempuri.org/0>";
            boundary="uuid:0ca0e16e-feb1-426c-97d8-c4508ada5e82+id=3";
              start-info="application/soap+xml";
              action="http://xmlsoap.org/echoBinaryAsString"
Host: 131.107.72.15
Content-Length: 1941
--uuid:0ca0e16e-feb1-426c-97d8-c4508ada5e82+id=3
Content-ID: <http://tempuri.org/0>
Content-Transfer-Encoding: 8bit
Content-Type: application/xop+xml;charset=utf-8;type="application/soap+xml"
<s:Envelope xmlns:s="http://schemas.xmlsoap.org/soap/envelope/" xmlns:u="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-utility-1.0.xsd">
  <s:Header>
    <o:Security s:mustUnderstand="1" xmlns:o="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-secext-1.0.xsd">
      <u:Timestamp u:Id="uuid-4d4ee765-5717-4d53-9ac9-99bddc07df6c-5">
        <u:Created>2005-09-09T06:57:32.488Z</u:Created>
        <u:Expires>2005-09-09T07:02:32.488Z</u:Expires>
      </u:Timestamp>
      <o:BinarySecurityToken u:Id="uuid-4d4ee765-5717-4d53-9ac9-99bddc07df6c-2" ValueType="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-x509-token-profile-1.0#X509v3" EncodingType="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-soap-message-security-1.0#Base64Binary">
        <xop:Include href="cid:http%3A%2F%2Ftempuri.org%2F1%2F632618206525089430" xmlns:xop="http://www.w3.org/2004/08/xop/include"/>
      </o:BinarySecurityToken>
      <e:EncryptedKey Id="_1" xmlns:e="http://www.w3.org/2001/04/xmlenc#">
        <e:EncryptionMethod Algorithm="http://www.w3.org/2001/04/xmlenc#rsa-oaep-mgf1p"/>
        <KeyInfo xmlns="http://www.w3.org/2000/09/xmldsig#">
          <o:SecurityTokenReference>
            <o:KeyIdentifier ValueType="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-x509-token-profile-1.0#X509SubjectKeyIdentifier">Xeg55vRyK3ZhAEhEf+YT0z986L0=</o:KeyIdentifier>
          </o:SecurityTokenReference>
        </KeyInfo>
        <e:CipherData>          <e:CipherValue>oQfpxwT8/SAGyZQzKE2b4yO6dXuQj7pwJ+5CGL3Rf7C06bQ5ttMoQ9GLJcQYkXTzin+WwHEgs5bj5ml9HKTW9QAU5JJ6lksdymmQvWP5ZtGPBVchO4sofEGoCKmBiZL/DYS/cnbzgnc/3a6NYnc10y2fWGaGLiqa00zijAw7o0Y=</e:CipherValue>
        </e:CipherData>
      </e:EncryptedKey>
      <c:DerivedKeyToken u:Id="_2" xmlns:c="http://schemas.xmlsoap.org/ws/2005/02/sc">
        <o:SecurityTokenReference>
          <o:Reference URI="#_1"/>
        </o:SecurityTokenReference>
        <c:Nonce>OrEPRX7fISIS4sXYWPMv3g==</c:Nonce>
      </c:DerivedKeyToken>
      <e:ReferenceList xmlns:e="http://www.w3.org/2001/04/xmlenc#">
        <e:DataReference URI="#_3"/>
        <e:DataReference URI="#_4"/>
      </e:ReferenceList>
      <e:EncryptedData Id="_4" Type="http://www.w3.org/2001/04/xmlenc#Element" xmlns:e="http://www.w3.org/2001/04/xmlenc#">
        <e:EncryptionMethod Algorithm="http://www.w3.org/2001/04/xmlenc#aes256-cbc"/>
        <KeyInfo xmlns="http://www.w3.org/2000/09/xmldsig#">
          <o:SecurityTokenReference>
            <o:Reference URI="#_2"/>
          </o:SecurityTokenReference>
        </KeyInfo>
        <e:CipherData>
          <e:CipherValue>
            <xop:Include href="cid:http%3A%2F%2Ftempuri.org%2F2%2F632618206525089430" xmlns:xop="http://www.w3.org/2004/08/xop/include"/>
          </e:CipherValue>
        </e:CipherData>
      </e:EncryptedData>
    </o:Security>
  </s:Header>
  <s:Body u:Id="_0">
    <e:EncryptedData Id="_3" Type="http://www.w3.org/2001/04/xmlenc#Content" xmlns:e="http://www.w3.org/2001/04/xmlenc#">
      <e:EncryptionMethod Algorithm="http://www.w3.org/2001/04/xmlenc#aes256-cbc"/>
      <KeyInfo xmlns="http://www.w3.org/2000/09/xmldsig#">
        <o:SecurityTokenReference xmlns:o="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-secext-1.0.xsd">
          <o:Reference URI="#_2"/>
        </o:SecurityTokenReference>
      </KeyInfo>
      <e:CipherData>
        <e:CipherValue>
          <xop:Include href="cid:http%3A%2F%2Ftempuri.org%2F3%2F632618206525089430" xmlns:xop="http://www.w3.org/2004/08/xop/include"/>
        </e:CipherValue>
      </e:CipherData>
    </e:EncryptedData>
  </s:Body>
</s:Envelope>
--uuid:0ca0e16e-feb1-426c-97d8-c4508ada5e82+id=3
Content-ID: <http://tempuri.org/1/632618206525089430>
Content-Transfer-Encoding: binary
Content-Type: application/octet-stream
...Binary content of BinarySecurityToken - X509 Certificate...
--uuid:0ca0e16e-feb1-426c-97d8-c4508ada5e82+id=3
Content-ID: <http://tempuri.org/2/632618206525089430>
Content-Transfer-Encoding: binary
Content-Type: application/octet-stream
...Binary serialization of the encrypted primary signature...
--uuid:0ca0e16e-feb1-426c-97d8-c4508ada5e82+id=3
Content-ID: <http://tempuri.org/3/632618206525089430>
Content-Transfer-Encoding: binary
Content-Type: application/octet-stream
...Binary serialization of the encrypted Body...
--uuid:0ca0e16e-feb1-426c-97d8-c4508ada5e82+id=3--
```
