---
title: カスタム バインディング セキュリティ
ms.date: 03/30/2017
ms.assetid: a6383dff-4308-46d2-bc6d-acd4e18b4b8d
ms.openlocfilehash: eb575594cec9ea714578bc104344acc14b00e9df
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84592464"
---
# <a name="custom-binding-security"></a>カスタム バインディング セキュリティ

このサンプルでは、カスタム バインディングを使用してセキュリティを構成する方法を示します。 カスタム バインドを使用して、セキュリティで保護されたトランスポートと共にメッセージ レベルのセキュリティを有効にする方法を示します。 これは、クライアントとサービス間でメッセージを転送する際にセキュリティで保護されたトランスポートが必要であると同時に、そのメッセージをメッセージ レベルでセキュリティ保護する必要がある場合に便利です。 この構成は、システム指定のバインディングではサポートされていません。

このサンプルは、クライアント コンソール プログラム (EXE) とサービス コンソール プログラム (EXE) で構成されています。 サービスは、双方向コントラクトを実装します。 このコントラクトは `ICalculatorDuplex` インターフェイスによって定義されており、算術演算 (加算、減算、乗算、および 除算) を公開しています。 `ICalculatorDuplex` インターフェイスを使用することにより、クライアントは算術演算を実行し、セッション経由で実行結果を計算できます。 サービスは、`ICalculatorDuplexCallback` インターフェイスで結果を個別に返すことができます。 コンテキストを確立して、クライアントとサービスの間で送信される一連のメッセージを相互に関連付ける必要があるため、二重のコントラクトにはセッションが必要です。 カスタム バインドは、双方向通信をサポートしてセキュリティで保護されるよう定義されます。

> [!NOTE]
> このサンプルのセットアップ手順とビルド手順については、このトピックの最後を参照してください。

サービス構成では、次をサポートするカスタム バインディングが定義されます。

- TLS/SSL プロトコルを使用して保護される TCP 通信。

- Windows メッセージ セキュリティ。

カスタム バインドの構成により、トランスポートのセキュリティ保護が有効になると同時に、メッセージ レベルのセキュリティも有効になります。 バインディング要素の順序は、カスタムバインディングを定義する際に重要です。これは、それぞれがチャネルスタック内のレイヤーを表しているためです (「[カスタムバインド](../extending/custom-bindings.md)」を参照してください)。 カスタム バインディングはサービスとクライアントの構成ファイルで定義されます。次のサンプル構成を参照してください。

```xml
<bindings>
  <!-- Configure a custom binding. -->
  <customBinding>
    <binding name="Binding1">
      <security authenticationMode="SecureConversation"
                 requireSecurityContextCancellation="true">
      </security>
      <textMessageEncoding messageVersion="Soap12WSAddressing10" writeEncoding="utf-8"/>
      <sslStreamSecurity requireClientCertificate="false"/>
      <tcpTransport/>
    </binding>
  </customBinding>
</bindings>
```

カスタム バインドはサービス証明書を使用して、トランスポート レベルでサービスを認証し、クライアントとサービス間で転送中のメッセージを保護します。 これは `sslStreamSecurity` バインド要素によって実現されます。 サービスの証明書は、サービス動作を使用して構成されます。次のサンプル構成を参照してください。

```xml
<behaviors>
    <serviceBehaviors>
    <behavior name="CalculatorServiceBehavior">
        <serviceMetadata />
        <serviceDebug includeExceptionDetailInFaults="False" />
        <serviceCredentials>
        <serviceCertificate findValue="localhost" storeLocation="LocalMachine" storeName="My" x509FindType="FindBySubjectName"/>
        </serviceCredentials>
    </behavior>
    </serviceBehaviors>
</behaviors>
```

さらに、カスタム バインドは Windows 資格情報の種類 (既定の資格情報の種類) によるメッセージ セキュリティを使用します。 これは `security` バインド要素によって実現されます。 Kerberos 認証機構が利用できる場合は、クライアントとサービスはどちらもメッセージ レベルのセキュリティを使用して認証されます。 サンプルを Active Directory 環境で実行する場合、この認証が行われます。 Kerberos 認証機構が利用できない場合は、NTLM 認証が使用されます。 NTLM はサービスに対してクライアントを認証しますが、クライアントに対するサービスの認証は行いません。 `security`バインド要素は、を使用するように構成されます `SecureConversation` `authenticationType` 。これにより、クライアントとサービスの両方でセキュリティセッションが作成されます。 これは、サービスの双方向コントラクトを動作させるために必要です。

このサンプルを実行する場合は、操作要求および応答はクライアントのコンソール ウィンドウに表示されます。 クライアントをシャットダウンするには、クライアント ウィンドウで Enter キーを押します。

```console
Press <ENTER> to terminate client.
Result(100)
Result(50)
Result(882.5)
Result(441.25)
Equation(0 + 100 - 50 * 17.65 / 2 = 441.25)
```

サンプルを実行すると、クライアントに戻ってきたメッセージがサービスから送信されたコールバック インターフェイスに表示されます。 それぞれの中間結果が表示され、その後にすべての操作が完了したときの数式全体が表示されます。 Enter キーを押してクライアントをシャットダウンします。

サンプルに用意されている Setup.bat ファイルを使用すると、適切なサービス証明書を使用してクライアントとサーバーを構成し、証明書ベースのセキュリティを必要とするホスト アプリケーションを実行できるようになります。 このバッチ ファイルは、複数のコンピューターを使用する場合またはホストなしの場合に応じて変更する必要があります。

次に、このサンプルに適用されるバッチ ファイルのセクションのうち、該当する構成で実行するために変更が必要となる部分を示します。

- サーバー証明書の作成。

  Setup.bat ファイルの次の行は、使用するサーバー証明書を作成します。 `%SERVER_NAME%` 変数はサーバー名です。 この変数を変更して、使用するサーバー名を指定します。 このバッチ ファイルでのサーバー名の既定は localhost です。

  Web ホスト サービスの場合、証明書は CurrentUser ストアに格納されます。

  ```bat
  echo ************
  echo Server cert setup starting
  echo %SERVER_NAME%
  echo ************
  echo making server cert
  echo ************
  makecert.exe -sr LocalMachine -ss MY -a sha1 -n CN=%SERVER_NAME% -sky exchange -pe
  ```

- クライアントの信頼された証明書ストアへのサーバー証明書のインストール。

  Setup.bat ファイルの次の行は、サーバー証明書をクライアントの信頼されたユーザーのストアにコピーします。 この手順が必要なのは、Makecert.exe によって生成される証明書がクライアント システムにより暗黙には信頼されないからです。 マイクロソフト発行の証明書など、クライアントの信頼されたルート証明書に基づいた証明書が既にある場合は、クライアント証明書ストアにサーバー証明書を配置するこの手順は不要です。

  ```console
  certmgr.exe -add -r LocalMachine -s My -c -n %SERVER_NAME% -r CurrentUser -s TrustedPeople
  ```

  > [!NOTE]
  > Setup.bat バッチ ファイルは、Visual Studio 2010 コマンド プロンプトから実行します。 MSSDK 環境変数が SDK のインストール ディレクトリを指している必要があります。 この環境変数は、Visual Studio 2010 コマンド プロンプトで自動設定されます。

### <a name="to-set-up-build-and-run-the-sample"></a>サンプルをセットアップ、ビルド、および実行するには

1. [Windows Communication Foundation サンプルの1回限りのセットアップ手順](one-time-setup-procedure-for-the-wcf-samples.md)を実行したことを確認します。

2. ソリューションの C# 版または Visual Basic .NET 版をビルドするには、「 [Building the Windows Communication Foundation Samples](building-the-samples.md)」の手順に従います。

3. サンプルを単一コンピューター構成または複数コンピューター構成で実行するには、「 [Windows Communication Foundation サンプルの実行](running-the-samples.md)」の手順に従います。

### <a name="to-run-the-sample-on-the-same-computer"></a>サンプルを同じコンピューターで実行するには

1. 管理者特権で Visual Studio の開発者コマンドプロンプトを開き、サンプルのインストールフォルダーから Setup.exe を実行します。 これにより、サンプルの実行に必要なすべての証明書がインストールされます。

    > [!NOTE]
    > セットアップの .bat バッチファイルは、Visual Studio 2012 のコマンドプロンプトから実行するように設計されています。 Visual Studio 2012 のコマンドプロンプト内で設定された PATH 環境変数は、セットアップの .bat スクリプトで必要な実行可能ファイルが格納されているディレクトリを指します。

2. Service.exe を \service\bin で起動します。

3. Client.exe を \client\bin で起動します。 クライアント アクティビティがクライアントのコンソール アプリケーションに表示されます。

4. クライアントとサービスが通信できない場合は、「 [WCF サンプルのトラブルシューティングのヒント](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms751511(v=vs.90))」を参照してください。

### <a name="to-run-the-sample-across-computers"></a>サンプルを複数のコンピューターで実行するには

1. サービス コンピューター上で次の手順を実行します。

    1. サービス コンピューターで、servicemodelsamples という仮想ディレクトリを作成します。

    2. サービス プログラム ファイルを \inetpub\wwwroot\servicemodelsamples からサービス コンピューターの仮想ディレクトリにコピーします。 ファイルのコピー先が \bin サブディレクトリであることを確認します。

    3. Setup.bat ファイルと Cleanup.bat ファイルをサービス コンピューターにコピーします。

    4. 管理者特権で Visual Studio を開いた開発者コマンドプロンプトで、次のコマンドを実行し `Setup.bat service` ます。 これにより、バッチ ファイルが実行されたコンピューターの名前と一致するサブジェクト名を持つ、サービス証明書が作成されます。

        > [!NOTE]
        > Setup.bat バッチ ファイルは、Visual Studio 2010 コマンド プロンプトから実行します。 path 環境変数が SDK のインストール ディレクトリを指している必要があります。 この環境変数は、Visual Studio 2010 コマンド プロンプトで自動設定されます。

    5. 前の [\<serviceCertificate>](../../configure-apps/file-schema/wcf/servicecertificate-of-servicecredentials.md) 手順で生成された証明書のサブジェクト名を反映するように、サービスの .exe ファイル内のを変更します。

    6. コマンド プロンプトから Service.exe を起動します。

2. クライアント コンピューターでの操作:

    1. クライアント プログラム ファイルを、\client\bin\ フォルダーからクライアント コンピューターにコピーします。 Cleanup.bat ファイルもコピーします。

    2. Cleanup.bat を実行して、前のサンプルから古い証明書を削除します。

    3. 管理者特権で Visual Studio の開発者コマンドプロンプトを開き、サービスコンピューターで次のコマンドを実行して、サービスの証明書をエクスポートします (サービス `%SERVER_NAME%` が実行されているコンピューターの完全修飾名に置き換えます)。

        ```console
        certmgr -put -r LocalMachine -s My -c -n %SERVER_NAME% %SERVER_NAME%.cer
        ```

    4. %SERVER_NAME%.cer をクライアント コンピューターにコピーします (%SERVER_NAME% は、サービスが実行されているコンピューターの完全修飾名に置き換えてください)。

    5. 管理者特権で Visual Studio の開発者コマンドプロンプトを開き、クライアントコンピューターで次のコマンドを実行して、サービスの証明書をインポートします (% SERVER_NAME% は、サービスが実行されているコンピューターの完全修飾名に置き換えます)。

        ```console
        certmgr.exe -add -c %SERVER_NAME%.cer -s -r CurrentUser TrustedPeople
        ```

        証明書が信頼できる発行元から発行されている場合は、手順 c.、d.、および e. は不要です。

    6. 次のようにクライアントの App.config ファイルを変更します。

        ```xml
        <client>
            <endpoint name="default"
                address="net.tcp://ReplaceThisWithServiceMachineName:8000/ServiceModelSamples/Service"
                binding="customBinding"
                bindingConfiguration="Binding1"
                contract="Microsoft.ServiceModel.Samples.ICalculatorDuplex"
                behaviorConfiguration="CalculatorClientBehavior" />
        </client>
        ```

    7. ドメイン環境でサービスが NetworkService または LocalSystem 以外のアカウントで実行されている場合は、クライアントの App.config ファイル内のサービス エンドポイントのエンドポイント ID を変更し、サービスの実行に使用されているアカウントに基づいて、適切な UPN または SPN を設定する必要がある場合があります。 エンドポイント id の詳細については、「[サービス id と認証](../feature-details/service-identity-and-authentication.md)」トピックを参照してください。

    8. コマンド プロンプトから Client.exe を起動します。

### <a name="to-clean-up-after-the-sample"></a>サンプルの実行後にクリーンアップするには

- サンプルの実行が終わったら、サンプル フォルダーにある Cleanup.bat を実行します。
