---
ms.openlocfilehash: 9b734fe960165b6d4b97b861cb3e8f31979f25c5
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85621212"
---
### <a name="remove-ssl3-from-the-wcf-transportdefaults"></a>WCF TransportDefaults からの Ssl3 の削除

#### <a name="details"></a>説明

トランスポート セキュリティで NetTcp を使用し、証明書の資格情報の種類を使用する場合、SSL 3 プロトコルは、安全な接続のネゴシエーションに使用される既定のプロトコルではなくなりました。 TLS 1.0 は常に NetTcp のプロトコル一覧に含まれているため、ほとんどの場合、既存のアプリには影響はないと考えられます。 既存のすべてのクライアントは TLS 1.0 以降を使用して接続をネゴシエートできるようになりました。

#### <a name="suggestion"></a>提案される解決策

Ssl3 が必要な場合は、以下の構成メカニズムのいずれかを使用して、ネゴシエートされたプロトコルの一覧に Ssl3 を追加します。<ul><li><xref:System.ServiceModel.Channels.SslStreamSecurityBindingElement.SslProtocols></li><li><xref:System.ServiceModel.TcpTransportSecurity.SslProtocols></li><li>[<](~/docs/framework/configure-apps/file-schema/wcf/transport-of-nettcpbinding.md)</li><li>[&lt;customBinding&gt; の &lt;sslStreamSecurity&gt; セクション]~/docs/framework/configure-apps/file-schema/wcf/sslstreamsecurity.md)</li></ul>

| 名前    | 値       |
|:--------|:------------|
| スコープ   |エッジ|
|バージョン|4.6.2|
|種類|ランタイム

#### <a name="affected-apis"></a>影響を受ける API

-<xref:System.ServiceModel.Channels.SslStreamSecurityBindingElement.SslProtocols?displayProperty=nameWithType></li><li><xref:System.ServiceModel.TcpTransportSecurity.SslProtocols?displayProperty=nameWithType></li></ul>|
