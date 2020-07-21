---
ms.openlocfilehash: 3c6142fd536bad5676f02570fecd4eb0605db829
ms.sourcegitcommit: 0926684d8d34f4c6b5acce58d2193db093cb9cf2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/20/2020
ms.locfileid: "83721142"
---
### <a name="begin-trusted-certificate-syntax-no-longer-supported-for-root-certificates-on-linux"></a>Linux のルート証明書に対して "BEGIN TRUSTED CERTIFICATE" 構文がサポートされなくなった

Linux およびその他の Unix 類似システム (macOS 以外) のルート証明書は、標準の `BEGIN CERTIFICATE` PEM ヘッダーと、OpenSSL 固有の `BEGIN TRUSTED CERTIFICATE` PEM ヘッダーの 2 つの形式で提示できます。 後者の構文では、.NET Core の <xref:System.Security.Cryptography.X509Certificates.X509Chain?displayProperty=fullName> クラスとの互換性の問題の原因となる追加の構成が可能です。 `BEGIN TRUSTED CERTIFICATE` ルート証明書の内容は、.NET Core 3.0 以降のチェーン エンジンでは読み込まれなくなりました。

#### <a name="change-description"></a>変更の説明

以前は、ルート信頼リストを設定するために、`BEGIN CERTIFICATE` と `BEGIN TRUSTED CERTIFICATE` 両方の構文が使用されていました。 `BEGIN TRUSTED CERTIFICATE` 構文を使用し、ファイルで追加のオプションを指定した場合、信頼チェーンが明示的に禁止されたことが、<xref:System.Security.Cryptography.X509Certificates.X509Chain> によって報告される場合があります (<xref:System.Security.Cryptography.X509Certificates.X509ChainStatusFlags.ExplicitDistrust?displayProperty=nameWithType>)。 ただし、その証明書が、それより前に読み込まれたファイルの `BEGIN CERTIFICATE` 構文でも指定されていた場合は、信頼チェーンは許可されました。

.NET Core 3.0 以降、`BEGIN TRUSTED CERTIFICATE` の内容は読み取られなくなりました。 証明書が標準の `BEGIN CERTIFICATE` 構文でも指定されていない場合、<xref:System.Security.Cryptography.X509Certificates.X509Chain> ではルートが信頼されていないと報告されます (<xref:System.Security.Cryptography.X509Certificates.X509ChainStatusFlags.UntrustedRoot?displayProperty=nameWithType>)。

#### <a name="version-introduced"></a>導入されたバージョン

3.0

#### <a name="recommended-action"></a>推奨アクション

ほとんどのアプリケーションはこの変更の影響を受けませんが、アクセス許可の問題のために両方のルート証明書ソースを確認できないアプリケーションでは、アップグレード後に予期しない `UntrustedRoot` エラーが発生する可能性があります。

多くの Linux ディストリビューションでは、ルート証明書はファイルごとに 1 証明書のディレクトリと、1 ファイル連結の 2 つの場所に書き込まれます。 一部のディストリビューションでは、ファイルごとに 1 証明書のディレクトリには `BEGIN TRUSTED CERTIFICATE` 構文が使用され、ファイル連結には標準の `BEGIN CERTIFICATE` 構文が使用されています。 これらの場所の少なくとも 1 つにすべてのカスタム ルート証明書が `BEGIN CERTIFICATE` として追加されていること、およびアプリケーションで両方の場所を読み取ることができることを確認してください。

一般的なディレクトリは */etc/ssl/certs/* であり、一般的な連結されたファイルは */etc/ssl/cert.pem* です。 プラットフォーム固有のルートを確認するには、`openssl version -d` コマンドを使用します。これは、 */etc/ssl/* と異なる場合があります。 たとえば、Ubuntu 18.04 では、ディレクトリは */usr/lib/ssl/certs/* であり、ファイルは */usr/lib/ssl/cert.pem* です。 ただし、 */usr/lib/ssl/certs/* は */etc/ssl/certs/* へのシンボリック リンクであり、 */usr/lib/ssl/cert.pem* は存在しません。

```bash
$ openssl version -d
OPENSSLDIR: "/usr/lib/ssl"
$ ls -al /usr/lib/ssl
total 12
drwxr-xr-x  3 root root 4096 Dec 12 17:10 .
drwxr-xr-x 73 root root 4096 Feb 20 15:18 ..
lrwxrwxrwx  1 root root   14 Mar 27  2018 certs -> /etc/ssl/certs
drwxr-xr-x  2 root root 4096 Dec 12 17:10 misc
lrwxrwxrwx  1 root root   20 Nov 12 16:58 openssl.cnf -> /etc/ssl/openssl.cnf
lrwxrwxrwx  1 root root   16 Mar 27  2018 private -> /etc/ssl/private
```

#### <a name="category"></a>カテゴリ

暗号

#### <a name="affected-apis"></a>影響を受ける API

- <xref:System.Security.Cryptography.X509Certificates.X509Chain?displayProperty=fullName>

<!--

#### Affected APIs

- `T:System.Security.Cryptography.X509Certificates.X509Chain`

-->
