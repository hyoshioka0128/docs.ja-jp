---
title: '方法: カスタム ユーザー名およびパスワード検証を使用する'
description: 既定の Windows ユーザー名とパスワードの検証の代わりに、WFC アプリケーションのカスタムパスワード検証を組み込む方法について説明します。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WCF, username and password
ms.assetid: 8e08b74b-fa44-4018-b63d-0d0805f85e3f
ms.openlocfilehash: 7f69db7bf8248593b64cdae4378983c2460de597
ms.sourcegitcommit: 358a28048f36a8dca39a9fe6e6ac1f1913acadd5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85246793"
---
# <a name="how-to-use-a-custom-user-name-and-password-validator"></a>方法: カスタム ユーザー名およびパスワード検証を使用する

既定では、ユーザー名とパスワードが認証に使用されると、Windows Communication Foundation (WCF) は Windows を使用してユーザー名とパスワードを検証します。 ただし、WCF では、カスタムのユーザー名とパスワードの認証方式 (*検証コントロール*とも呼ばれます) を使用できます。 ユーザー名およびパスワードのカスタム検証を組み込むには、<xref:System.IdentityModel.Selectors.UserNamePasswordValidator> から派生するクラスを作成して構成します。

サンプルアプリケーションについては、「[ユーザー名パスワード検証コントロール](../samples/user-name-password-validator.md)」を参照してください。

### <a name="to-create-a-custom-user-name-and-password-validator"></a>カスタムのユーザー名/パスワード検証コントロールを作成するには

1. <xref:System.IdentityModel.Selectors.UserNamePasswordValidator> から派生するクラスを作成します。

    [!code-csharp[C_CustomUsernameAndPasswordValidator#3](~/samples/snippets/csharp/VS_Snippets_CFX/c_customusernameandpasswordvalidator/cs/service.cs#3)]
    [!code-vb[C_CustomUsernameAndPasswordValidator#3](~/samples/snippets/visualbasic/VS_Snippets_CFX/c_customusernameandpasswordvalidator/vb/service.vb#3)]

2. <xref:System.IdentityModel.Selectors.UserNamePasswordValidator.Validate%2A> メソッドをオーバーライドして、カスタム認証方式を実装します。

    次の例のコードは、<xref:System.IdentityModel.Selectors.UserNamePasswordValidator.Validate%2A> メソッドをオーバーライドします。稼働環境では、このようなコードを使用しないでください。 このコードをカスタムのユーザー名/パスワード検証方式に置き換えます。この場合、ユーザー名とパスワードの組み合わせをデータベースから取得する必要があります。

    クライアントに認証エラーを返すには、<xref:System.ServiceModel.FaultException> メソッドで <xref:System.IdentityModel.Selectors.UserNamePasswordValidator.Validate%2A> をスローします。

    [!code-csharp[C_CustomUsernameAndPasswordValidator#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customusernameandpasswordvalidator/cs/service.cs#4)]
    [!code-vb[C_CustomUsernameAndPasswordValidator#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customusernameandpasswordvalidator/vb/service.vb#4)]

### <a name="to-configure-a-service-to-use-a-custom-user-name-and-password-validator"></a>カスタムのユーザー名/パスワード検証コントロールを使用するようにサービスを構成するには

1. 任意のトランスポート上のメッセージ セキュリティ、または HTTP(S) 上のトランスポート レベル セキュリティを使用するバインディングを構成します。

    メッセージセキュリティを使用する場合は、などのシステム指定のバインディング、 [\<wsHttpBinding>](../../configure-apps/file-schema/wcf/wshttpbinding.md) または [\<customBinding>](../../configure-apps/file-schema/wcf/custombinding.md) メッセージセキュリティと資格情報の種類をサポートするのいずれかを追加し `UserName` ます。

    HTTP (S) でトランスポートレベルのセキュリティを使用する場合は、 [\<wsHttpBinding>](../../configure-apps/file-schema/wcf/wshttpbinding.md) [\<basicHttpBinding>](../../configure-apps/file-schema/wcf/basichttpbinding.md) [\<netTcpBinding>](../../configure-apps/file-schema/wcf/nettcpbinding.md) [\<customBinding>](../../configure-apps/file-schema/wcf/custombinding.md) http (s) と認証スキームを使用するまたはを追加し `Basic` ます。

    > [!NOTE]
    > .NET Framework 3.5 以降のバージョンを使用する場合は、メッセージおよびトランスポートセキュリティと共にカスタムのユーザー名とパスワード検証を使用できます。 WinFX では、カスタムのユーザー名とパスワード検証コントロールは、メッセージセキュリティでのみ使用できます。

    > [!TIP]
    > このコンテキストでを使用する方法の詳細につい \<netTcpBinding> ては、「」を参照してください [\<security>](../../configure-apps/file-schema/wcf/security-of-nettcpbinding.md) 。

    1. 構成ファイルの要素の下に [\<system.serviceModel>](../../configure-apps/file-schema/wcf/system-servicemodel.md) 要素を追加 [\<bindings>](../../configure-apps/file-schema/wcf/bindings.md) します。

    2. [\<wsHttpBinding>](../../configure-apps/file-schema/wcf/wshttpbinding.md)バインドセクションにまたは要素を追加し [\<basicHttpBinding>](../../configure-apps/file-schema/wcf/basichttpbinding.md) ます。 WCF バインド要素の作成の詳細については、「[方法: 構成でサービスバインディングを指定](../how-to-specify-a-service-binding-in-configuration.md)する」を参照してください。

    3. `mode`またはの属性を [\<security>](../../configure-apps/file-schema/wcf/security-of-wshttpbinding.md) 、、、 [\<security>](../../configure-apps/file-schema/wcf/security-of-basichttpbinding.md) `Message` またはに設定 `Transport` `TransportWithMessageCredential` します。

    4. `clientCredentialType`またはの属性を設定し [\<message>](../../configure-apps/file-schema/wcf/message-of-wshttpbinding.md) [\<transport>](../../configure-apps/file-schema/wcf/transport-of-wshttpbinding.md) ます。

        メッセージセキュリティを使用する場合は、 `clientCredentialType` の属性を [\<message>](../../configure-apps/file-schema/wcf/message-of-wshttpbinding.md) に設定 `UserName` します。

        HTTP (S) でトランスポートレベルのセキュリティを使用する場合 `clientCredentialType` は、またはの属性を [\<transport>](../../configure-apps/file-schema/wcf/transport-of-wshttpbinding.md) に設定 [\<transport>](../../configure-apps/file-schema/wcf/transport-of-basichttpbinding.md) `Basic` します。

        > [!NOTE]
        > WCF サービスがトランスポートレベルのセキュリティを使用してインターネットインフォメーションサービス (IIS) でホストされていて、 <xref:System.ServiceModel.Security.UserNamePasswordServiceCredential.UserNamePasswordValidationMode%2A> プロパティがに設定されている場合 <xref:System.ServiceModel.Security.UserNamePasswordValidationMode.Custom> 、カスタム認証スキームは Windows 認証のサブセットを使用します。 このシナリオでは、WCF がカスタム認証システムを呼び出す前に、IIS が Windows 認証を実行します。

    WCF バインド要素の作成の詳細については、「[方法: 構成でサービスバインディングを指定](../how-to-specify-a-service-binding-in-configuration.md)する」を参照してください。

    次の例は、バインディングの構成コードを示しています。

    ```xml
    <system.serviceModel>
      <bindings>
      <wsHttpBinding>
          <binding name="Binding1">
            <security mode="Message">
              <message clientCredentialType="UserName" />
            </security>
          </binding>
        </wsHttpBinding>
      </bindings>
    </system.serviceModel>
    ```

2. 受信 <xref:System.IdentityModel.Tokens.UserNameSecurityToken> セキュリティ トークンのユーザー名とパスワードの組み合わせを検証する際に、カスタムのユーザー名/パスワード検証コントロールを使用することを指定する動作を構成します。

    1. 要素の子として [\<system.serviceModel>](../../configure-apps/file-schema/wcf/system-servicemodel.md) 、要素を追加し [\<behaviors>](../../configure-apps/file-schema/wcf/behaviors.md) ます。

    2. を [\<serviceBehaviors>](../../configure-apps/file-schema/wcf/servicebehaviors.md) 要素に追加し [\<behaviors>](../../configure-apps/file-schema/wcf/behaviors.md) ます。

    3. 要素を追加 [\<behavior>](../../configure-apps/file-schema/wcf/behavior-of-servicebehaviors.md) し、 `name` 属性を適切な値に設定します。

    4. を [\<serviceCredentials>](../../configure-apps/file-schema/wcf/servicecredentials.md) 要素に追加し [\<behavior>](../../configure-apps/file-schema/wcf/behavior-of-servicebehaviors.md) ます。

    5. を [\<userNameAuthentication>](../../configure-apps/file-schema/wcf/usernameauthentication.md) に追加し [\<serviceCredentials>](../../configure-apps/file-schema/wcf/servicecredentials.md) ます。

    6. `userNamePasswordValidationMode` を `Custom` に設定します。

        > [!IMPORTANT]
        > `userNamePasswordValidationMode`値が設定されていない場合、WCF はカスタムユーザー名とパスワード検証コントロールではなく Windows 認証を使用します。

    7. `customUserNamePasswordValidatorType` を、カスタムのユーザー名/パスワード検証コントロールを表す型に設定します。

    次の例は、 `<serviceCredentials>` この点を示すフラグメントを示しています。

    ```xml
    <serviceCredentials>
      <userNameAuthentication userNamePasswordValidationMode="Custom" customUserNamePasswordValidatorType="Microsoft.ServiceModel.Samples.CalculatorService.CustomUserNameValidator, service" />
    </serviceCredentials>
    ```

## <a name="example"></a>例

カスタムのユーザー名/パスワード検証コントロールを作成する方法を次のコード例に示します。 稼働環境では、<xref:System.IdentityModel.Selectors.UserNamePasswordValidator.Validate%2A> メソッドをオーバーライドするコードを使用しないでください。 このコードをカスタムのユーザー名/パスワード検証方式に置き換えます。この場合、ユーザー名とパスワードの組み合わせをデータベースから取得する必要があります。

[!code-csharp[C_CustomUsernameAndPasswordValidator#1](~/samples/snippets/csharp/VS_Snippets_CFX/c_customusernameandpasswordvalidator/cs/service.cs#1)]
[!code-vb[C_CustomUsernameAndPasswordValidator#1](~/samples/snippets/visualbasic/VS_Snippets_CFX/c_customusernameandpasswordvalidator/vb/service.vb#1)]
[!code-csharp[C_CustomUsernameAndPasswordValidator#2](~/samples/snippets/csharp/VS_Snippets_CFX/c_customusernameandpasswordvalidator/cs/service.cs#2)]
[!code-vb[C_CustomUsernameAndPasswordValidator#2](~/samples/snippets/visualbasic/VS_Snippets_CFX/c_customusernameandpasswordvalidator/vb/service.vb#2)]

## <a name="see-also"></a>関連項目

- <xref:System.IdentityModel.Selectors.UserNamePasswordValidator>
- [方法: ASP.NET メンバーシップ プロバイダーを使用する](how-to-use-the-aspnet-membership-provider.md)
- [認証](authentication-in-wcf.md)
