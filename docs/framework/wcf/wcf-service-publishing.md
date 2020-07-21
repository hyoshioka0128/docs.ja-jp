---
title: WCF サービス発行
description: WCF サービスの公開は、テスト目的でアプリケーションを運用環境に配置するのに役立ちます。
ms.date: 03/30/2017
ms.assetid: c806b253-cd47-4b96-b831-e73cbf08808f
ms.openlocfilehash: 99798b75e1dc01c8db361f4d8d1f162c7f7617b1
ms.sourcegitcommit: 358a28048f36a8dca39a9fe6e6ac1f1913acadd5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85245675"
---
# <a name="wcf-service-publishing"></a>WCF サービス発行

Windows Communication Foundation (WCF) サービス公開は、WCF サービスホストと WCF テストクライアントによって提供される初期の開発環境から、テスト目的で実際にアプリケーションを運用環境に配置するために役立ちます。 最終的な配置計画にコミットする前に、Windows Communication Foundation (WCF) サービス発行を使用して、WCF サービスが正常に実行され、公開する準備が整っていることを確認できます。 また、WCF サービスライブラリをテスト用のさまざまなターゲットの場所に配置することもできます。

## <a name="supported-services-and-target-locations"></a>サポートされているサービスとターゲットの場所

Wcf サービスの公開では、wcf サービスライブラリテンプレートのセットから作成された WCF サービスと、それに対応する項目テンプレート (次のものを含む) の公開をサポートしています。

- 項目テンプレートを含む WCF サービスライブラリテンプレート。

- 配信サービス ライブラリ

これらのサービステンプレートを見つけるには、[**ファイル**]  >  **[新しいプロジェクト**> [**Visual Basic**または**Visual C#**] > **WCF**] を選択します。 この場所 (WCF ワークフローサービスアプリケーションや WCF サービスアプリケーションなど) のその他の WCF テンプレートについては、 [web アプリケーションのワンクリック発行](https://docs.microsoft.com/previous-versions/aspnet/dd465337(v=vs.110))を使用して発行できます。

サービスは、次のターゲットの場所に発行できます。

- ローカル IIS

- ファイル システム。

- FTP サイト

## <a name="using-wcf-service-publishing"></a>WCF サービス発行の使用

サービス実装を配置するには、次の手順を実行します。

1. 昇格した特権で Visual Studio を開きます (実行可能ファイルを右クリックし、[**管理者として実行**] を選択して開きます)。  IIS 7.0 以降を使用している場合は、コントロールパネルの [Windows の機能の有効化または無効化] を使用して、"IIS メタベースと IIS6 の構成の互換性" コンポーネントがインストールされていることを確認します。

2. サービスプロジェクトを開き、メインメニューから [**ビルド**] [発行  >  ** \<Project Name> ** ] を選択するか、**ソリューションエクスプローラー**でプロジェクトを右クリックして [**発行**] をクリックします。

3. [**発行**] ウィンドウが表示されます。 [... **] をクリック**します。 サービスの配置先にするターゲットの場所を指定します。 ローカルの IIS、ファイルシステム、または FTP サイトにアプリケーションを配置するように選択できます。 ローカル IIS にアプリケーションを配置する場合は、右上隅にある [**新しい Web アプリケーションの作成**] アイコンをクリックして、web サイトを選択し、その下に web アプリケーションを作成できます。

4. メインウィンドウで [**発行**] をクリックすると、Visual Studio によってアプリケーションが指定したターゲットの場所に配置され、Web.config、.svc、およびアセンブリファイルがターゲットディレクトリにコピーされます。 . .Svc の名前は "ProjectName. ServiceName. svc" になります。 サービスが正常に発行されると、Visual Studio の [出力] ウィンドウにホットリンクが表示されます。これは、"接続先" のように `http://localhost/WebApplicationFolderName...` なります。 Ctrl キーを押しながらリンクをクリックすると、Visual Studio の内側にブラウザー ページが開き、サービス ディレクトリ構造が表示されます。

     サイトを参照できない場合、IIS でディレクトリ ブラウザーが有効になっていない可能性があります。 有効にするには、「試してみてください」セクションのヒントに従ってください。 または、直接入力し `http://localhost/WebApplicationFolderName/ProjectName.ServiceName.svc` てサービスページを表示することもできます。

**Publish**を使用して、プロジェクトで定義されているすべてのサービスのアセンブリ、構成、.svc ファイルをターゲットの場所にコピーし、既存のファイルを転送先に上書きするかどうかを指定できます。

ローカルの IIS にアプリケーションを配置すると、IIS セットアップに関連するエラーが発生することがあります。 IIS が正しくインストールされていることを確認してください。 `http://localhost`ブラウザーのアドレスバーに「」と入力して、IIS の既定のページが表示されているかどうかを確認できます。 場合によっては、IIS での ASP.NET または WCF の不適切な登録によって問題が発生することもあります。 Visual Studio の開発者コマンドプロンプトを開き、コマンドを実行して `aspnet_regiis.exe -ir` ASP.NET 登録の問題を修正するか、コマンドを実行して `ServiceModelReg.exe –ia` WCF の登録に関する問題を修正することができます。

## <a name="files-generated-for-publishing"></a>発行用に生成されるファイル
 WCF サービスライブラリを Web ホストできるようにするには、ツールによって、アセンブリファイル、Web.config ファイル、および .svc ファイルの各ファイルが生成されます。 生成されたファイルは、すべてターゲットの場所にコピーされます。 その後でサービスが発行されます。

### <a name="assembly-files"></a>アセンブリ ファイル
 このツールを使用して WCF サービスを公開すると、サービスが最初に自動的に構築され、ビルド後にアセンブリファイルがサービスプロジェクトで生成されます。

### <a name="svc-file"></a>.SVC ファイル
 発行操作により、ファイルが存在するかどうかにかかわらず、各 WCF サービスの * .svc ファイルが生成され、バージョンの有効性が保証されます。 Svc ファイルには2種類あります。1つは WCF サービスライブラリおよび配信サービスライブラリ用で、もう1つはシーケンシャルおよびステートマシンワークフローサービスライブラリ用です。 生成された \* .svc ファイルが、ターゲットの場所のルートフォルダーにコピーされます。

### <a name="webconfig-file"></a>Web.config ファイル
 サービス プロジェクトが特定のターゲットの場所に発行されるたびに、Web.config ファイルが作成されます。

 生成された Web.config ファイルには、Web ホスティングに役立つ Web セクションと、WCF サービスライブラリの App.config の内容 (次の変更があります) が含まれています。

- ベース アドレスが除外されています。

- ターゲット プラットフォームのトレース設定を保持するために、`<diagnostics>` 要素の設定が除外されています。

## <a name="publishing-wcf-services-with-non-http-bindings-to-iis"></a>IIS への非 HTTP バインドを使用した WCF サービスの公開
 IIS 7.0 以降を使用している場合は、IIS に HTTP 以外のバインドを使用して WCF サービスを公開できます。 事前の構成を行う必要があります。 詳細については、「 [Windows プロセスアクティブ化サービスでのホスト](./feature-details/hosting-in-windows-process-activation-service.md)」のトピックを参照してください。

## <a name="security"></a>Security
 IIS は管理者アカウントで実行する必要があるため、ローカル IIS に発行するには、管理特権が必要です。 管理者特権を持たないユーザーが WCF サービス公開を開く場合、IIS はターゲットの場所として使用できません。 ファイルシステムまたは FTP サイトへの発行は、管理者特権なしで動作します。

## <a name="see-also"></a>関連項目

- [WCF Visual Studio テンプレート](wcf-vs-templates.md)
- [WCF サービス ホスト (WcfSvcHost.exe)](wcf-service-host-wcfsvchost-exe.md)
- [WCF のテスト用クライアント (WcfTestClient.exe)](wcf-test-client-wcftestclient-exe.md)
