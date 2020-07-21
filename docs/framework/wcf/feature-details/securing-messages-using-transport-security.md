---
title: トランスポート セキュリティを使用したメッセージのセキュリティ保護
ms.date: 03/30/2017
ms.assetid: 9029771a-097e-448a-a13a-55d2878330b8
ms.openlocfilehash: 7d160f6f0d1d29e34ca3365501b86d1a736de67b
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84589943"
---
# <a name="securing-messages-using-transport-security"></a>トランスポート セキュリティを使用したメッセージのセキュリティ保護
ここでは、キューに送信されるメッセージをセキュリティで保護するために使用できるメッセージ キュー (MSMQ) トランスポート セキュリティについて説明します。  
  
> [!NOTE]
> このトピックを読む前に、「[セキュリティの概念](security-concepts.md)」を読むことをお勧めします。  
  
 次の図は、Windows Communication Foundation (WCF) を使用したキュー通信の概念モデルを示しています。 この図および用語を使用して、トランスポート セキュリティの概念について解説します。  
  
 ![キューに置かれたアプリケーションの図](media/distributed-queue-figure.jpg "配信キュー図")  
  
 WCF を使用してキューに置かれたメッセージをと共に送信する場合 <xref:System.ServiceModel.NetMsmqBinding> 、wcf メッセージは MSMQ メッセージの本文として添付されます。 トランスポート セキュリティは、MSMQ メッセージ全体 (MSMQ メッセージ ヘッダーまたはプロパティ、およびメッセージ本文) をセキュリティで保護します。 MSMQ メッセージの本文であるため、トランスポートセキュリティを使用すると、WCF メッセージも保護されます。  
  
 トランスポート セキュリティの背後にある重要な概念は、メッセージがターゲット キューに到達するためには、クライアントがセキュリティ要件を満たす必要があるという点です。 これは、メッセージ セキュリティとは異なります。メッセージ セキュリティでは、メッセージを受信するアプリケーションに対してメッセージが保護されます。  
  
 <xref:System.ServiceModel.NetMsmqBinding> と <xref:System.ServiceModel.MsmqIntegration.MsmqIntegrationBinding> を使用するトランスポート セキュリティは、転送キューとターゲット キュー間を移動している MSMQ メッセージがセキュリティで保護される方法に影響します。この場合、"セキュリティで保護される" とは次のことを意味します。  
  
- メッセージが改ざんされないように、メッセージに署名する。  
  
- メッセージが読み取られたり、改ざんされたりしないしないように、メッセージを暗号化する。 これは推奨事項ですが、必須ではありません。  
  
- 否認防止のため、ターゲット キュー マネージャーがメッセージの送信者を識別する。  
  
 MSMQ では、認証とは別に、ターゲット キューがアクセス制御リスト (ACL: Access Control List) を持っており、これで、ターゲット キューにメッセージを送信するためのアクセス許可がクライアントに与えられているどうかをチェックします。 ターゲット キューからメッセージを受信するためのアクセス許可があるかどうかのチェックは、受信側のアプリケーションに対しても行われます。  
  
## <a name="wcf-msmq-transport-security-properties"></a>WCF MSMQ トランスポート セキュリティのプロパティ  
 MSMQ では、Windows セキュリティを使用して認証を行います。 Windows セキュリティは、Windows セキュリティ識別子 (SID: Security Identifier) を使用してクライアントを識別し、クライアントの認証時に、証明機関として Active Directory ディレクトリ サービスを使用します。 このため、MSMQ を Active Directory 統合と共にインストールする必要があります。 クライアントの識別には Windows ドメインの SID が使用されるため、このセキュリティ オプションは、クライアントとサービスの両方が同じ Windows ドメインに属している場合にのみ有効です。  
  
 また、MSMQ は、Active Directory に登録されていないメッセージに証明書を添付する機能も提供します。 この場合は、添付された証明書を使用してメッセージが署名されたことが保証されます。  
  
 WCF では、これらのオプションの両方が MSMQ トランスポートセキュリティの一部として提供されており、トランスポートセキュリティの主要なピボットです。  
  
 既定では、トランスポート セキュリティが有効になります。  
  
 これらの基本事項に基づいて、以降のセクションでは <xref:System.ServiceModel.NetMsmqBinding> および <xref:System.ServiceModel.MsmqIntegration.MsmqIntegrationBinding> に結び付けられたトランスポート セキュリティのプロパティについて詳しく説明します。  
  
#### <a name="msmq-authentication-mode"></a>MSMQ 認証モード  
 <xref:System.ServiceModel.MsmqTransportSecurity.MsmqAuthenticationMode%2A> は、Windows ドメインのセキュリティと外部の証明書ベースのセキュリティのどちらを使用してメッセージを保護するかを決定します。 どちらの認証モードでも、WCF のキューに置かれたトランスポートチャネルは、 `CertificateValidationMode` サービス構成で指定されたを使用します。 証明書検証モードは、証明書の有効性を確認するために使用される機構を指定します。  
  
 トランスポート セキュリティが有効になっている場合、既定の設定は <xref:System.ServiceModel.MsmqAuthenticationMode.WindowsDomain> です。  
  
#### <a name="windows-domain-authentication-mode"></a>Windows ドメイン認証モード  
 Windows セキュリティを選択した場合は、Active Directory 統合が必要となります。 <xref:System.ServiceModel.MsmqAuthenticationMode.WindowsDomain> が既定のトランスポート セキュリティ モードです。 これが設定されると、WCF チャネルは MSMQ メッセージに Windows SID をアタッチし、Active Directory から取得した内部証明書を使用します。 MSMQ は、この内部証明書を使用してメッセージをセキュリティで保護します。 受信側キュー マネージャーは、Active Directory を使用して一致する証明書を検索し、クライアントを認証します。また、SID がクライアントの SID と一致するかどうかをチェックします。 この認証手順は、認証を要求するようにターゲット キューがマークされていない場合でも、内部的 (`WindowsDomain` 認証モードの場合) または外部的 (`Certificate` 認証モードの場合) に生成された証明書がメッセージに添付されているときに実行されます。  
  
> [!NOTE]
> キューを作成する際に認証キューとしてマークすることにより、そのキューにメッセージを送信するクライアントに対して認証を求めることができます。 これにより、認証されたメッセージだけをキューに受け入れることができます。  
  
 また、メッセージに添付された SID は、キューにメッセージを送信する権限をクライアントが持つことを確認するためにターゲット キューの ACL をチェックする目的でも使用されます。  
  
#### <a name="certificate-authentication-mode"></a>証明書認証モード  
 証明書認証モードを選択した場合は、Active Directory 統合をインストールする必要がありません。 実際、(Active Directory 統合をインストールせずに) MSMQ をワークグループ モードでインストールしている場合や、SOAP リライアブル メッセージ プロトコル (SRMP: SOAP Reliable Messaging Protocol) 転送プロトコルを使用してメッセージをキューに送信する場合など、<xref:System.ServiceModel.MsmqAuthenticationMode.Certificate> だけが機能するというケースもあります。  
  
 Wcf メッセージをと共に送信する場合、 <xref:System.ServiceModel.MsmqAuthenticationMode.Certificate> wcf チャネルは MSMQ メッセージに WINDOWS SID を添付しません。 そのため、ターゲット キューの ACL は、キューへの送信に対して `Anonymous` ユーザー アクセスを許可する必要があります。 受信側キュー マネージャーは、証明書を使用して MSMQ メッセージが署名されたかどうかをチェックしますが、認証は行いません。  
  
 クレームと id 情報を含む証明書は、WCF の <xref:System.ServiceModel.ServiceSecurityContext> キューに置かれたトランスポートチャネルによってに設定されます。 サービスは、この情報を使用して独自の方式で送信者の認証を行います。  
  
### <a name="msmq-protection-level"></a>MSMQ の保護レベル  
 保護レベルは、MSMQ メッセージが改ざんされないように MSMQ メッセージを保護する方法を決定します。 これは、<xref:System.ServiceModel.MsmqTransportSecurity.MsmqProtectionLevel%2A> プロパティで指定します。 既定値は <xref:System.Net.Security.ProtectionLevel.Sign> です。  
  
#### <a name="sign-protection-level"></a>署名による保護レベル  
 MSMQ メッセージでは、`WindowsDomain` 認証モードを使用する場合は内部生成された証明書を使用して署名され、`Certificate` 認証モードを使用する場合は、外部生成された証明書を使用して署名されます。  
  
#### <a name="sign-and-encrypt-protection-level"></a>署名と暗号化による保護レベル  
 MSMQ メッセージでは、`WindowsDomain` 認証モードを使用する場合は内部生成された証明書を使用して署名され、`Certificate` 認証モードを使用する場合は、外部生成された証明書を使用して署名されます。  
  
 メッセージの署名に加えて、MSMQ メッセージは、ターゲット キューをホストする受信側キュー マネージャーに属する Active Directory から取得した証明書の公開キーを使用して暗号化されます。 送信側キュー マネージャーは、MSMQ メッセージが送信時に暗号化されているかどうかを確認します。 受信側キュー マネージャーは、内部証明書の秘密キーを使用して MSMQ メッセージを復号化し、クリア テキストでメッセージをキューに格納します (認証と承認が完了している場合)。  
  
> [!NOTE]
> メッセージを暗号化するには、Active Directory にアクセスでき (`UseActiveDirectory` の <xref:System.ServiceModel.NetMsmqBinding> プロパティが `true` に設定されている)、かつ <xref:System.ServiceModel.MsmqAuthenticationMode.Certificate> と <xref:System.ServiceModel.MsmqAuthenticationMode.WindowsDomain> の両方で Active Directory を使用できる必要があります。  
  
#### <a name="none-protection-level"></a>保護のないレベル  
 <xref:System.ServiceModel.MsmqTransportSecurity.MsmqProtectionLevel%2A> を <xref:System.Net.Security.ProtectionLevel.None> に設定することにより指定されます。 この値は、他の認証モードに対しては無効です。  
  
> [!NOTE]
> MSMQ メッセージが署名されている場合は、キューの状態 (つまり、認証キューであるかどうか) に関係なく、添付されている (内部または外部) 証明書を使用してメッセージが署名されているかどうかがチェックされます。  
  
### <a name="msmq-encryption-algorithm"></a>MSMQ の暗号化アルゴリズム  
 暗号化アルゴリズムは、ネットワーク上の MSMQ メッセージを暗号化するために使用されるアルゴリズムを指定します。 このプロパティは、<xref:System.ServiceModel.MsmqTransportSecurity.MsmqProtectionLevel%2A> を <xref:System.Net.Security.ProtectionLevel.EncryptAndSign> に設定している場合にのみ使用します。  
  
 サポートされているアルゴリズムは `RC4Stream` と `AES` で、既定値は `RC4Stream` です。  
  
 `AES` アルゴリズムは、送信元が MSMQ 4.0 以降をインストールしている場合にのみ使用できます。 また、ターゲット キューも MSMQ 4.0 でホストされている必要があります。  
  
### <a name="msmq-hash-algorithm"></a>MSMQ ハッシュ アルゴリズム  
 ハッシュ アルゴリズムは、MSMQ メッセージのデジタル署名を作成するために使用されるアルゴリズムを指定します。 受信側キュー マネージャーも、これと同じアルゴリズムを使用して MSMQ メッセージを認証します。 このプロパティは、<xref:System.ServiceModel.MsmqTransportSecurity.MsmqProtectionLevel%2A> が <xref:System.Net.Security.ProtectionLevel.Sign> または <xref:System.Net.Security.ProtectionLevel.EncryptAndSign> に設定されている場合にのみ使用されます。  
  
 サポートされるアルゴリズムは、`MD5`、`SHA1`、`SHA256`、および `SHA512` です。 既定値は、`SHA1` です。

 MD5/SHA1 の衝突の問題のため、SHA256 以上をお勧めします。
  
## <a name="see-also"></a>関連項目

- [キューの概要](queues-overview.md)
- [セキュリティの概念](security-concepts.md)
- [サービスおよびクライアントのセキュリティ保護](securing-services-and-clients.md)
