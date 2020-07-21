---
title: Windows Communication Foundation サンプルの 1 回限りのセットアップの手順
ms.date: 03/30/2017
ms.assetid: a5848ffd-3eb5-432d-812e-bd948ccb6bca
ms.openlocfilehash: 954ec04d2ef1ca7667b4f75a8a6652010b5dbd33
ms.sourcegitcommit: 43cbde34970f5f38f30c43cd63b9c7e2e83717ae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/11/2020
ms.locfileid: "81121628"
---
# <a name="one-time-setup-procedure-for-the-windows-communication-foundation-samples"></a>Windows Communication Foundation サンプルの 1 回限りのセットアップの手順

Windows 通信基盤 (WCF) のサンプルのほとんどは、インターネット インフォメーション サービス (IIS) でホストされ、共通の仮想ディレクトリから実行されます。 この 1 回限りのセットアップ手順では、ディスク上にフォルダが作成されます。また **、IIS**に仮想ディレクトリを追加します。

**仮想**ディレクトリは、IIS でホストされるサービスを使用するすべてのサンプルをビルドおよび実行するために使用されます。 サンプルの実行に必要な仮想ディレクトリはこれだけです。 サンプルをビルドすると、この仮想ディレクトリにある、以前に配置されたサービスがすべて置き換えられます。この仮想ディレクトリには最近ビルドされたサンプルだけが配置されるため、そのサンプルしか使用できません。

> [!NOTE]
> すべてのコマンドは、ローカル管理者アカウントで実行する必要があります。 Windows 7、Windows Vista、または Windows Server 2008 R2 を使用している場合は、管理者特権を使用してコマンド プロンプトも実行する必要があります。 これを行うには、コマンド プロンプト アイコンを右クリックし、[**管理者として実行**] をクリックします。 このトピックで使用するすべてのコマンドは、適切なパスが設定されているコマンド プロンプトで実行する必要があります。  このようにするための最も簡単な方法は、Visual Studio コマンド プロンプトを使用する方法です。 このプロンプトを開くには、[**スタート**] ボタンをクリックし、[**すべてのプログラム**] を選択**します。** **Visual Studio 2010** **Visual Studio Tools** **Visual Studio Command Prompt (2010)** Visual Studio Express Editions のいずれかがインストールされている場合は、このコマンド プロンプトを使用できません。この場合、システム パスに "C:\Windows\Microsoft.Net\Framework\v4.0" を追加する必要があります。

### <a name="one-time-setup-procedure-for-wcf-samples"></a>WCF サンプルの 1 回限りのセットアップの手順

1. ASP.NETがセットアップされていることを確認します。 ASP.NETの設定方法の詳細については、「[インターネット インフォメーション サービスのホスティング手順](internet-information-service-hosting-instructions.md)」を参照してください。

2. .NET Framework 4 がインストールされていることを確認します。 v4.0 (またはそれ以降) を次のディレクトリで検索**します**。

3. Visual Studio 2012 以降がインストールされているか、オペレーティング システムが Windows Server 2008 SP2 以降であることを確認します。

4. 次のコマンドを実行します。 これらのコマンドを実行する必要がある理由の詳細については、「 [IIS のホストされたサービスが失敗する](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms752252(v=vs.90))」を参照してください。

    > [!WARNING]
    > IIS を再インストールした場合は、次のコマンドを再実行します。

    ```console
    "%WINDIR%\Microsoft.Net\Framework\v4.0.30319\aspnet_regiis" –i –enable
    "%WINDIR%\Microsoft.Net\Framework\v4.0.30319\ServiceModelReg.exe" -r
    ```

    > [!WARNING]
    > このコマンド`aspnet_regiis –i –enable`を実行すると、.NET Framework 4 を使用して既定のアプリケーション プールが実行され、同じコンピューター上の他のアプリケーションに対して互換性の問題が発生する可能性があります。

5. サンプルで使用するポートを有効にするには、[ファイアウォールの指示](firewall-instructions.md)に従います。

6. 次の既定のディレクトリを確認\<してください: インストール ドライブ>:**\WF_WCF_Samples**。 サンプルが既にインストールされている場合は、これが既定のディレクトリです。

7. サンプルがインストールされていない場合は[、.NET Framework 4 の Windows コミュニケーション ファウンデーション (WCF) および Windows ワークフローファウンデーション (WF) サンプルからインストール](https://www.microsoft.com/download/details.aspx?id=21459)します。

8. サンプルをインストールした後、 \<**WF_WCF_Samples\\ **> 次の場所に移動します。

9. **Setupvroot.bat**バッチ ファイルを実行します。 次の手順を実行します。

    - ServiceModelSamples という名前の仮想ディレクトリが IIS に作成されます。

    - %SystemDrive%\Inetpub\wwwroot\ServiceModelSamples and %SystemDrive%\Inetpub\wwwroot\ServiceModelSamples\bin という名前の新しいディスク ディレクトリが作成されます。

    これらのディレクトリを手動でセットアップする場合は、[仮想ディレクトリのセットアップに関する説明](virtual-directory-setup-instructions.md)を参照してください。 この手順で行ったすべての変更を元に戻すには、サンプルの使用が終わった後で cleanupvroot.bat を実行します。

    > [!NOTE]
    > cleanupvroot.bat を実行しない限り、この手順を実行するのは、1 台のコンピューターで 1 回だけです。

10. サンプルおよび Network Service ユーザーのビルドに使用するアカウントに対し、%SystemDrive%\inetpub\wwwroot の変更権限を付与する必要があります。 ビルドの実行時に、Web ホストの一部のサンプルがコンパイル済みバイナリを前述の場所にコピーしようとする場合があり、適切な権限が設定されていないと、ビルドは破損します。 または、アクセス許可をそのままにして、SDK コマンド プロンプトまたは Visual Studio コマンド プロンプト (2012) を管理者として実行するか、Visual Studio 2012 でサンプルをビルドすることもできます。

    > [!NOTE]
    > この手順を完了していない場合は、ビルドの実行時に IIS でホストされているすべてのサンプルでエラーが発生します。 アクセス許可が正しく設定されていることを確認するか、SDK コマンド プロンプトと Visual Studio コマンド プロンプト (2012) を管理者として実行してください。

11. コンピューター上に C:\logs ディレクトリを作成します (一部のサンプルで必要になることがあります)。 このフォルダーに対する書き込みアクセスが適切なアカウントに付与されていることを確認してください。 Windows 7、Windows Vista、および Windows Server 2008 R2 の場合、このアカウントは**ネットワーク サービス**です。 Windows Server 2008 の場合、アカウントは NT 機関\ネットワーク サービスです。 Windows XP および Windows Server 2003 の場合、アカウントは ASPNET です。

12. Setupcerttool.bat ファイルを実行します。 このファイルは、\<インストール パス>\WF_WCF_Samples\WCF\セットアップ\ フォルダーにあります。  このスクリプトでは、次のタスクが実行されます。

    - FindPrivateKey ツールをビルドします。

    - %ProgramFiles%\ServiceModelSampleTools という名前のディレクトリを作成します。

    - 新しい FindPrivateKey ツールをこのディレクトリにコピーします。

    このツールは、証明書を使用して IIS でホストされるサンプルで必要です。

    > [!NOTE]
    > セキュリティの目的で、サンプルの使用が終わったら、このセットアップ手順で付与された仮想ディレクトリの定義とアクセス許可を必ず削除してください。削除するには、Cleanupvroot.bat という名前のバッチ ファイルを実行します。

13. 自己ホスト型の (IIS でホストされていない) サンプルでは、リッスンを行うコンピューター上で HTTP アドレスを登録するためのアクセス許可が必要です。 HTTP 名前空間予約のアクセス許可は、サンプルの実行に使用されるユーザー アカウントから提供されます。 既定では、管理者アカウントには、任意の HTTP アドレスを登録するためのアクセス許可があります。 管理者以外のアカウントの場合は、サンプルで使用される HTTP 名前空間へのアクセス許可が付与される必要があります。 名前空間の予約を構成する方法については、「[Configuring HTTP and HTTPS](../feature-details/configuring-http-and-https.md)」 (HTTP と HTTPS を構成する) を参照してください。

14. 一部のサンプルにはメッセージ キューが必要です。 インストール手順については、「[メッセージ キュー (MSMQ) のインストール」](installing-message-queuing-msmq.md)を参照してください。

    > [!NOTE]
    > メッセージ キューが必要なサンプルを実行する場合は、MSMQ サービスを事前に開始しておいてください。

15. 一部のサンプルには証明書が必要です。 「[インターネット インフォメーション サービス (IIS) サーバーの証明書をインストールするための指示に関するページ](iis-server-certificate-installation-instructions.md)」を参照してください。
