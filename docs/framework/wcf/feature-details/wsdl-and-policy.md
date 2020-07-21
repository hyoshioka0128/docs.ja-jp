---
title: WSDL とポリシー
ms.date: 03/30/2017
ms.assetid: cea87440-3519-4640-8494-b8a2b0e88c84
ms.openlocfilehash: 201920a8ebf639c74acfb20b2e990c8bbc0c5b55
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84600102"
---
# <a name="wsdl-and-policy"></a>WSDL とポリシー
このトピックでは、Windows Communication Foundation (WCF) WSDL 1.1、WS-POLICY および WS-POLICY 添付の実装の詳細、および WCF によって導入された追加の WS-POLICY アサーションと WSDL 1.1 拡張について説明します。  
  
 WCF は、このドキュメントで説明されている制約と説明に従って、W3C に送信される WS-POLICY および WS-POLICY 添付仕様を実装します。  
  
 このドキュメントでは、次の表に示すプレフィックスと名前空間を使用します。  
  
|Prefix|名前空間|  
|------------|---------------|  
|wsp (WS-Policy 1.2)|`http://schemas.xmlsoap.org/ws/2004/09/policy`|  
|wsp (WS-Policy 1.5)|`http://www.w3.org/ns/ws-policy`|  
|http|`http://schemas.microsoft.com/ws/06/2004/policy/http`|  
|msmq|`http://schemas.microsoft.com/ws/06/2004/mspolicy/msmq`|  
|msf|`http://schemas.microsoft.com/ws/2006/05/framing/policy`|  
|mssp|`http://schemas.microsoft.com/ws/2005/07/securitypolicy`|  
|msc|`http://schemas.microsoft.com/ws/2005/12/wsdl/contract`|  
|cdp|`http://schemas.microsoft.com/net/2006/06/duplex`|  
  
## <a name="wcf-wsdl11-extensions"></a>WCF WSDL1.1 の拡張  
 WCF では、次の WSDL 1.1 拡張機能を使用して、コントラクトセッションの要件を記述します。  
  
 wsdl:portType/wsdl:operation/@msc:isInitiating  
 xs: boolean は、この操作が WCF セッションを開始することを示します。既定値は `false` です。  
  
 wsdl:portType/wsdl:operation/@msc:isTerminating  
 xs: boolean は、この操作が WCF セッションを終了することを示します。既定値は `false` です。  
  
 wsdl:portType/wsdl:operation/@msc:usingSession  
 xs:boolean は、このコントラクトでセッションを確立する必要があるかどうかを示します。  
  
### <a name="soap-1x-http-binding-transport-uris"></a>SOAP 1.x HTTP バインディング トランスポートの URI  
 WCF では、次の Uri を使用して、WSDL 1.1、SOAP 1.1、および SOAP 1.2 バインド拡張要素に使用されるトランスポートを示します。  
  
|トランスポート|URI|  
|---------------|---------|  
|HTTP|`http://schemas.xmlsoap.org/soap/http`|  
|TCP|`http://schemas.microsoft.com/soap/tcp`|  
|MSMQ|`http://schemas.microsoft.com/soap/msmq`|  
|名前付きパイプ|`http://schemas.microsoft.com/soap/named-pipe`|  
  
## <a name="policy-assertions-implemented-by-wcf"></a>WCF で実装されるポリシー アサーション  
 Web サービス仕様 (WS-*) で導入されたポリシーアサーションに加えて、このドキュメントの他のセクションで説明したように、WCF では次のポリシーアサーションが実装されています。  
  
|ポリシー アサーション|ポリシー サブジェクト|説明|  
|----------------------|--------------------|-----------------|  
|http:HttpBasicAuthentication|エンドポイント|エンドポイントは、HTTP 基本認証を使用します。|  
|http:HttpDigestAuthentication|エンドポイント|エンドポイントは、HTTP ダイジェスト認証を使用します。|  
|http:HttpNegotiateAuthentication|エンドポイント|エンドポイントは、HTTP ネゴシエート認証を使用します。|  
|http:HttpNtlmAuthentication|エンドポイント|エンドポイントは、HTTP NTLM 認証を使用します。|  
|msf:Streamed|エンドポイント|エンドポイントは、ストリーミングされたメッセージ フレームを使用します。 このアサーションは、TCP、名前付きパイプのようなトランスポートに提供されるメッセージ フレーム プロトコルと共に使用されます。|  
|msf:SslTransportSecurity|エンドポイント|エンドポイントは、トランスポート層セキュリティ (TLS) をメッセージ フレームと共に使用します。|  
|msf:WindowsTransportSecurity|エンドポイント|エンドポイントは、Security Provider Negotiation (SPNEGO) をメッセージ フレームと共に使用します。|  
|msmq:MsmqBestEffort|エンドポイント|MSMQ はベストエフォート保証を使用します。|  
|msmq:MsmqSession|エンドポイント|MSMQ はセッション保証を使用します。|  
|msmq:MsmqVolatile|エンドポイント|MSMQ は揮発性です。|  
|msmq:Authenticated|エンドポイント|認証が、MSMQ トランスポートと共に使用されます。|  
|msmq:WindowsDomain|エンドポイント|MSMQ は Windows ドメイン認証を使用します。|  
|cdp:CompositeDuplex|エンドポイント|エンドポイントは、メッセージの送受信に 2 つの個別の逆方向トランスポート接続を使用します。|  
|mssp:RsaToken|入れ子|RSA キー トークンのアサーションです。 通常、この要件を満たすのは、保証する署名内でキー情報の一部として直接シリアル化される RSA キーです。|  
|mssp:SslContextToken|入れ子|WS-Trust を使用するバイナリ TLS ハンドシェイクによって取得される SecurityContextToken の使用を要求します。 入れ子になったアサーションには、sp:RequireDerivedKeys、mssp:MustNotSendCancel、mssp:RequireClientCertificate があります。|  
|mssp:MustNotSendCancel|入れ子|Cancel バインディング [WS-Trust、WS-SC] を使用するセキュリティ トークン要求 (RST) の要求メッセージ [WS-Trust] を特定の SecurityContextToken の発行者に送信しないという要件を指定します。 このアサーションが存在する場合、このような要求メッセージを発行者に送信することはできません。 このアサーションが存在しない場合、このような要求メッセージを発行者に送信できます。|  
|mssp:RequireClientCertificate|入れ子|このオプション要素では、TLSNEGO プロトコルの一部としてクライアント証明書を提供するという要件を指定します。 このアサーションが存在する場合、クライアント証明書を提供する必要があります。 このアサーションが存在しない場合、クライアント証明書を提供しないでください。 このアサーションは、mssp:SslContextToken の外側で使用することはできません。|  
  
## <a name="see-also"></a>関連項目

- [カスタム WSDL パブリケーション](../samples/custom-wsdl-publication.md)
- [方法: カスタム WSDL をエクスポートする](../extending/how-to-export-custom-wsdl.md)
- [方法: カスタム WSDL をインポートする](../extending/how-to-import-custom-wsdl.md)
