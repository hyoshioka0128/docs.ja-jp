---
title: '方法: トランスポート セキュリティとメッセージ資格情報を使用する'
description: メッセージ資格情報を使用してトランスポートセキュリティを実装する方法について説明します。これにより、WCF でトランスポートとメッセージのセキュリティモードが最適になります。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- TransportWithMessageCredentials
ms.assetid: 6cc35346-c37a-4859-b82b-946c0ba6e68f
ms.openlocfilehash: f632a4389eafc155cedcae94707c9418b6696f2c
ms.sourcegitcommit: 358a28048f36a8dca39a9fe6e6ac1f1913acadd5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85246650"
---
# <a name="how-to-use-transport-security-and-message-credentials"></a>方法: トランスポート セキュリティとメッセージ資格情報を使用する
トランスポートとメッセージの両方の資格情報を使用してサービスをセキュリティ保護するには、Windows Communication Foundation (WCF) のトランスポートとメッセージの両方のセキュリティモードを使用します。 つまり、トランスポート層セキュリティでは整合性と機密性が提供され、メッセージ層セキュリティでは、厳密なトランスポート セキュリティ機構では実現できないさまざまな資格情報が提供されます。 ここでは、<xref:System.ServiceModel.WSHttpBinding> バインディングと <xref:System.ServiceModel.NetTcpBinding> バインディングを使用して、メッセージ資格情報付きトランスポートを実装するための基本手順を示します。 セキュリティモードの設定の詳細については、「[方法: セキュリティモードを設定する](../how-to-set-the-security-mode.md)」を参照してください。  
  
 セキュリティ モードを `TransportWithMessageCredential` に設定した場合、トランスポート レベルのセキュリティを提供する実際の機構はトランスポートによって決まります。 この機構は、HTTP の場合は SSL (Secure Sockets Layer) over HTTP (HTTPS)、TCP の場合は SSL over TCP または Windows です。  
  
 トランスポートが HTTP (<xref:System.ServiceModel.WSHttpBinding> を使用) の場合は、トランスポート レベルのセキュリティが SSL over HTTP によって提供されます。 この場合、このトピックで後述するように、ポートにバインドされた SSL 証明書を使用してサービスをホストするコンピューターを構成する必要があります。  
  
 トランスポートが TCP (<xref:System.ServiceModel.NetTcpBinding> を使用) の場合、既定では、Windows セキュリティ または SSL over TCP によってトランスポート レベルのセキュリティが提供されます。 SSL over TCP を使用する場合は、このトピックで後述するように、<xref:System.ServiceModel.Security.X509CertificateRecipientServiceCredential.SetCertificate%2A> メソッドを使用して証明書を指定する必要があります。  
  
### <a name="to-use-the-wshttpbinding-with-a-certificate-for-transport-security-in-code"></a>WSHttpBinding と証明書を使用してトランスポート セキュリティを提供するには (コードを使用する場合)  
  
1. HttpCfg.exe ツールを使用して、コンピューターの任意のポートに SSL 証明書をバインドします。 詳細については、「[方法: SSL 証明書を使用してポートを構成する](how-to-configure-a-port-with-an-ssl-certificate.md)」を参照してください。  
  
2. <xref:System.ServiceModel.WSHttpBinding> クラスのインスタンスを作成し、<xref:System.ServiceModel.WSHttpSecurity.Mode%2A> プロパティを <xref:System.ServiceModel.SecurityMode.TransportWithMessageCredential> に設定します。  
  
3. <xref:System.ServiceModel.HttpTransportSecurity.ClientCredentialType%2A> プロパティに適切な値を設定します。 (詳細については、「[資格情報の種類の選択](selecting-a-credential-type.md)」を参照してください)。次のコードでは、値を使用し <xref:System.ServiceModel.MessageCredentialType.Certificate> ます。  
  
4. 適切なベース アドレスを持つ <xref:System.Uri> クラスのインスタンスを作成します。 このアドレスでは、"HTTPS" スキームを使用し、コンピューターの実際の名前と SSL 証明書のバインド先のポート番号を含める必要があります。 (または、構成で基本アドレスを設定できます。)  
  
5. <xref:System.ServiceModel.ServiceHost.AddServiceEndpoint%2A> メソッドを使用してサービス エンドポイントを追加します。  
  
6. <xref:System.ServiceModel.ServiceHost> のインスタンスを作成し、<xref:System.ServiceModel.ICommunicationObject.Open%2A> メソッドを呼び出します。コードは次のようになります。  
  
     [!code-csharp[c_SettingSecurityMode#7](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_settingsecuritymode/cs/source.cs#7)]
     [!code-vb[c_SettingSecurityMode#7](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_settingsecuritymode/vb/source.vb#7)]  
  
### <a name="to-use-the-nettcpbinding-with-a-certificate-for-transport-security-in-code"></a>NetTcpBinding と証明書を使用してトランスポート セキュリティを提供するには (コードを使用する場合)  
  
1. <xref:System.ServiceModel.NetTcpBinding> クラスのインスタンスを作成し、<xref:System.ServiceModel.NetTcpSecurity.Mode%2A> プロパティを <xref:System.ServiceModel.SecurityMode.TransportWithMessageCredential> に設定します。  
  
2. <xref:System.ServiceModel.MessageSecurityOverTcp.ClientCredentialType%2A> を適切な値に設定します。 次のコードでは、<xref:System.ServiceModel.MessageCredentialType.Certificate> 値を使用しています。  
  
3. 適切なベース アドレスを持つ <xref:System.Uri> クラスのインスタンスを作成します。 アドレスには "net.tcp" スキーマを使用する必要があることに注意してください。 (または、構成で基本アドレスを設定できます。)  
  
4. <xref:System.ServiceModel.ServiceHost> クラスのインスタンスを作成します。  
  
5. <xref:System.ServiceModel.Security.X509CertificateRecipientServiceCredential.SetCertificate%2A> クラスの <xref:System.ServiceModel.Security.X509CertificateRecipientServiceCredential> メソッドを使用して、サービスに X.509 資格情報を明示的に設定します。  
  
6. <xref:System.ServiceModel.ServiceHost.AddServiceEndpoint%2A> メソッドを使用してサービス エンドポイントを追加します。  
  
7. 次のコードに示すように、<xref:System.ServiceModel.ICommunicationObject.Open%2A> メソッドを呼び出します。  
  
     [!code-csharp[c_SettingSecurityMode#8](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_settingsecuritymode/cs/source.cs#8)]
     [!code-vb[c_SettingSecurityMode#8](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_settingsecuritymode/vb/source.vb#8)]  
  
### <a name="to-use-the-nettcpbinding-with-windows-for-transport-security-in-code"></a>NetTcpBinding と Windows を使用してトランスポート セキュリティを提供するには (コードを使用する場合)  
  
1. <xref:System.ServiceModel.NetTcpBinding> クラスのインスタンスを作成し、<xref:System.ServiceModel.NetTcpSecurity.Mode%2A> プロパティを <xref:System.ServiceModel.SecurityMode.TransportWithMessageCredential> に設定します。  
  
2. トランスポート セキュリティが Windows を使用するように、<xref:System.ServiceModel.TcpTransportSecurity.ClientCredentialType%2A> を <xref:System.ServiceModel.TcpClientCredentialType.Windows> に設定します  (これは、既定の設定です)。  
  
3. <xref:System.ServiceModel.MessageSecurityOverTcp.ClientCredentialType%2A> を適切な値に設定します。 次のコードでは、<xref:System.ServiceModel.MessageCredentialType.Certificate> 値を使用しています。  
  
4. 適切なベース アドレスを持つ <xref:System.Uri> クラスのインスタンスを作成します。 アドレスには "net.tcp" スキーマを使用する必要があることに注意してください。 (または、構成で基本アドレスを設定できます。)  
  
5. <xref:System.ServiceModel.ServiceHost> クラスのインスタンスを作成します。  
  
6. <xref:System.ServiceModel.Security.X509CertificateRecipientServiceCredential.SetCertificate%2A> クラスの <xref:System.ServiceModel.Security.X509CertificateRecipientServiceCredential> メソッドを使用して、サービスに X.509 資格情報を明示的に設定します。  
  
7. <xref:System.ServiceModel.ServiceHost.AddServiceEndpoint%2A> メソッドを使用してサービス エンドポイントを追加します。  
  
8. 次のコードに示すように、<xref:System.ServiceModel.ICommunicationObject.Open%2A> メソッドを呼び出します。  
  
     [!code-csharp[c_SettingSecurityMode#9](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_settingsecuritymode/cs/source.cs#9)]
     [!code-vb[c_SettingSecurityMode#9](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_settingsecuritymode/vb/source.vb#9)]  
  
## <a name="using-configuration"></a>構成の使用  
  
#### <a name="to-use-the-wshttpbinding"></a>WSHttpBinding を使用するには  
  
1. ポートにバインドされた SSL 証明書を使用してコンピューターを構成します  (詳細については、「[方法: SSL 証明書を使用してポートを構成する](how-to-configure-a-port-with-an-ssl-certificate.md)」を参照してください)。 この構成で <> 要素の値を設定する必要はありません `transport` 。  
  
2. メッセージ レベルのセキュリティのクライアント資格情報の種類を指定します。 次の例では、 `clientCredentialType` <`message`> 要素の属性をに設定 `UserName` します。  
  
    ```xml  
    <wsHttpBinding>  
    <binding name="WsHttpBinding_ICalculator">  
            <security mode="TransportWithMessageCredential" >  
               <message clientCredentialType="UserName" />  
            </security>  
    </binding>  
    </wsHttpBinding>  
    ```  
  
#### <a name="to-use-the-nettcpbinding-with-a-certificate-for-transport-security"></a>NetTcpBinding と証明書を使用してトランスポート セキュリティを提供するには  
  
1. SSL over TCP の場合、`<behaviors>` 要素内で証明書を明示的に指定する必要があります。 既定のストアの場所 (ローカル コンピューターの個人ストア) にある証明書を、発行者で指定する例を次に示します。  
  
    ```xml  
    <behaviors>  
     <serviceBehaviors>  
       <behavior name="mySvcBehavior">  
           <serviceCredentials>  
             <serviceCertificate findValue="contoso.com"  
                                 x509FindType="FindByIssuerName" />  
           </serviceCredentials>  
       </behavior>  
     </serviceBehaviors>  
    </behaviors>  
    ```  
  
2. [\<netTcpBinding>](../../configure-apps/file-schema/wcf/nettcpbinding.md)バインドセクションにを追加します  
  
3. バインド要素を追加して、`name` 属性を適切な値に設定します。  
  
4. <`security`> 要素を追加し、 `mode` 属性をに設定し `TransportWithMessageCredential` ます。  
  
5. <要素を追加 `message>` し、 `clientCredentialType` 属性を適切な値に設定します。  
  
    ```xml  
    <bindings>  
    <netTcpBinding>  
      <binding name="myTcpBinding">  
        <security mode="TransportWithMessageCredential" >  
           <message clientCredentialType="Windows" />  
        </security>  
      </binding>  
    </netTcpBinding>  
    </bindings>  
    ```  
  
#### <a name="to-use-the-nettcpbinding-with-windows-for-transport-security"></a>NetTcpBinding と Windows を使用してトランスポート セキュリティを提供するには  
  
1. バインドセクションにを追加します。 [\<netTcpBinding>](../../configure-apps/file-schema/wcf/nettcpbinding.md)  
  
2. <`binding`> 要素を追加し、 `name` 属性を適切な値に設定します。  
  
3. <`security`> 要素を追加し、 `mode` 属性をに設定し `TransportWithMessageCredential` ます。  
  
4. <`transport`> 要素を追加し、 `clientCredentialType` 属性をに設定し `Windows` ます。  
  
5. <`message`> 要素を追加し、 `clientCredentialType` 属性を適切な値に設定します。 次のコードは、値を証明書に設定します。  
  
    ```xml  
    <bindings>  
    <netTcpBinding>  
      <binding name="myTcpBinding">  
        <security mode="TransportWithMessageCredential" >  
           <transport clientCredentialType="Windows" />  
           <message clientCredentialType="Certificate" />  
        </security>  
      </binding>  
    </netTcpBinding>  
    </bindings>  
    ```  
  
## <a name="see-also"></a>関連項目

- [方法: セキュリティ モードを設定する](../how-to-set-the-security-mode.md)
- [サービスのセキュリティ保護](../securing-services.md)
- [サービスおよびクライアントのセキュリティ保護](securing-services-and-clients.md)
