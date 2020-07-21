---
title: サービス監査動作
ms.date: 03/30/2017
ms.assetid: 59bf0cda-e496-4418-a3a1-2f0f6e85f8ce
ms.openlocfilehash: bfe13146a7f7cdec648a82a34c34077ec5466809
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84599933"
---
# <a name="service-auditing-behavior"></a>サービス監査動作
このサンプルでは、<xref:System.ServiceModel.Description.ServiceSecurityAuditBehavior> を使用して、サービス操作中にセキュリティ イベントの監査を有効にする方法を示します。 このサンプルは、[はじめに](getting-started-sample.md)に基づいています。 サービスとクライアントは、を使用して構成されてい [\<wsHttpBinding>](../../configure-apps/file-schema/wcf/wshttpbinding.md) ます。 `mode`の属性 [\<security>](../../configure-apps/file-schema/wcf/security-of-custombinding.md) がに設定され、 `Message` `clientCredentialType` がに設定されてい `Windows` ます。 この例では、クライアントはコンソール アプリケーション (.exe) であり、サービスはインターネット インフォメーション サービス (IIS) によってホストされます。  
  
> [!NOTE]
> このサンプルのセットアップ手順とビルド手順については、このトピックの最後を参照してください。  
  
 サービス構成ファイルは、次のように `serviceSecurityAudit` 要素を使用して監査を構成します。  
  
```xml  
<behaviors>  
  <serviceBehaviors>  
    <behavior name="CalculatorServiceBehavior">  
      ...  
<!-- serviceSecurityAudit allows specification of audit location   
     and whether to audit success, failure or both. This service   
     logs success and failure of messageAuthentication   
     to the default location -->  
     <serviceSecurityAudit auditLogLocation ="Default" messageAuthenticationAuditLevel = "SuccessOrFailure" />  
    </behavior>  
  </serviceBehaviors>  
</behaviors>  
```  
  
 このサンプルを実行すると、操作要求および応答がクライアントのコンソール ウィンドウに表示されます。 クライアントをシャットダウンするには、コンソール ウィンドウで Enter キーを押します。  
  
 結果として得られる監査ログは、イベント ビューアーを実行して表示できます。 監査イベントは既定で、Windows XP の場合はアプリケーション ログに、Windows Server 2003 と Windows Vista の場合はセキュリティ ログに表示されます。 Windows Server 2008 と Windows 7 では、監査イベントをアプリケーション ログとサービス ログに表示できます。 監査イベントの場所は、 `auditLogLocation` 属性を "Application" または "Security" に設定することによって指定できます。 詳細については、「[方法: セキュリティイベントを監査](../feature-details/how-to-audit-wcf-security-events.md)する」を参照してください。 イベントがセキュリティログに書き込まれる場合は、LocalSecurityPolicy-> Enable オブジェクトアクセスを "Success" と "Failure" に設定する必要があります。  
  
 イベント ログを調べる場合、監査イベントのソースは "ServiceModel Audit 3.0.0.0" です。 メッセージ認証監査レコードには "MessageAuthentication" のカテゴリがありますが、サービス承認監査レコードには "ServiceAuthorization" のカテゴリがあります。  
  
 メッセージ認証監査イベントは、メッセージの改ざんや期限切れの有無、クライアントによるサービス認証の成否などに適用されます。 このイベントでは、認証の成功または失敗に関する情報とクライアント ID、およびメッセージ送信先のエンドポイントとそのメッセージに関連付けられたアクションに関する情報が提供されます。  
  
 サービス承認監査イベントは、サービス承認マネージャーによって決定される承認に適用されます。 このイベントでは、承認の成功または失敗に関する情報とクライアント ID、メッセージ送信先のエンドポイント、そのメッセージに関連付けられたアクション、受信メッセージから生成された承認コンテキストの ID、およびアクセス決定を行った承認マネージャーの種類に関する情報が提供されます。  
  
### <a name="to-set-up-build-and-run-the-sample"></a>サンプルをセットアップ、ビルド、および実行するには  
  
1. [Windows Communication Foundation サンプルの1回限りのセットアップ手順](one-time-setup-procedure-for-the-wcf-samples.md)を実行したことを確認します。  
  
2. ソリューションの C# 版または Visual Basic .NET 版をビルドするには、「 [Building the Windows Communication Foundation Samples](building-the-samples.md)」の手順に従います。  
  
3. サンプルを単一コンピューター構成または複数コンピューター構成で実行するには、「 [Windows Communication Foundation サンプルの実行](running-the-samples.md)」の手順に従います。  
  
## <a name="see-also"></a>関連項目

- [監査](../feature-details/auditing-security-events.md)
- [方法: セキュリティ イベントを監査する](../feature-details/how-to-audit-wcf-security-events.md)
