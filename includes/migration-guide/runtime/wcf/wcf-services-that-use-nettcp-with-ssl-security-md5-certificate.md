---
ms.openlocfilehash: fb9436ec9e525afb497033775e34b6b636ced22d
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85621351"
---
### <a name="wcf-services-that-use-nettcp-with-ssl-security-and-md5-certificate-authentication"></a>SSL セキュリティと MD5 証明書認証で NETTCP を使用する WCF サービス

#### <a name="details"></a>説明

.NET Framework 4.6 では、WCF SSL の既定のプロトコル一覧に TLS 1.1 および TLS 1.2 が追加されます。 クライアントとサーバーの両方のコンピューターに .NET Framework 4.6 以降がインストールされている場合は、TLS 1.2 がネゴシエーションに使用されます。TLS 1.2 では MD5 証明書認証がサポートされません。 このため、顧客が MD5 証明書を使用する場合、WCF クライアントでは WCF サービスへ接続できません。

#### <a name="suggestion"></a>提案される解決策

次のいずれかの操作を実行することで、この問題を回避して、WCF クライアントを WCF サーバーに接続できるようになります。

- MD5 アルゴリズムを使用しないように証明書を更新します。 この解決策をお勧めします。
- バインドがソース コードで動的に構成されていない場合は、TLS 1.1 または以前のバージョンのプロトコルを使用するようにアプリケーションの構成ファイルを更新します。 これにより、引き続き MD5 ハッシュ アルゴリズムによる証明書を使用することができます。

> [!WARNING]
> MD5 ハッシュ アルゴリズムによる証明書は安全でないと見なされるため、この回避策はお勧めできません。

次の構成ファイルでこれを行います。

```xml
<configuration>
  <system.serviceModel>
    <bindings>
      <netTcpBinding>
        <binding>
          <security mode= "None/Transport/Message/TransportWithMessageCredential" >
            <transport clientCredentialType="None/Windows/Certificate"
                       protectionLevel="None/Sign/EncryptAndSign"
                       sslProtocols="Ssl3/Tls1/Tls11">
            </transport>
          </security>
        </binding>
      </netTcpBinding>
    </bindings>
  </system.ServiceModel>
</configuration>
```

- バインドがソース コードで動的に構成されている場合は、ソース コード内で TLS 1.1 (<xref:System.Security.Authentication.SslProtocols.Tls11?displayProperty=nameWithType>) または以前のバージョンのプロトコルを使用するように <xref:System.ServiceModel.TcpTransportSecurity.SslProtocols?displayProperty=nameWithType> プロパティを更新します。

> [!WARNING]
> MD5 ハッシュ アルゴリズムによる証明書は安全でないと見なされるため、この回避策はお勧めできません。

| 名前    | 値   |
|:--------|:--------|
| スコープ   | マイナー   |
| バージョン | 4.6     |
| 種類    | ランタイム |
