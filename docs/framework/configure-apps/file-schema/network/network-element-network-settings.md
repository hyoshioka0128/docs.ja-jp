---
title: <network> 要素 (ネットワーク設定)
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#network
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/mailSettings/smtp/network
helpviewer_keywords:
- <network> element
- network element
ms.assetid: 2c2c6ad4-ed11-48ab-b28e-2bc0ba9b42c7
ms.openlocfilehash: bac288bb28c4176e52366d0e0b7d8bc7d313cf96
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/01/2019
ms.locfileid: "71698014"
---
# <a name="network-element-network-settings"></a>@no__t 0network > 要素 (ネットワーク設定)
外部の簡易メール転送プロトコル (SMTP) サーバーのネットワークオプションを構成します。  
  
[ **\<configuration>** ](../configuration-element.md)  
&nbsp; @ no__t-1[ **@no__t 47 >** ](system-net-element-network-settings.md)  
&nbsp; @ no__t @ no__t-2 @ no__t-3[ **\<mailSettings >** ](mailsettings-element-network-settings.md)  
&nbsp; @ no__t-1 @ no__t @ no__t @ no__t-5[ **\<smtp >** のようになります。](smtp-element-network-settings.md)  
&nbsp; @ no__t-1 @ no__t @ no__t @ no__t-5 @ no__t-6 @ no__t-7 **\<network > に**なります。  
  
## <a name="syntax"></a>構文  
  
```xml  
<network  
  clientDomain="string"   
  defaultCredentials="true|false"  
  enableSsl="true|false"  
  host="string"   
  password="string"  
  port="integer"   
  targetName="string"  
  userName="string"  
/>  
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|`clientDomain`|SMTP メールサーバーに接続するための最初の SMTP プロトコル要求で使用するクライアントドメイン名を指定します。 既定値は、要求を送信しているローカルコンピューターの localhost 名です。|  
|`defaultCredentials`|Smtp トランザクションの SMTP メールサーバーへのアクセスに、既定のユーザー資格情報を使用するかどうかを指定します。 既定値は `false` です。|  
|`enableSsl`|SMTP メールサーバーへのアクセスに SSL を使用するかどうかを指定します。 既定値は `false` です。|  
|`host`|SMTP トランザクションに使用する SMTP メールサーバーのホスト名を指定します。 この属性には既定値はありません。|  
|`password`|SMTP メールサーバーへの認証に使用するパスワードを指定します。 この属性には既定値はありません。|  
|`port`|SMTP メールサーバーへの接続に使用するポート番号を指定します。 既定値は、25 です。|  
|`targetName`|SMTP トランザクションの拡張保護を使用するときに認証に使用するサービスプロバイダー名 (SPN) を指定します。 この属性には既定値はありません。|  
|`userName`|SMTP メールサーバーへの認証に使用するユーザー名を指定します。 この属性には既定値はありません。|  
  
### <a name="child-elements"></a>子要素  
 なし。  
  
### <a name="parent-elements"></a>親要素  
  
|要素|説明|  
|-------------|-----------------|  
|[\<smtp> 要素 (ネットワーク設定)](smtp-element-network-settings.md)|簡易メール転送プロトコル (SMTP) 電子メールの送信オプションを構成します。|  
  
## <a name="remarks"></a>Remarks  
 一部の SMTP サーバーでは、使用する前にサーバーに対して認証を行う必要があります。 ホストで既定のネットワーク資格情報を使用して認証する場合は、`defaultCredentials` 属性を `true` に設定します。 @No__t-0 プロパティを使用して、適用可能な構成ファイルから `defaultCredentials` 属性の現在の値を取得できます。  
  
 基本認証 (ユーザー名とパスワード) を使用して、SMTP サーバーに対する認証を行うこともできます。 このオプションを使用するには、指定した SMTP サーバーの有効なユーザー名とパスワードを指定する必要があります。  
  
> [!NOTE]
> 基本認証では、`userName` および `password` の値が暗号化されずにサーバーに送信されます。 ネットワークトラフィックを監視するすべてのユーザーは、資格情報を表示し、それらを使用してサーバーに接続できます。 Kerberos や NT LAN Manager (NTLM) など、より安全な認証メカニズムの使用を検討する必要があります。@No__t-0 が `true` の場合、サーバーがこれらのプロトコルをサポートする場合、Kerberos または NTLM が使用されます。  
  
 基本認証および既定のネットワーク資格情報オプションは、同時には指定できません。`defaultCredentials` を `true` に設定し、ユーザー名とパスワードを指定すると、既定のネットワーク資格情報が使用され、基本認証データは無視されます。  
  
 @No__t-0 を指定する場合は、[基本認証] で、メールサーバーに対して自分で認証を行うための `password` を指定する必要もあります。  
  
 @No__t-0 プロパティを使用して、適用可能な構成ファイルから `userName` 属性の現在の値を取得できます。 @No__t-0 プロパティを使用して、適用可能な構成ファイルから `password` 属性の現在の値を取得できます。 セキュリティ上の理由から、通常、構成ファイルには @no__t 0 属性が入力されません。  
  
 @No__t-0 属性は、SMTP プロトコルの初期要求で使用されるクライアントのドメイン名を SMTP サーバーに変更します。 @No__t-0 属性は、既定で使用される localhost 名ではなく、ローカルコンピューターの完全修飾ドメイン名に設定できます。 これにより、SMTP プロトコル標準への準拠が向上します。 既定値は、要求を送信しているローカルコンピューターの localhost 名です。 @No__t-0 プロパティを使用して、適用可能な構成ファイルから `clientDomain` 属性の現在の値を取得できます。  
  
 @No__t-0 属性は、拡張保護を使用する場合に認証に使用されます。 既定値は "SMTPSVC/\<host >" の形式です。ここで \<host > は SMTP メールサーバーのホスト名です。 @No__t-0 プロパティを使用して、適用可能な構成ファイルから `targetName` 属性の現在の値を取得できます。  
  
 @No__t-0 属性は、SMTP メールサーバーへのアクセスに SSL を使用するかどうかを指定します。 <xref:System.Net.Mail.SmtpClient?displayProperty=nameWithType>クラスでサポートされているのは、RFC 3207 で定義されているトランスポート層セキュリティ経由の Secure smtp に対する smtp サービス拡張のみです。 このモードでは、暗号化されていないチャネルで SMTP セッションが開始され、SSL を使用してセキュリティで保護された通信に切り替えるために、クライアントからサーバーに STARTTLS コマンドが発行されます。 詳細については、インターネット技術標準化委員会 (IETF) によって発行された RFC 3207 を参照してください。  
  
 代替の接続方法では、プロトコルコマンドが送信される前に、SSL セッションが事前に確立されます。 この接続方法は SMTPS とも呼ばれ、既定ではポート465を使用します。 SSL を使用したこの代替接続方法は、現在サポートされていません。  
  
 @No__t-0 プロパティを使用して、適用可能な構成ファイルから `enableSsl` 属性の現在の値を取得できます。  
  
## <a name="example"></a>例  
 次の例では、既定のネットワーク資格情報を使用して電子メールを送信するための適切な SMTP パラメーターを指定しています。  
  
```xml  
<configuration>  
  <system.net>  
    <mailSettings>  
      <smtp deliveryMethod="Network">  
        <network  
          clientDomain="www.contoso.com"  
          defaultCredentials="true"  
          enableSsl="false"  
          host="mail.contoso.com"  
          port="25"  
        />  
      </smtp>  
    </mailSettings>  
  </system.net>  
</configuration>  
```  
  
## <a name="see-also"></a>関連項目

- <xref:System.Net.Configuration.SmtpNetworkElement?displayProperty=nameWithType>
- <xref:System.Net.Configuration.SmtpSection?displayProperty=nameWithType>
- <xref:System.Net.Mail.SmtpClient?displayProperty=nameWithType>
- [ネットワーク設定スキーマ](index.md)
