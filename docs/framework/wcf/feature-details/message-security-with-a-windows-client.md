---
title: Windows クライアントとのメッセージ セキュリティ
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 01e7d0b8-10f9-45c3-a4c5-53d44dc61eb8
ms.openlocfilehash: dcb311523c6ec41b62f6e69fe6bc7635b9d49708
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84595233"
---
# <a name="message-security-with-a-windows-client"></a>Windows クライアントとのメッセージ セキュリティ
このシナリオは、メッセージセキュリティモードによってセキュリティ保護された Windows Communication Foundation (WCF) クライアントおよびサーバーを示しています。 クライアントとサービスは、Windows 資格情報を使用して認証します。  
  
 ![Windows クライアントを使用したメッセージセキュリティ](media/1c8618d4-0005-4022-beb6-32fd087a8c3c.gif "1c8618d4-0005-4022-beb6-32fd087a8c3c")  
  
|特徴|説明|  
|--------------------|-----------------|  
|セキュリティ モード|Message|  
|相互運用性|WCF のみ|  
|認証 (サーバー)|サーバーとクライアントの相互認証|  
|認証 (クライアント)|サーバーとクライアントの相互認証|  
|整合性|はい、共有のセキュリティ コンテキストを使用します|  
|機密情報|はい、共有のセキュリティ コンテキストを使用します|  
|トランスポート|NET.TCP|  
|バインド|<xref:System.ServiceModel.NetTcpBinding>|  
  
## <a name="service"></a>サービス  
 次のコードと構成は、別々に実行します。 次のいずれかの操作を行います。  
  
- 構成を使用せずに、コードを使用してスタンドアロン サービスを作成します。  
  
- 提供された構成を使用してサービスを作成しますが、エンドポイントを定義しません。  
  
### <a name="code"></a>コード  
 次のコードでは、メッセージ セキュリティを使用するサービス エンドポイントを作成し、Windows コンピューターとの間にセキュリティで保護されたコンテキストを確立する方法を示します。  
  
 [!code-csharp[C_SecurityScenarios#11](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securityscenarios/cs/source.cs#11)]
 [!code-vb[C_SecurityScenarios#11](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securityscenarios/vb/source.vb#11)]  
  
### <a name="configuration"></a>構成  
 コードの代わりに次の構成を使用して、サービスをセットアップできます。  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<configuration>  
  <system.serviceModel>  
    <services>  
      <service behaviorConfiguration=""  
               name="ServiceModel.Calculator">  
        <endpoint address="net.tcp://localhost:8008/Calculator"  
                  binding="netTcpBinding"  
                  bindingConfiguration="Windows"  
                  name="WindowsOverMessage"  
                  contract="ServiceModel.ICalculator" />  
      </service>  
    </services>  
    <bindings>  
      <netTcpBinding>  
        <binding name="Windows">  
          <security mode="Message">  
            <message clientCredentialType="Windows" />  
          </security>  
        </binding>  
      </netTcpBinding>  
    </bindings>  
    <client />  
  </system.serviceModel>  
</configuration>  
```  
  
## <a name="client"></a>クライアント  
 次のコードと構成は、別々に実行します。 次のいずれかの操作を行います。  
  
- コード (およびクライアント コード) を使用してスタンドアロン クライアントを作成します。  
  
- エンドポイント アドレスを定義しないクライアントを作成します。 代わりに、引数として構成名を受け取るクライアント コンストラクターを使用します。 次に例を示します。  
  
     [!code-csharp[C_SecurityScenarios#0](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securityscenarios/cs/source.cs#0)]
     [!code-vb[C_SecurityScenarios#0](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securityscenarios/vb/source.vb#0)]  
  
### <a name="code"></a>コード  
 クライアントを作成する場合のコード例を次に示します。 バインディングはメッセージ モード セキュリティに対して行い、クライアント資格情報の種類は `Windows` に設定します。  
  
 [!code-csharp[C_SecurityScenarios#18](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securityscenarios/cs/source.cs#18)]
 [!code-vb[C_SecurityScenarios#18](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securityscenarios/vb/source.vb#18)]  
  
### <a name="configuration"></a>構成  
 次の構成を使用してクライアントのプロパティを設定します。  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<configuration>  
  <system.serviceModel>  
    <bindings>  
      <netTcpBinding>  
        <binding name="NetTcpBinding_ICalculator" >  
         <security mode="Message">  
            <message clientCredentialType="Windows" />  
          </security>  
        </binding>  
      </netTcpBinding>  
    </bindings>  
    <client>  
      <endpoint address="net.tcp://machineName:8008/Calculator"
                binding="netTcpBinding"  
                bindingConfiguration="NetTcpBinding_ICalculator"  
                contract="ICalculator"  
                name="NetTcpBinding_ICalculator">
      </endpoint>  
    </client>  
  </system.serviceModel>  
</configuration>  
```  
  
## <a name="see-also"></a>関連項目

- [セキュリティの概要](security-overview.md)
- [Windows Server AppFabric のセキュリティ モデル](https://docs.microsoft.com/previous-versions/appfabric/ee677202(v=azure.10))
