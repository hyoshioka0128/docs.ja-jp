---
title: '方法: ASP.NET メンバーシップ プロバイダーを使用する'
description: ASP.NET メンバーシッププロバイダーが、Windows ドメインアカウントを使用せずにアクセスするためのユーザー名とパスワードを作成できる web サイトをどのようにサポートするかについて説明します。
ms.date: 03/30/2017
helpviewer_keywords:
- WCF and ASP.NET
- WCF, authorization
- WCF, security
ms.assetid: 322c56e0-938f-4f19-a981-7b6530045b90
ms.openlocfilehash: 6d527993dcf1fc5d5cd39bf22c3e772baf60e62f
ms.sourcegitcommit: 358a28048f36a8dca39a9fe6e6ac1f1913acadd5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85246728"
---
# <a name="how-to-use-the-aspnet-membership-provider"></a>方法: ASP.NET メンバーシップ プロバイダーを使用する

ASP.NET メンバーシッププロバイダーは、ユーザーが一意のユーザー名とパスワードの組み合わせを作成できるようにする Web サイトを ASP.NET 開発者が作成できるようにする機能です。 この機能を使用すれば、ユーザーはだれでもサイトでアカウントを作成し、そのサイトにサインインして、サービスに排他的にアクセスできます。 これは、ユーザーが Windows ドメイン内にアカウントを持っていることが必要な Windows セキュリティとは対照的です。 その代わりに、資格情報を提供するすべてのユーザー (ユーザー名とパスワードの組み合わせ) で、サイトとそのサービスを使用できます。

サンプルアプリケーションについては、「[メンバーシップとロールプロバイダー](../samples/membership-and-role-provider.md)」を参照してください。 ASP.NET ロールプロバイダー機能の使用方法の詳細については、「 [How to: Use the ASP.NET Role provider with a Service](how-to-use-the-aspnet-role-provider-with-a-service.md)」を参照してください。

メンバーシップ機能では、SQL Server データベースを使用してユーザー情報を格納する必要があります。 メンバーシップ機能には、パスワードを忘れたユーザーへの質問を行うためのメソッドも含まれています。

Windows Communication Foundation (WCF) 開発者は、これらの機能をセキュリティ上の目的で利用できます。 WCF アプリケーションに統合されている場合、ユーザーは、WCF クライアントアプリケーションに対してユーザー名とパスワードの組み合わせを指定する必要があります。 WCF サービスにデータを転送するには、ユーザー名とパスワードの資格情報 (構成では) をサポートするバインディングを使用して、 <xref:System.ServiceModel.WSHttpBinding> [\<wsHttpBinding>](../../configure-apps/file-schema/wcf/wshttpbinding.md) クライアント資格情報の種類をに設定し `UserName` ます。 サービスでは、WCF セキュリティはユーザー名とパスワードに基づいてユーザーを認証し、ASP.NET ロールによって指定されたロールも割り当てます。

> [!NOTE]
> WCF には、ユーザー名とパスワードの組み合わせ、またはその他のユーザー情報をデータベースに設定するメソッドは用意されていません。

### <a name="to-configure-the-membership-provider"></a>メンバーシップ プロバイダーを構成するには

1. Web.config ファイルの <> 要素の下に、 `system.web` <の `membership`> 要素を作成します。

2. `<membership>` 要素を作成します。

3. <> 要素の子として `providers` 、 `<clear />` プロバイダーのコレクションをフラッシュする要素を追加します。

4. 要素の下に、、、、、、、、、 `<clear />` `add` `name` `type` `connectionStringName` `applicationName` `enablePasswordRetrieval` `enablePasswordReset` `requiresQuestionAndAnswer` `requiresUniqueEmail` および `passwordFormat` の各属性を適切な値に設定して、<の> 要素を作成します。 `name` 属性は、構成ファイルの値として後で使用します。 `SqlMembershipProvider` に設定する方法の例を次に示します。

    次の例は構成セクションを示します。

    ```xml
    <!-- Configure the Sql Membership Provider -->
    <membership defaultProvider="SqlMembershipProvider" userIsOnlineTimeWindow="15">
      <providers>
        <clear />
          <add
            name="SqlMembershipProvider"
            type="System.Web.Security.SqlMembershipProvider"
            connectionStringName="SqlConn"
            applicationName="MembershipAndRoleProviderSample"
            enablePasswordRetrieval="false"
            enablePasswordReset="false"
            requiresQuestionAndAnswer="false"
            requiresUniqueEmail="true"
            passwordFormat="Hashed" />
      </providers>
    </membership>
    ```

### <a name="to-configure-service-security-to-accept-the-user-namepassword-combination"></a>ユーザー名/パスワードの組み合わせを受け入れるようにサービス セキュリティを構成するには

1. 構成ファイルの要素の下に [\<system.serviceModel>](../../configure-apps/file-schema/wcf/system-servicemodel.md) 要素を追加 [\<bindings>](../../configure-apps/file-schema/wcf/bindings.md) します。

2. [\<wsHttpBinding>](../../configure-apps/file-schema/wcf/wshttpbinding.md)バインドセクションにを追加します。 WCF バインド要素の作成の詳細については、「[方法: 構成でサービスバインディングを指定](../how-to-specify-a-service-binding-in-configuration.md)する」を参照してください。

3. `mode` 要素の `<security>` 属性を `Message` に設定します。

4. `clientCredentialType`<`message`> 要素の属性をに設定 `UserName` します。 これにより、ユーザー名/パスワードの組み合わせがクライアントの資格情報として使用されるようになります。

    次のコード例は、バインディングの構成コードを示しています。

    ```xml
    <system.serviceModel>
    <bindings>
      <wsHttpBinding>
      <!-- Set up a binding that uses UserName as the client credential type -->
        <binding name="MembershipBinding">
          <security mode ="Message">
            <message clientCredentialType ="UserName"/>
          </security>
        </binding>
      </wsHttpBinding>
    </bindings>
    </system.serviceModel>
    ```

### <a name="to-configure-a-service-to-use-the-membership-provider"></a>メンバーシップ プロバイダーを使用するようにサービスを構成するには

1. 要素の子として `<system.serviceModel>` 、要素を追加します。 [\<behaviors>](../../configure-apps/file-schema/wcf/behaviors.md)

2. [\<serviceBehaviors>](../../configure-apps/file-schema/wcf/servicebehaviors.md)<> 要素にを追加 `behaviors` します。

3. を追加 [\<behavior>](../../configure-apps/file-schema/wcf/behavior-of-endpointbehaviors.md) し、 `name` 属性を適切な値に設定します。

4. [\<serviceCredentials>](../../configure-apps/file-schema/wcf/servicecredentials.md)<> 要素にを追加 `behavior` します。

5. を [\<userNameAuthentication>](../../configure-apps/file-schema/wcf/usernameauthentication.md) 要素に追加し `<serviceCredentials>` ます。

6. `userNamePasswordValidationMode` 属性を `MembershipProvider` に設定します。

    > [!IMPORTANT]
    > `userNamePasswordValidationMode`値が設定されていない場合、WCF は ASP.NET メンバーシッププロバイダーの代わりに Windows 認証を使用します。

7. `membershipProviderName` 属性をプロバイダーの名前 (このトピックの最初の手順でプロバイダーを追加したときに指定したもの) に設定します。 次の例に、この時点での `<serviceCredentials>` のフラグメントを示します。

    ```xml
    <behaviors>
       <serviceBehaviors>
          <behavior name="MyServiceBehavior">
             <serviceCredentials>
                <userNameAuthentication
                userNamePasswordValidationMode="MembershipProvider"
                membershipProviderName="SqlMembershipProvider" />
             </serviceCredentials>
          </behavior>
       </serviceBehaviors>
    </behaviors>
    ```

## <a name="example"></a>例

次のコードは、ASP メンバーシップ機能を使用するサービスの構成を示します。

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.serviceModel>
    <services>
      <service behaviorConfiguration="MyServiceBehavior" name="Microsoft.Samples.GettingStarted.CalculatorService">
        <endpoint address="http://microsoft.com/WCFservices/Calculator"
          binding="wsHttpBinding" bindingConfiguration="MembershipBinding"
          name="ASPmemberUserName" contract="Microsoft.Samples.GettingStarted.ICalculator" />
      </service>
    </services>
    <behaviors>
      <serviceBehaviors>
        <behavior name="MyServiceBehavior">
          <serviceCredentials>
            <userNameAuthentication
              userNamePasswordValidationMode="MembershipProvider"
              membershipProviderName="SqlMembershipProvider" />
          </serviceCredentials>
        </behavior>
          </serviceBehaviors>
    </behaviors>
    <bindings>
      <wsHttpBinding>
        <binding name="MembershipBinding">
          <security mode="Message">
            <message clientCredentialType="UserName" />
          </security>
        </binding>
      </wsHttpBinding>
    </bindings>
  </system.serviceModel>
</configuration>
```

## <a name="see-also"></a>関連項目

- [方法: ASP.NET のロール プロバイダーとサービスを使用する](how-to-use-the-aspnet-role-provider-with-a-service.md)
- [メンバーシップとロール プロバイダー](../samples/membership-and-role-provider.md)
