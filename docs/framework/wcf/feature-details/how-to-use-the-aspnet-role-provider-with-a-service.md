---
title: '方法: ASP.NET のロール プロバイダーとサービスを使用する'
ms.date: 03/30/2017
ms.assetid: 88d33a81-8ac7-48de-978c-5c5b1257951e
ms.openlocfilehash: 45eeda046e877b4379d7d0e5edd90fac305f5e44
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84595298"
---
# <a name="how-to-use-the-aspnet-role-provider-with-a-service"></a>方法: ASP.NET のロール プロバイダーとサービスを使用する

ASP.NET ロールプロバイダー (ASP.NET メンバーシッププロバイダーと共に) は、ASP.NET 開発者がサイトを使用してアカウントを作成し、承認のためにロールを割り当てることができる Web サイトを作成できるようにする機能です。 この機能を使用すれば、ユーザーはだれでもサイトでアカウントを作成し、そのサイトにログインしてサービスに排他的にアクセスできます。 これは、ユーザーが Windows ドメイン内にアカウントを持っていることが必要な Windows セキュリティとは対照的です。 代わりに、資格情報 (ユーザー名とパスワードの組み合わせ) を指定するすべてのユーザーが、サイトとそのサービスを使用できます。  
  
サンプルアプリケーションについては、「[メンバーシップとロールプロバイダー](../samples/membership-and-role-provider.md)」を参照してください。 メンバーシッププロバイダーの ASP.NET 機能の詳細については、「[方法: ASP.NET メンバーシッププロバイダーを使用](how-to-use-the-aspnet-membership-provider.md)する」を参照してください。  
  
ロール プロバイダー機能では、SQL Server データベースを使用してユーザー情報を格納します。 Windows Communication Foundation (WCF) 開発者は、これらの機能をセキュリティ上の目的で利用できます。 WCF アプリケーションに統合されている場合、ユーザーは、WCF クライアントアプリケーションに対してユーザー名とパスワードの組み合わせを指定する必要があります。 WCF でデータベースを使用できるようにするには、クラスのインスタンスを作成し、 <xref:System.ServiceModel.Description.ServiceAuthorizationBehavior> その <xref:System.ServiceModel.Description.ServiceAuthorizationBehavior.PrincipalPermissionMode%2A> プロパティをに設定 <xref:System.ServiceModel.Description.PrincipalPermissionMode.UseAspNetRoles> して、サービスをホストしているへの動作のコレクションにインスタンスを追加する必要があり <xref:System.ServiceModel.ServiceHost> ます。  
  
## <a name="configure-the-role-provider"></a>ロールプロバイダーを構成する  
  
1. Web.config ファイルの < > 要素の下に `system.web` < > 要素を追加し、 `roleManager` その `enabled` 属性をに設定し `true` ます。  
  
2. `defaultProvider` 属性を `SqlRoleProvider` に設定します。  
  
3. <> 要素の子として `roleManager` 、<> 要素を追加し `providers` ます。  
  
4. <> 要素の子として、次の `providers` `add` `name` `type` `connectionStringName` `applicationName` 例に示すように、、、、およびの各属性を適切な値に設定して、<> 要素を追加します。  
  
    ```xml  
    <!-- Configure the Sql Role Provider. -->  
    <roleManager enabled ="true"
     defaultProvider ="SqlRoleProvider" >  
       <providers>  
         <add name ="SqlRoleProvider"
           type="System.Web.Security.SqlRoleProvider"
           connectionStringName="SqlConn"
           applicationName="MembershipAndRoleProviderSample"/>  
       </providers>  
    </roleManager>  
    ```  
  
## <a name="configure-the-service-to-use-the-role-provider"></a>ロールプロバイダーを使用するようにサービスを構成する  
  
1. Web.config ファイルで、要素を追加し [\<system.serviceModel>](../../configure-apps/file-schema/wcf/system-servicemodel.md) ます。  
  
2. 要素を [\<behaviors>](../../configure-apps/file-schema/wcf/behaviors.md) <`system.ServiceModel`> 要素に追加します。  
  
3. [\<serviceBehaviors>](../../configure-apps/file-schema/wcf/servicebehaviors.md)<> 要素にを追加 `behaviors` します。  
  
4. 要素を追加 [\<behavior>](../../configure-apps/file-schema/wcf/behavior-of-endpointbehaviors.md) し、 `name` 属性を適切な値に設定します。  
  
5. [\<serviceAuthorization>](../../configure-apps/file-schema/wcf/serviceauthorization-element.md)<> 要素にを追加 `behavior` します。  
  
6. `principalPermissionMode` 属性を `UseAspNetRoles` に設定します。  
  
7. `roleProviderName` 属性を `SqlRoleProvider` に設定します。 この構成の一部を次の例に示します。  
  
    ```xml  
    <behaviors>  
     <serviceBehaviors>  
      <behavior name="CalculatorServiceBehavior">  
       <serviceAuthorization principalPermissionMode ="UseAspNetRoles"  
                             roleProviderName ="SqlRoleProvider" />  
      </behavior>  
     </serviceBehaviors>  
    </behaviors>  
    ```  
  
## <a name="see-also"></a>関連項目

- [メンバーシップとロール プロバイダー](../samples/membership-and-role-provider.md)
- [方法: ASP.NET メンバーシップ プロバイダーを使用する](how-to-use-the-aspnet-membership-provider.md)
