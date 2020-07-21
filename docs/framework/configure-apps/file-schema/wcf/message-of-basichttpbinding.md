---
title: <message> の <basicHttpBinding>
ms.date: 03/30/2017
ms.assetid: 51cdd329-6461-471a-8747-56c2299b61e5
ms.openlocfilehash: 748a734af8cf6767ce47cfffce9aec3ef627cb44
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "73736743"
---
# <a name="message-of-basichttpbinding"></a>\<message> の \<basicHttpBinding>
のメッセージレベルのセキュリティの設定を定義し [\<basicHttpBinding>](basichttpbinding.md) ます。  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<bindings>**](bindings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<basicHttpBinding>**](basichttpbinding.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<binding>**\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<security>**](security-of-basichttpbinding.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<message>**  
  
## <a name="syntax"></a>構文  
  
```xml  
<message algorithmSuite="Basic128/Basic192/Basic256/Basic128Rsa15/Basic256Rsa15/TripleDes/TripleDesRsa15/Basic128Sha256/Basic192Sha256/TripleDesSha256/Basic128Sha256Rsa15/Basic192Sha256Rsa15/Basic256Sha256Rsa15/TripleDesSha256Rsa15"
         clientCredentialType="UserName/Certificate" />
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|algorithmSuite|メッセージの暗号化とキー ラップ アルゴリズムを設定します。 この属性は、アルゴリズムとキー サイズを指定する <xref:System.ServiceModel.Security.SecurityAlgorithmSuite> 型です。 これらのアルゴリズムは、セキュリティ ポリシー言語 (WS-SecurityPolicy) 仕様で指定されたアルゴリズムにマップされます。<br /><br /> 既定値は `Basic256` です。|  
|clientCredentialType|メッセージ ベースのセキュリティを使用してクライアント認証を実行するときに使用される資格情報の種類を指定します。 既定値は、`UserName` です。|  
  
## <a name="clientcredentialtype-attribute"></a>clientCredentialType 属性  
  
|値|Description|  
|-----------|-----------------|  
|UserName|-クライアントがユーザー名資格情報を使用してサーバーに対して認証される必要があります。 この資格情報は、を使用して指定する必要があり [\<clientCredentials>](clientcredentials.md) ます。<br />-WCF では、パスワードダイジェストの送信や、パスワードを使用したキーの派生、およびメッセージセキュリティのためのこのようなキーの使用はサポートされていません。 そのため、ユーザー名の資格情報を使用する場合、WCF はトランスポートをセキュリティで保護するように強制します。 `basicHttpBinding` の場合は、SSL チャネルの設定が必要です。|  
|Certificate|証明書を使用してクライアントをサーバーに認証するように要求します。 この場合のクライアント資格情報は、およびを使用して指定する必要があり [\<clientCredentials>](clientcredentials.md) [\<clientCertificate>](clientcertificate-of-servicecredentials.md) ます。 さらに、メッセージのセキュリティ モードを使用する場合は、クライアントにサービス証明書を準備する必要があります。 この場合のサービス資格情報は <xref:System.ServiceModel.Description.ClientCredentials> 、クラスまたは動作要素を使用して指定し、を `ClientCredentials` 使用してサービス証明書を指定する必要があり [\<serviceCertificate>](servicecertificate-of-servicecredentials.md) ます。|  
  
### <a name="child-elements"></a>子要素  
 なし  
  
### <a name="parent-elements"></a>親要素  
  
|要素|Description|  
|-------------|-----------------|  
|[\<security>](security-of-basichttpbinding.md)|のセキュリティ機能を定義 [\<basicHttpBinding>](basichttpbinding.md) します。|  
  
## <a name="example"></a>例  
 このサンプルでは、basicHttpBinding とメッセージ セキュリティを使用するアプリケーションを実装する方法を示します。 サービスの次の構成例では、エンドポイント定義によって basicHttpBinding が指定され、`Binding1` という名前のバインディング構成が参照されます。 サービスがクライアントに対してサービス自体を認証するために使用する証明書は、`behaviors` 要素の下にある構成ファイルの `serviceCredentials` セクションで設定されます。 クライアントがサービスに対してクライアント自体を認証するために使用する証明書に適用される検証モードも、`behaviors` 要素の下にある `clientCertificate` セクションで設定されます。  
  
 同じバインディングとセキュリティの詳細が、クライアントの構成ファイルで指定されます。  
  
```xml  
<system.serviceModel>
  <services>
    <service name="Microsoft.ServiceModel.Samples.CalculatorService"
             behaviorConfiguration="CalculatorServiceBehavior">
      <host>
        <baseAddresses>
          <add baseAddress="http://localhost:8000/ServiceModelSamples/service" />
        </baseAddresses>
      </host>
      <!-- this endpoint is exposed at the base address provided by host: http://localhost:8000/ServiceModelSamples/service -->
      <endpoint address=""
                binding="basicHttpBinding"
                bindingConfiguration="Binding1"
                contract="Microsoft.ServiceModel.Samples.ICalculator" />
      <!-- the mex endpoint is exposed at http://localhost:8000/ServiceModelSamples/service/mex -->
      <endpoint address="mex"
                binding="mexHttpBinding"
                contract="IMetadataExchange" />
    </service>
  </services>
  <bindings>
    <basicHttpBinding>
    <!-- This configuration defines the SecurityMode as Message and
         the clientCredentialType as Certificate. -->
      <binding name="Binding1">
        <security mode = "Message">
          <message clientCredentialType="Certificate" />
        </security>
      </binding>
    </basicHttpBinding>
  </bindings>
  <!--For debugging purposes set the includeExceptionDetailInFaults attribute to true-->
  <behaviors>
    <serviceBehaviors>
      <behavior name="CalculatorServiceBehavior">
        <serviceMetadata httpGetEnabled="True" />
        <serviceDebug includeExceptionDetailInFaults="False" />
        <!-- The serviceCredentials behavior allows one to define a service certificate.
             A service certificate is used by a client to authenticate the service and provide message protection.
             This configuration references the "localhost" certificate installed during the setup instructions. -->
        <serviceCredentials>
          <serviceCertificate findValue="localhost"
                              storeLocation="LocalMachine"
                              storeName="My"
                              x509FindType="FindBySubjectName" />
          <clientCertificate>
            <!-- Setting the certificateValidationMode to PeerOrChainTrust means that if the certificate
               is in the user's Trusted People store, then it will be trusted without performing a
               validation of the certificate's issuer chain. This setting is used here for convenience so that the
               sample can be run without having to have certificates issued by a certification authority (CA).
               This setting is less secure than the default, ChainTrust. The security implications of this
               setting should be carefully considered before using PeerOrChainTrust in production code. -->
            <authentication certificateValidationMode="PeerOrChainTrust" />
          </clientCertificate>
        </serviceCredentials>
      </behavior>
    </serviceBehaviors>
  </behaviors>
</system.serviceModel>
```  
  
## <a name="see-also"></a>関連項目

- <xref:System.ServiceModel.BasicHttpMessageSecurity>
- <xref:System.ServiceModel.Configuration.BasicHttpSecurityElement.Message%2A>
- <xref:System.ServiceModel.BasicHttpSecurity.Message%2A>
- <xref:System.ServiceModel.Configuration.BasicHttpMessageSecurityElement>
- [サービスおよびクライアントのセキュリティ保護](../../../wcf/feature-details/securing-services-and-clients.md)
- [バインド](../../../wcf/bindings.md)
- [システムが提供するバインディングの構成](../../../wcf/feature-details/configuring-system-provided-bindings.md)
- [サービスとクライアントを構成するためのバインディングの使用](../../../wcf/using-bindings-to-configure-services-and-clients.md)
- [\<binding>](bindings.md)
