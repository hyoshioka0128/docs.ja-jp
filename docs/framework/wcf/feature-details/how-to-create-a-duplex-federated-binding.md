---
title: '方法: 双方向フェデレーション バインディングを作成する'
ms.date: 03/30/2017
ms.assetid: 4331d2bc-5455-492a-9189-634a82597726
ms.openlocfilehash: e93651ce9fe9dae55c299fcb061da6bdc4b6bc5e
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84598971"
---
# <a name="how-to-create-a-duplex-federated-binding"></a>方法: 双方向フェデレーション バインディングを作成する

<xref:System.ServiceModel.WSFederationHttpBinding> はデータグラムと要求/応答メッセージの交換コントラクトのみをサポートします。 双方向メッセージ交換コントラクトを使用するには、カスタム バインディングを作成する必要があります。 次の手順は、構成の中でそれを行う方法を説明します。HTTP と TCP トランスポートにはメッセージ モード セキュリティを、TCP トランスポートには混合モード セキュリティを使用します。 このトピックの最後に 3 つのバインディングすべてのサンプル コードがあります。

バインディングはコード内でも作成できます。 作成するバインド要素スタックの説明については、「[方法: カスタムバインディングを使用してカスタムバインディングを作成](how-to-create-a-custom-binding-using-the-securitybindingelement.md)する」を参照してください。

## <a name="to-create-a-duplex-federated-custom-binding-with-http"></a>HTTP で双方向カスタム フェデレーション バインディングを作成するには

1. [\<bindings>](../../configure-apps/file-schema/wcf/bindings.md)構成ファイルのノードで、要素を作成 [\<customBinding>](../../configure-apps/file-schema/wcf/custombinding.md) します。

2. 要素内に、 [\<customBinding>](../../configure-apps/file-schema/wcf/custombinding.md) [\<binding>](../../configure-apps/file-schema/wcf/bindings.md) 属性をに設定して要素を作成 `name` `FederationDuplexHttpMessageSecurityBinding` します。

3. 要素内に、 [\<binding>](../../configure-apps/file-schema/wcf/bindings.md) [\<security>](../../configure-apps/file-schema/wcf/security-of-custombinding.md) 属性をに設定して要素を作成 `authenticationMode` `SecureConversation` します。

4. 要素内に、 [\<security>](../../configure-apps/file-schema/wcf/security-of-custombinding.md) 属性を [\<secureConversationBootstrap>](../../configure-apps/file-schema/wcf/secureconversationbootstrap.md) `authenticationMode` またはに設定して要素を作成し `IssuedTokenForCertificate` `IssuedTokenForSslNegotiated` ます。

5. 要素の後 [\<security>](../../configure-apps/file-schema/wcf/security-of-custombinding.md) に、空の [\<compositeDuplex>](../../configure-apps/file-schema/wcf/compositeduplex.md) 要素を作成します。

6. 要素の後 [\<compositeDuplex>](../../configure-apps/file-schema/wcf/compositeduplex.md) に、空の [\<oneWay>](../../configure-apps/file-schema/wcf/oneway.md) 要素を作成します。

7. 要素の後 [\<oneWay>](../../configure-apps/file-schema/wcf/oneway.md) に、空の [\<httpTransport>](../../configure-apps/file-schema/wcf/httptransport.md) 要素を作成します。

## <a name="to-create-a-duplex-federated-custom-binding-with-tcp-message-security-mode"></a>TCP メッセージ セキュリティ モードで双方向カスタム フェデレーション バインディングを作成するには

1. [\<bindings>](../../configure-apps/file-schema/wcf/bindings.md)構成ファイルのノードで、要素を作成 [\<customBinding>](../../configure-apps/file-schema/wcf/custombinding.md) します。

2. 要素内に、 [\<customBinding>](../../configure-apps/file-schema/wcf/custombinding.md) [\<binding>](../../configure-apps/file-schema/wcf/bindings.md) 属性をに設定して要素を作成 `name` `FederationDuplexTcpMessageSecurityBinding` します。

3. 要素内に、 [\<binding>](../../configure-apps/file-schema/wcf/bindings.md) [\<security>](../../configure-apps/file-schema/wcf/security-of-custombinding.md) 属性をに設定して要素を作成 `authenticationMode` `SecureConversation` します。

4. 要素内に、 [\<security>](../../configure-apps/file-schema/wcf/security-of-custombinding.md) 属性を [\<secureConversationBootstrap>](../../configure-apps/file-schema/wcf/secureconversationbootstrap.md) `authenticationMode` またはに設定して要素を作成し `IssuedTokenForCertificate` `IssuedTokenForSslNegotiated` ます。

5. 要素の後 [\<security>](../../configure-apps/file-schema/wcf/security-of-custombinding.md) に、空の [\<tcpTransport>](../../configure-apps/file-schema/wcf/tcptransport.md) 要素を作成します。

## <a name="to-create-a-duplex-federated-custom-binding-with-tcp-mixed-security-mode"></a>TCP 混合セキュリティ モードで双方向カスタム フェデレーション バインディングを作成するには

1. [\<bindings>](../../configure-apps/file-schema/wcf/bindings.md)構成ファイルのノードで、要素を作成 [\<customBinding>](../../configure-apps/file-schema/wcf/custombinding.md) します。

2. 要素内に、 [\<customBinding>](../../configure-apps/file-schema/wcf/custombinding.md) [\<binding>](../../configure-apps/file-schema/wcf/bindings.md) 属性をに設定して要素を作成 `name` `FederationDuplexTcpTransportSecurityWithMessageCredentialBinding` します。

3. 要素内に、 [\<binding>](../../configure-apps/file-schema/wcf/bindings.md) [\<security>](../../configure-apps/file-schema/wcf/security-of-custombinding.md) 属性をに設定して要素を作成 `authenticationMode` `SecureConversation` します。

4. 要素内に、 [\<security>](../../configure-apps/file-schema/wcf/security-of-custombinding.md) 属性を [\<secureConversationBootstrap>](../../configure-apps/file-schema/wcf/secureconversationbootstrap.md) `authenticationMode` またはに設定して要素を作成し `IssuedTokenForCertificate` `IssuedTokenForSslNegotiated` ます。

5. 要素の後 [\<security>](../../configure-apps/file-schema/wcf/security-of-custombinding.md) に、空の [\<sslStreamSecurity>](../../configure-apps/file-schema/wcf/sslstreamsecurity.md) 要素を作成します。

6. 要素の後 [\<sslStreamSecurity>](../../configure-apps/file-schema/wcf/sslstreamsecurity.md) に、空の [\<tcpTransport>](../../configure-apps/file-schema/wcf/tcptransport.md) 要素を作成します。

## <a name="code-sample"></a>コード サンプル

### <a name="sample-with-3-bindings"></a>3 つのバインディングの例

1. 次のコードを構成ファイルに挿入します。

## <a name="example"></a>例

```xml
<bindings>
   <customBinding>
      <binding name="FederationDuplexHttpMessageSecurityBinding">
<!-- duplex contract requires secure conversation with require cancellation = true -->
          <security authenticationMode="SecureConversation">
              <secureConversationBootstrap authenticationMode="IssuedTokenForSslNegotiated" />
          </security>
          <compositeDuplex />
          <oneWay />
          <httpTransport />
       </binding>
<!-- duplex over https is not supported -->
       <binding name="FederationDuplexTcpMessageSecurityBinding">
<!-- duplex contract requires secure conversation with require cancellation = true -->
          <security authenticationMode="SecureConversation">
              <secureConversationBootstrap authenticationMode="IssuedTokenForSslNegotiated" />
          </security>
          <tcpTransport />
       </binding>
       <binding name="FederationDuplexTcpTransportSecurityWithMessageCredentialsBinding">
<!-- duplex contract requires secure conversation with require cancellation = true -->
          <security authenticationMode="SecureConversation">
              <secureConversationBootstrap authenticationMode="IssuedTokenOverTransport" />
          </security>
<!-- requireClientCertificate = true or <windowsStreamSecurity /> can be used, but does not make sense for most scenarios -->
          <sslStreamSecurity />
          <tcpTransport />
       </binding>
    </customBinding>
</bindings>
```
