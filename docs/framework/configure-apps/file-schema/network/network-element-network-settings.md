---
title: <network> 要素 (ネットワーク設定)
description: <network>Network settings 要素は、.NET Framework の外部 SMTP サーバーオプションのネットワークオプションを構成します。
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#network
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/mailSettings/smtp/network
helpviewer_keywords:
- <network> element
- network element
ms.assetid: 2c2c6ad4-ed11-48ab-b28e-2bc0ba9b42c7
ms.openlocfilehash: 36857e63871b4672df349934594f0887a042609e
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84504551"
---
# <a name="network-element-network-settings"></a>\<network> 要素 (ネットワーク設定)
外部の簡易メール転送プロトコル (SMTP) サーバーのネットワークオプションを構成します。  

[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.net>**](system-net-element-network-settings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<mailSettings>**](mailsettings-element-network-settings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<smtp>**](smtp-element-network-settings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<network>**

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
|`port`|SMTP メールサーバーへの接続に使用するポート番号を指定します。 既定値は 25 です。|  
|`targetName`|SMTP トランザクションの拡張保護を使用するときに認証に使用するサービスプロバイダー名 (SPN) を指定します。 この属性には既定値はありません。|  
|`userName`|SMTP メールサーバーへの認証に使用するユーザー名を指定します。 この属性には既定値はありません。|  
  
### <a name="child-elements"></a>子要素  
 なし。  
  
### <a name="parent-elements"></a>親要素  
  
|要素|説明|  
|-------------|-----------------|  
|[\<smtp>要素 (ネットワーク設定)](smtp-element-network-settings.md)|SMTP (Simple Mail Transport Protocol) メール送信オプションを構成します。|  
  
## <a name="remarks"></a>解説  
 一部の SMTP サーバーでは、使用する前にサーバーに対して認証を行う必要があります。 ホストで既定のネットワーク資格情報を使用して認証する場合は、 `defaultCredentials` 属性をに設定 `true` します。 プロパティは、 <xref:System.Net.Configuration.SmtpNetworkElement.DefaultCredentials%2A?displayProperty=nameWithType> `defaultCredentials` 適用可能な構成ファイルから属性の現在の値を取得するために使用できます。  
  
 基本認証 (ユーザー名とパスワード) を使用して、SMTP サーバーに対する認証を行うこともできます。 このオプションを使用するには、指定した SMTP サーバーの有効なユーザー名とパスワードを指定する必要があります。  
  
> [!NOTE]
> 基本認証は、 `userName` およびの `password` 値を暗号化せずにサーバーに送信します。 ネットワークトラフィックを監視するすべてのユーザーは、資格情報を表示し、それらを使用してサーバーに接続できます。 Kerberos や NT LAN Manager (NTLM) など、より安全な認証メカニズムの使用を検討する必要があります。がの場合 `defaultCredentials` `true` 、サーバーがこれらのプロトコルをサポートする場合、Kerberos または NTLM が使用されます。  
  
 基本認証および既定のネットワーク資格情報オプションは、同時には指定できません。`defaultCredentials`をに設定 `true` し、ユーザー名とパスワードを指定した場合、既定のネットワーク資格情報が使用され、基本認証データは無視されます。  
  
 基本認証でを指定する場合は、 `userName` メールサーバーに対して自分で認証を行うようにを指定する必要もあり `password` ます。  
  
 プロパティは、 <xref:System.Net.Configuration.SmtpNetworkElement.UserName%2A?displayProperty=nameWithType> `userName` 適用可能な構成ファイルから属性の現在の値を取得するために使用できます。 プロパティは、 <xref:System.Net.Configuration.SmtpNetworkElement.Password%2A?displayProperty=nameWithType> `password` 適用可能な構成ファイルから属性の現在の値を取得するために使用できます。 `password`通常、セキュリティ上の理由から、属性を構成ファイルに入力することはできません。  
  
 属性は、 `clientDomain` smtp プロトコルの初期要求で使用されるクライアントのドメイン名を smtp サーバーに変更します。 属性は、 `clientDomain` 既定で使用される localhost 名ではなく、ローカルコンピューターの完全修飾ドメイン名に設定できます。 これにより、SMTP プロトコル標準への準拠が向上します。 既定値は、要求を送信しているローカルコンピューターの localhost 名です。 プロパティは、 <xref:System.Net.Configuration.SmtpNetworkElement.ClientDomain%2A?displayProperty=nameWithType> `clientDomain` 適用可能な構成ファイルから属性の現在の値を取得するために使用できます。  
  
 `targetName`拡張保護を使用する場合、この属性は認証に使用されます。 既定値は "SMTPSVC/" の形式です \<host> 。ここ \<host> で、は SMTP メールサーバーのホスト名です。 プロパティは、 <xref:System.Net.Configuration.SmtpNetworkElement.TargetName%2A?displayProperty=nameWithType> `targetName` 適用可能な構成ファイルから属性の現在の値を取得するために使用できます。  
  
 属性では、 `enableSsl` SMTP メールサーバーへのアクセスに SSL を使用するかどうかを指定します。 クラスでサポートされているのは、 <xref:System.Net.Mail.SmtpClient?displayProperty=nameWithType> RFC 3207 で定義されているトランスポート層セキュリティ経由の SECURE smtp に対する Smtp サービス拡張のみです。 このモードでは、暗号化されていないチャネルで SMTP セッションが開始され、SSL を使用してセキュリティで保護された通信に切り替えるために、クライアントからサーバーに STARTTLS コマンドが発行されます。 詳細については、インターネット技術標準化委員会 (IETF) によって発行された RFC 3207 を参照してください。  
  
 代替の接続方法では、プロトコルコマンドが送信される前に、SSL セッションが事前に確立されます。 この接続方法は SMTPS とも呼ばれ、既定ではポート465を使用します。 SSL を使用したこの代替接続方法は、現在サポートされていません。  
  
 プロパティは、 <xref:System.Net.Configuration.SmtpNetworkElement.EnableSsl%2A?displayProperty=nameWithType> `enableSsl` 適用可能な構成ファイルから属性の現在の値を取得するために使用できます。  
  
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
