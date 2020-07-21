---
title: '方法: セキュリティで保護されたセッションを作成する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- security [WCF], creating a session
ms.assetid: b6f42b5a-bbf7-45cf-b917-7ec9fa7ae110
ms.openlocfilehash: 80973a31050cf1ede03d4a3919066c62625ae590
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84593413"
---
# <a name="how-to-create-a-secure-session"></a>方法: セキュリティで保護されたセッションを作成する
バインディングを除き、 [\<basicHttpBinding>](../../configure-apps/file-schema/wcf/basichttpbinding.md) Windows Communication Foundation (WCF) のシステム指定のバインディングでは、メッセージセキュリティが有効になっている場合、セキュリティで保護されたセッションが自動的に使用されます。  
  
 既定では、セキュリティで保護されたセッションは、再利用される Web サーバーで存続します。 セキュリティで保護されたセッションが確立されると、クライアントとサービスが、セキュリティで保護されたセッションに関連付けられているキーをキャッシュします。 メッセージを交換するときは、キャッシュされたキーの識別子のみが交換されます。 Web サーバーが再利用される場合は、Web サーバーが識別子のキャッシュされたキーを取得できないようにキャッシュも再利用されます。 これが発生した場合、例外がクライアントにスローされます。 ステートフルなセキュリティ コンテキスト トークン (SCT: Security Context Token) を使用するセキュリティで保護されたセッションは、再利用される Web サーバーで存続することができます。 セキュリティで保護されたセッションでのステートフルな SCT の使用の詳細については、「[方法: セキュリティで保護されたセッションのセキュリティコンテキストトークンを作成](how-to-create-a-security-context-token-for-a-secure-session.md)する」を参照してください。  
  
### <a name="to-specify-that-a-service-uses-secure-sessions-by-using-one-of-the-system-provided-bindings"></a>サービスが、システム提供のバインディングの 1 つを使用して、セキュリティで保護されたセッションを使用するように指定するには  
  
- メッセージ セキュリティをサポートするシステム提供のバインディングを使用するようにサービスを構成します。  
  
     バインディングを除き、 [\<basicHttpBinding>](../../configure-apps/file-schema/wcf/basichttpbinding.md) システム指定のバインディングがメッセージセキュリティを使用するように構成されている場合、WCF は自動的にセキュリティで保護されたセッションを使用します。 次の表は、メッセージ セキュリティをサポートするシステム提供のバインディングを示し、そのバインディングでメッセージ セキュリティが既定のセキュリティ機構であるかどうかを示しています。  
  
    |システム提供のバインディング|構成要素|既定でメッセージ セキュリティが有効|  
    |------------------------------|---------------------------|------------------------------------|  
    |<xref:System.ServiceModel.BasicHttpBinding>|[\<basicHttpBinding>](../../configure-apps/file-schema/wcf/basichttpbinding.md)|いいえ|  
    |<xref:System.ServiceModel.WSHttpBinding>|[\<wsHttpBinding>](../../configure-apps/file-schema/wcf/wshttpbinding.md)|はい|  
    |<xref:System.ServiceModel.WSDualHttpBinding>|[\<wsDualHttpBinding>](../../configure-apps/file-schema/wcf/wsdualhttpbinding.md)|はい|  
    |<xref:System.ServiceModel.WSFederationHttpBinding>|[\<wsFederationHttpBinding>](../../configure-apps/file-schema/wcf/wsfederationhttpbinding.md)|はい|  
    |<xref:System.ServiceModel.NetTcpBinding>|[\<netTcpBinding>](../../configure-apps/file-schema/wcf/nettcpbinding.md)|いいえ|  
    |<xref:System.ServiceModel.NetMsmqBinding>|[\<netMsmqBinding>](../../configure-apps/file-schema/wcf/netmsmqbinding.md)|いいえ|  
  
     次のコード例では、構成を使用して、 `wsHttpBinding_Calculator` [\<wsHttpBinding>](../../configure-apps/file-schema/wcf/wshttpbinding.md) 、メッセージセキュリティ、およびセキュリティで保護されたセッションを使用するという名前のバインディングを指定します。  
  
    ```xml  
    <bindings>  
      <WSHttpBinding>  
       <binding name = "wsHttpBinding_Calculator">  
         <security mode="Message">  
           <message clientCredentialType="Windows"/>  
         </security>  
        </binding>  
      </WSHttpBinding>  
    </bindings>  
    ```  
  
     次のコード例では、、メッセージセキュリティ、およびセキュリティで保護されたセッションを使用してサービスをセキュリティで保護するように指定してい [\<wsHttpBinding>](../../configure-apps/file-schema/wcf/wshttpbinding.md) `secureCalculator` ます。  
  
     [!code-csharp[c_CreateSecureSession#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_createsecuresession/cs/secureservice.cs#1)]
     [!code-vb[c_CreateSecureSession#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_createsecuresession/vb/secureservice.vb#1)]  
  
    > [!NOTE]
    > では、 [\<wsHttpBinding>](../../configure-apps/file-schema/wcf/wshttpbinding.md) 属性をに設定することによって、セキュリティで保護されたセッションを無効にすることができます `establishSecurityContext` `false` 。 他のシステム提供のバインディングについては、カスタム バインドを作成することでのみ、セキュリティで保護されたセッションを無効にできます。  
  
### <a name="to-specify-that-a-service-uses-secure-sessions-by-using-a-custom-binding"></a>カスタム バインドを使用して、サービスでセキュリティで保護されたセッションが使用されるように指定するには  
  
- セキュリティで保護されたセッションで SOAP メッセージが保護されるように指定したカスタム バインドを作成します。  
  
     カスタムバインディングの作成の詳細については、「[方法: システム指定のバインディングをカスタマイズ](../extending/how-to-customize-a-system-provided-binding.md)する」を参照してください。  
  
     次のコード例で使用されている構成では、セキュリティで保護されたセッションを使用して SOAP メッセージを保護するカスタム バインドを指定しています。  
  
    ```xml  
    <bindings>  
      <!-- configure a custom binding -->  
      <customBinding>  
        <binding name="customBinding_Calculator">  
          <security authenticationMode="SecureConversation" />  
          <secureConversationBootstrap authenticationMode="SspiNegotiated" />  
          <textMessageEncoding messageVersion="Soap12WSAddressing10" writeEncoding="utf-8"/>  
          <httpTransport/>  
        </binding>  
      </customBinding>  
    </bindings>  
    ```  
  
     セキュリティで保護されたセッションをブートストラップするための <xref:System.ServiceModel.Configuration.AuthenticationMode.MutualCertificate> 認証モードを使用する、カスタム バインドを作成するコード例を次に示します。  
  
     [!code-csharp[c_CreateSecureSession#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_createsecuresession/cs/secureservice.cs#2)]
     [!code-vb[c_CreateSecureSession#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_createsecuresession/vb/secureservice.vb#2)]  
  
## <a name="see-also"></a>関連項目

- [WCF のバインディングの概要](../bindings-overview.md)
