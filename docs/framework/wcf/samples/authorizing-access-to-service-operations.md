---
title: サービス操作へのアクセスの承認
ms.date: 03/30/2017
helpviewer_keywords:
- service behaviors, authorizing access sample
- Authorizing Access To Service Operations Sample [Windows Communication Foundation]
- authorization, Windows Communication Foundation sample
ms.assetid: ddcfdaa5-8b2e-4e13-bd85-887209dc6328
ms.openlocfilehash: 3097c86f50a75dec8a649ca4e1edd2511a046ca8
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84585533"
---
# <a name="authorizing-access-to-service-operations"></a>サービス操作へのアクセスの承認
このサンプルでは、を使用して、 [\<serviceAuthorization>](../../configure-apps/file-schema/wcf/serviceauthorization-element.md) サービス操作へのアクセスを承認するために属性を使用できるようにする方法を示し <xref:System.Security.Permissions.PrincipalPermissionAttribute> ます。 このサンプルは、[はじめに](getting-started-sample.md)のサンプルに基づいています。 サービスとクライアントは、を使用して構成され [\<wsHttpBinding>](../../configure-apps/file-schema/wcf/wshttpbinding.md) ます。 `mode`の属性 [\<security>](../../configure-apps/file-schema/wcf/security-of-custombinding.md) がに設定され、 `Message` `clientCredentialType` がに設定されてい `Windows` ます。 <xref:System.Security.Permissions.PrincipalPermissionAttribute> は各サービス メソッドに適用され、各操作へのアクセスを制限するために使用されます。 呼び出し元は、各操作にアクセスできる Windows 管理者である必要があります。  
  
 この例では、クライアントはコンソール アプリケーション (.exe) であり、サービスはインターネット インフォメーション サービス (IIS) によってホストされます。  
  
> [!NOTE]
> このサンプルのセットアップ手順とビルド手順については、このトピックの最後を参照してください。  
  
 サービス構成ファイルでは、を使用して [\<serviceAuthorization>](../../configure-apps/file-schema/wcf/serviceauthorization-element.md) 属性を設定し `principalPermissionMode` ます。  
  
```xml  
<behaviors>  
  <serviceBehaviors>  
    <behavior>
      <!-- The serviceAuthorization behavior sets the  
           principalPermissionMode to UseWindowsGroups.  
           This puts a WindowsPrincipal on the current thread when a   
           service is invoked. -->  
      <serviceAuthorization principalPermissionMode="UseWindowsGroups" />  
    </behavior>  
  </serviceBehaviors>  
</behaviors>  
```  
  
 `principalPermissionMode` を `UseWindowsGroups` に設定すると、Windows グループ名に基づいて <xref:System.Security.Permissions.PrincipalPermissionAttribute> を使用できるようになります。  
  
 呼び出し元が Windows 管理者グループのメンバーであることを要求するため、<xref:System.Security.Permissions.PrincipalPermissionAttribute> が各操作に適用されます。次のサンプル コードを参照してください。  
  
```csharp
[PrincipalPermission(SecurityAction.Demand,
                             Role = "Builtin\\Administrators")]  
public double Add(double n1, double n2)  
{  
    double result = n1 + n2;  
    return result;  
}  
```  
  
 このサンプルを実行すると、操作要求および応答がクライアントのコンソール ウィンドウに表示されます。 クライアントが管理者グループのメンバーであるアカウントで実行される場合、クライアントは各操作と正常に通信できます。それ以外のアカウントで実行される場合、アクセスは拒否されます。 承認エラーを試すには、管理グループのメンバーではないアカウントでクライアントを実行します。 クライアントをシャットダウンするには、コンソール ウィンドウで Enter キーを押します。  
  
 <xref:System.ServiceModel.Dispatcher.IErrorHandler> を実装すると、サービスに承認エラーを通知することができます。 の実装の詳細については[、「エラー処理およびレポートに対する制御の拡張](extending-control-over-error-handling-and-reporting.md)」を参照してください `IErrorHandler` 。  
  
### <a name="to-set-up-build-and-run-the-sample"></a>サンプルをセットアップ、ビルド、および実行するには  
  
1. [Windows Communication Foundation サンプルの1回限りのセットアップ手順](one-time-setup-procedure-for-the-wcf-samples.md)を実行したことを確認します。  
  
2. ソリューションの C# 版または Visual Basic .NET 版をビルドするには、「 [Building the Windows Communication Foundation Samples](building-the-samples.md)」の手順に従います。  
  
3. サンプルを単一コンピューター構成または複数コンピューター構成で実行するには、「 [Windows Communication Foundation サンプルの実行](running-the-samples.md)」の手順に従います。  
