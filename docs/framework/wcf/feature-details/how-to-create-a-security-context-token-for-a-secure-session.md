---
title: '方法: セキュリティで保護されたセッションに対しセキュリティ コンテキスト トークンを作成する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 640676b6-c75a-4ff7-aea4-b1a1524d71b2
ms.openlocfilehash: 36cf5ce1aa6e0eef80123ac7008294062d7faf82
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84598906"
---
# <a name="how-to-create-a-security-context-token-for-a-secure-session"></a>方法: セキュリティで保護されたセッションに対しセキュリティ コンテキスト トークンを作成する
セキュリティで保護されたセッションでステートフルなセキュリティ コンテキスト トークン (SCT: Security Context Token) を使用すると、そのセッションでサービスを再利用できます。 たとえば、セキュリティで保護されたセッションでステートレスな SCT を使用しているときにインターネット インフォメーション サービス (IIS) をリセットすると、サービスに関連付けられているセッション データが失われます。 このセッション データには、SCT キャッシュが含まれています。 このため、クライアントが次回ステートレスな SCT をサービスに送信すると、エラーが返されます。これは、SCT に関連付けられているキーを取得できないためです。 しかし、ステートフルな SCT を使用した場合、SCT に関連付けられているキーは、その SCT 内に格納されます。 キーが SCT 内、つまりメッセージ内に格納されているため、セキュリティで保護されたセッションは、サービスの再使用の影響を受けません。 既定では、Windows Communication Foundation (WCF) は、セキュリティで保護されたセッションでステートレスな SCTs を使用します。 ここでは、セキュリティで保護されたセッションでステートフルな SCT を使用する方法について詳しく説明します。  
  
> [!NOTE]
> <xref:System.ServiceModel.Channels.IDuplexChannel> から派生したコントラクトに関係する、セキュリティで保護されたセッションでは、ステートフルな SCT を使用できません。  
  
> [!NOTE]
> セキュリティで保護されたセッションでステートフルな SCT を使用するアプリケーションでは、サービスのスレッド ID は、関連付けられたユーザー プロファイルを持つユーザー アカウントである必要があります。 ユーザー プロファイルを持たないアカウント (`Local Service` など) でサービスを実行すると、例外がスローされる場合があります。  
  
> [!NOTE]
> Windows XP で偽装が必要な場合は、ステートフルな SCT を使用しない、セキュリティで保護されたセッションを使用します。 ステートフル SCT が偽装と共に使用されると、<xref:System.InvalidOperationException> がスローされます。 詳細については、「サポートされ[ないシナリオ](unsupported-scenarios.md)」を参照してください。  
  
### <a name="to-use-stateful-scts-in-a-secure-session"></a>セキュリティで保護されたセッションでステートフルな SCT を使用するには  
  
- ステートフルな SCT を使用する、セキュリティで保護されたセッションによって SOAP メッセージを保護するように指定するカスタム バインディングを作成します。  
  
    1. サービスの構成ファイルにを追加することによって、カスタムバインディングを定義し [\<customBinding>](../../configure-apps/file-schema/wcf/custombinding.md) ます。  
  
        ```xml  
        <customBinding>  
        </customBinding>
        ```  
  
    2. [\<binding>](../../configure-apps/file-schema/wcf/bindings.md)に子要素を追加 [\<customBinding>](../../configure-apps/file-schema/wcf/custombinding.md) します。  
  
         `name` 属性を、構成ファイル内で一意の名前に設定してバンディング名を指定します。  
  
        ```xml  
        <binding name="StatefulSCTSecureSession">  
        </binding>
        ```  
  
    3. に子要素を追加して、このサービスとの間で送受信されるメッセージの認証モードを指定し [\<security>](../../configure-apps/file-schema/wcf/security-of-custombinding.md) [\<customBinding>](../../configure-apps/file-schema/wcf/custombinding.md) ます。  
  
         `authenticationMode` 属性を `SecureConversation` に設定して、セキュリティで保護されたセッションを指定します。 `requireSecurityContextCancellation` 属性を `false` に設定して、ステートフルな SCT を使用するように指定します。  
  
        ```xml  
        <security authenticationMode="SecureConversation"  
                  requireSecurityContextCancellation="false">
        </security>
        ```  
  
    4. に子要素を追加することによって、セキュリティで保護されたセッションを確立するときにクライアントを認証する方法を指定し [\<secureConversationBootstrap>](../../configure-apps/file-schema/wcf/secureconversationbootstrap.md) [\<security>](../../configure-apps/file-schema/wcf/security-of-custombinding.md) ます。  
  
         クライアントの認証方法は、`authenticationMode` 属性を設定して指定します。  
  
        ```xml  
        <secureConversationBootstrap authenticationMode="UserNameForCertificate" />  
        ```  
  
    5. などのエンコーディング要素を追加して、メッセージのエンコーディングを指定し [\<textMessageEncoding>](../../configure-apps/file-schema/wcf/textmessageencoding.md) ます。  
  
        ```xml  
        <textMessageEncoding />  
        ```  
  
    6. トランスポート要素 (など) を追加してトランスポートを指定し [\<httpTransport>](../../configure-apps/file-schema/wcf/httptransport.md) ます。  
  
        ```xml  
        <httpTransport />  
        ```  
  
     次のコード例では、構成を使用して、セキュリティで保護されたセッションでメッセージがステートフルな SCT と共に使用できるカスタム バインディングを指定します。  
  
    ```xml  
    <customBinding>  
      <binding name="StatefulSCTSecureSession">  
        <security authenticationMode="SecureConversation"  
                  requireSecurityContextCancellation="false">  
          <secureConversationBootstrap authenticationMode="UserNameForCertificate" />  
        </security>  
        <textMessageEncoding />  
        <httpTransport />  
      </binding>  
    </customBinding>  
    ```  
  
## <a name="example"></a>例  
 セキュリティで保護されたセッションをブートストラップするための <xref:System.ServiceModel.Configuration.AuthenticationMode.MutualCertificate> 認証モードを使用する、カスタム バインドを作成するコード例を次に示します。  
  
 [!code-csharp[c_CreateStatefulSCT#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_createstatefulsct/cs/secureservice.cs#2)]
 [!code-vb[c_CreateStatefulSCT#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_createstatefulsct/vb/secureservice.vb#2)]  
  
 Windows 認証をステートフルな SCT と組み合わせて使用する場合、WCF は、 <xref:System.ServiceModel.ServiceSecurityContext.WindowsIdentity%2A> プロパティに実際の呼び出し元の id を設定しません。代わりに、プロパティを anonymous に設定します。 WCF セキュリティでは、受信した SCT からのすべての要求に対してサービスセキュリティコンテキストの内容を再作成する必要があるため、サーバーはメモリ内のセキュリティセッションを追跡しません。 また、<xref:System.Security.Principal.WindowsIdentity> インスタンスは SCT にシリアル化できないため、<xref:System.ServiceModel.ServiceSecurityContext.WindowsIdentity%2A> プロパティは匿名 ID を返します。  
  
 次の構成は、この動作を示します。  
  
```xml  
<customBinding>  
  <binding name="Cancellation">  
       <textMessageEncoding />  
        <security
            requireSecurityContextCancellation="false">  
              <secureConversationBootstrap />  
        </security>  
    <httpTransport />  
  </binding>  
</customBinding>  
```  
  
## <a name="see-also"></a>関連項目

- [\<customBinding>](../../configure-apps/file-schema/wcf/custombinding.md)
