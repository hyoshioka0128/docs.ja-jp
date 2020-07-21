---
title: ユーザー名クライアントを使用したメッセージ セキュリティ
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 36335cb9-76b8-4443-92c7-44f081eabb21
ms.openlocfilehash: 9447487012cae370d35880e5b780465f9434051b
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84602623"
---
# <a name="message-security-with-a-user-name-client"></a>ユーザー名クライアントを使用したメッセージ セキュリティ
次の図は、メッセージレベルのセキュリティを使用してセキュリティで保護された Windows Communication Foundation (WCF) サービスとクライアントを示しています。 サービスは X.509 証明書を使用して認証されます。 クライアントはユーザー名とパスワードを使用して認証されます。  
  
 サンプルアプリケーションについては、「[メッセージセキュリティユーザー名](../samples/message-security-user-name.md)」を参照してください。  
  
 ![ユーザー名認証を使用したメッセージ セキュリティ](media/1fb10a61-7e1d-42f5-b1af-195bfee5b3c6.gif "1fb10a61-7e1d-42f5-b1af-195bfee5b3c6")  
  
|特徴|説明|  
|--------------------|-----------------|  
|セキュリティ モード|Message|  
|相互運用性|Windows Communication Foundation (WCF) のみ|  
|認証 (サーバー)|初期ネゴシエーションにはサーバー認証が必要|  
|認証 (クライアント)|ユーザー名/パスワード|  
|整合性|はい、共有のセキュリティ コンテキストを使用します|  
|機密情報|はい、共有のセキュリティ コンテキストを使用します|  
|トランスポート|HTTP|  
|バインド|<xref:System.ServiceModel.WSHttpBinding>|  
  
## <a name="service"></a>サービス  
 次のコードと構成は、別々に実行します。 次のいずれかの操作を行います。  
  
- 構成を使用せずに、コードを使用してスタンドアロン サービスを作成します。  
  
- 提供された構成を使用してサービスを作成しますが、エンドポイントを定義しません。  
  
### <a name="code"></a>コード  
 次のコードは、メッセージ セキュリティを使用するサービス エンドポイントの作成方法を示します。  
  
 [!code-csharp[C_SecurityScenarios#9](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securityscenarios/cs/source.cs#9)]
 [!code-vb[C_SecurityScenarios#9](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securityscenarios/vb/source.vb#9)]  
  
### <a name="configuration"></a>構成  
 コードの代わりに次の構成を使用できます。  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<configuration>  
  <system.serviceModel>  
    <behaviors>  
      <serviceBehaviors>  
        <behavior name="ServiceCredentialsBehavior">  
          <serviceCredentials>  
            <serviceCertificate findValue="Contoso.com"
                                storeLocation="LocalMachine"  
                                storeName="My"
                                x509FindType="FindBySubjectName" />  
          </serviceCredentials>  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
    <services>  
      <service behaviorConfiguration="ServiceCredentialsBehavior"  
               name="ServiceModel.Calculator">  
        <endpoint address="http://localhost/Calculator"  
                  binding="wsHttpBinding"  
                  bindingConfiguration="MessageAndUserName"  
                  name="SecuredByTransportEndpoint"  
                  contract="ServiceModel.ICalculator" />  
      </service>  
    </services>  
    <bindings>  
      <wsHttpBinding>  
        <binding name="MessageAndUserName">  
          <security mode="Message">
            <message clientCredentialType="UserName" />  
          </security>  
        </binding>  
      </wsHttpBinding>  
    </bindings>  
    <client />  
  </system.serviceModel>  
</configuration>  
```  
  
## <a name="client"></a>クライアント  
  
### <a name="code"></a>コード  
 クライアントを作成する場合のコード例を次に示します。 バインディングではメッセージ モード セキュリティを使用し、クライアント資格情報の種類は `UserName` に設定します。 ユーザー名とパスワードの指定はコードを使用する場合に限られます (構成可能ではありません)。 ユーザー名とパスワードを返すコードは、アプリケーション レベルで実行される必要があるため、ここには示しません。 たとえば、Windows フォーム ダイアログ ボックスを使用してユーザーにデータを照会します。  
  
 [!code-csharp[C_SecurityScenarios#16](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securityscenarios/cs/source.cs#16)]
 [!code-vb[C_SecurityScenarios#16](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securityscenarios/vb/source.vb#16)]  
  
### <a name="configuration"></a>構成  
 クライアントを構成する場合のコード例を次に示します。 バインディングではメッセージ モード セキュリティを使用し、クライアント資格情報の種類は `UserName` に設定します。 ユーザー名とパスワードの指定はコードを使用する場合に限られます (構成可能ではありません)。  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<configuration>  
  <system.serviceModel>  
    <bindings>  
      <wsHttpBinding>  
        <binding name="WSHttpBinding_ICalculator" >  
          <security mode="Message">  
            <message clientCredentialType="UserName" />  
          </security>  
        </binding>  
      </wsHttpBinding>  
    </bindings>  
    <client>  
      <endpoint address="http://machineName/Calculator"
                binding="wsHttpBinding"  
                bindingConfiguration="WSHttpBinding_ICalculator"
                contract="ICalculator"  
                name="WSHttpBinding_ICalculator">  
        <identity>  
          <dns value ="Contoso.com" />  
        </identity>  
      </endpoint>  
    </client>  
  </system.serviceModel>  
</configuration>  
```  
  
## <a name="see-also"></a>関連項目

- [セキュリティの概要](security-overview.md)
- [メッセージ セキュリティ ユーザー名](../samples/message-security-user-name.md)
- [サービス ID と認証](service-identity-and-authentication.md)
- [\<identity>](../../configure-apps/file-schema/wcf/identity.md)
- [Windows Server AppFabric のセキュリティ モデル](https://docs.microsoft.com/previous-versions/appfabric/ee677202(v=azure.10))
