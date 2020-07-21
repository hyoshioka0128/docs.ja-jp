---
title: '方法: ユーザー名とパスワードで認証する'
description: WCF サービスで、Windows ドメインのユーザー名とパスワードをサンプルコードと共に使用して、クライアントを認証できるようにする方法について説明します。
ms.date: 03/30/2017
helpviewer_keywords:
- authentication [WCF], user name and password
ms.assetid: a5415be2-0ef3-464c-9f76-c255cb8165a4
ms.openlocfilehash: 1f938f8041b2577b3705266948f29b42f23a6fd7
ms.sourcegitcommit: 358a28048f36a8dca39a9fe6e6ac1f1913acadd5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85247248"
---
# <a name="how-to-authenticate-with-a-user-name-and-password"></a>方法: ユーザー名とパスワードで認証する

このトピックでは、Windows Communication Foundation (WCF) サービスを有効にして、Windows ドメインのユーザー名とパスワードを使用してクライアントを認証する方法について説明します。 自己ホスト型 WCF サービスが稼働していることを前提としています。 基本的な自己ホスト型 WCF サービスを作成する例については、[はじめにチュートリアル](../getting-started-tutorial.md)を参照してください。 このトピックでは、サービスがコードで構成されているものとします。 構成ファイルを使用して同様のサービスを構成する例については、「[メッセージセキュリティユーザー名](../samples/message-security-user-name.md)」を参照してください。

Windows ドメイン ユーザー名とパスワードを使用してクライアントを認証するようにサービスを構成するには、<xref:System.ServiceModel.WSHttpBinding> を使用し、その `Security.Mode` プロパティを `Message` に設定します。 また、ユーザー名とパスワードをクライアントからサービスに送信するときに X.509 証明書を指定する必要があります。この証明書は、ユーザー名とパスワードの暗号化に使用されます。

クライアント側では、ユーザーにユーザー名とパスワードの入力を求め、WCF クライアント プロキシでユーザーの資格情報を指定する必要があります。

## <a name="to-configure-a-wcf-service-to-authenticate-using-windows-domain-username-and-password"></a>Windows ドメインのユーザー名とパスワードを使用して認証するように WCF サービスを構成するには

1. 次のコードに示すように、<xref:System.ServiceModel.WSHttpBinding> のインスタンスを作成し、バインディングのセキュリティ モードを <xref:System.ServiceModel.WSHttpSecurity.Message?displayProperty=nameWithType> に設定した後、バインディングの `ClientCredentialType` を <xref:System.ServiceModel.MessageCredentialType.UserName?displayProperty=nameWithType> に設定し、構成されたバインディングを使用するサービス エンドポイントをサービス ホストに追加します。

    ```csharp
    // ...
    var userNameBinding = new WSHttpBinding();
    userNameBinding.Security.Mode = SecurityMode.Message;
    userNameBinding.Security.Message.ClientCredentialType = MessageCredentialType.UserName;
    svcHost.AddServiceEndpoint(typeof(IService1), userNameBinding, "");
    // ...
    ```

2. ネットワーク経由で送信されるユーザー名とパスワードの情報を暗号化するために使用するサーバー証明書を指定します。 次のコードは、上記のコードの直後に追加します。 次の例では、[メッセージセキュリティユーザー名](../samples/message-security-user-name.md)のサンプルから、setup.bat ファイルによって作成された証明書を使用します。

    ```csharp
    // ...
    svcHost.Credentials.ServiceCertificate.SetCertificate(StoreLocation.LocalMachine, StoreName.My, X509FindType.FindBySubjectName, "localhost");
    // ...
    ```

    独自の証明書を使用する場合は、その証明書を参照するようにコードを変更します。 証明書の作成と使用の詳細については、「[証明書の](working-with-certificates.md)使用」を参照してください。 証明書がローカル コンピューターの信頼されたユーザー証明書ストア内に存在することを確認します。 これを行うには、mmc.exe を実行し、[**ファイル**] メニューの [スナップインの**追加と削除**] メニュー項目を選択します。 [スナップインの**追加と削除**] ダイアログで、[**証明書] スナップ**インを選択し、[**追加**] をクリックします。 [証明書スナップイン] ダイアログで、[**コンピューターアカウント**] を選択します。 既定では、「メッセージ セキュリティ ユーザー名」のサンプルから生成された証明書は個人/証明書フォルダーに配置されます。  これは、MMC ウィンドウの [発行先] 列の下に "localhost" として表示されます。 証明書を [**信頼さ**れた People] フォルダーにドラッグアンドドロップします。 これにより、WCF は、認証の実行時に、証明書を信頼された証明書として処理することができます。

## <a name="to-call-the-service-passing-username-and-password"></a>ユーザー名とパスワードを渡すサービスを呼び出すには

1. クライアント アプリケーションは、ユーザー名とパスワードの入力をユーザーに求める必要があります。 次のコードでは、ユーザーにユーザー名とパスワードの入力を求めています。

    > [!WARNING]
    > このコードは、入力中のパスワードが表示されるため、運用環境では使用しないでください。

    ```csharp
    public static void GetPassword(out string username, out string password)
    {
        Console.WriteLine("Provide a valid machine or domain account. [domain\\user]");
        Console.WriteLine("   Enter username:");
        username = Console.ReadLine();
        Console.WriteLine("   Enter password:");
        password = Console.ReadLine();
    }
    ```

2. 次のコードに示すように、クライアントの資格情報を指定して、クライアントプロキシのインスタンスを作成します。

    ```csharp
    string username;
    string password;

    // Instantiate the proxy.
    var proxy = new Service1Client();

    // Prompt the user for username & password.
    GetPassword(out username, out password);

    // Set the user's credentials on the proxy.
    proxy.ClientCredentials.UserName.UserName = username;
    proxy.ClientCredentials.UserName.Password = password;

    // Treat the test certificate as trusted.
    proxy.ClientCredentials.ServiceCertificate.Authentication.CertificateValidationMode = System.ServiceModel.Security.X509CertificateValidationMode.PeerOrChainTrust;
    // Call the service operation using the proxy
    ```

## <a name="see-also"></a>関連項目

- <xref:System.ServiceModel.WSHttpBinding>
- <xref:System.ServiceModel.WSHttpSecurity>
- <xref:System.ServiceModel.SecurityMode>
- <xref:System.ServiceModel.Security.UserNamePasswordClientCredential.UserName%2A>
- <xref:System.ServiceModel.Security.UserNamePasswordClientCredential.Password%2A>
- <xref:System.ServiceModel.Security.UserNamePasswordClientCredential>
- <xref:System.ServiceModel.WSHttpSecurity.Mode%2A>
- <xref:System.ServiceModel.HttpTransportSecurity.ClientCredentialType%2A>
- [基本認証でのトランスポート セキュリティ](transport-security-with-basic-authentication.md)
- [分散アプリケーションのセキュリティ](distributed-application-security.md)
- [\<wsHttpBinding>](../../configure-apps/file-schema/wcf/wshttpbinding.md)
