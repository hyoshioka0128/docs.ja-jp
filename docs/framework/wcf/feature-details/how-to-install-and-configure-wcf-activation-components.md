---
title: '方法: WCF アクティブ化コンポーネントをインストールして設定する'
description: Windows Vista で Windows プロセスアクティブ化サービス (WAS) をセットアップして、HTTP では通信しない WCF サービスをホストする方法について説明します。
ms.date: 03/30/2017
helpviewer_keywords:
- HTTP activation [WCF]
ms.assetid: 33a7054a-73ec-464d-83e5-b203aeded658
ms.openlocfilehash: 84a0dcc4fed28ebd7a536bdabfcdc389be6072d8
ms.sourcegitcommit: 358a28048f36a8dca39a9fe6e6ac1f1913acadd5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85246884"
---
# <a name="how-to-install-and-configure-wcf-activation-components"></a>方法: WCF アクティブ化コンポーネントをインストールして設定する

このトピックでは、windows Vista で Windows プロセスアクティブ化サービス (WAS) をセットアップして、HTTP ネットワークプロトコルでは通信しない Windows Communication Foundation (WCF) サービスをホストするために必要な手順について説明します。 以降の各セクションで、この構成に関する手順について概説します。

- WCF アクティブ化コンポーネントをインストール (または、のインストールを確認) します。

- 非 HTTP プロトコルをサポートようにする WAS を構成します。 次の手順では、TCP ライセンス認証用に Windows Vista を構成します。

WAS をインストールして構成した後、「 [How to: Host a Wcf service IN was](how-to-host-a-wcf-service-in-was.md) 」を参照して、was を使用する非 HTTP エンドポイントを公開する wcf サービスを作成する手順を参照してください。

## <a name="to-install-the-wcf-non-http-activation-components"></a>WCF 非 HTTP アクティブ化コンポーネントをインストールするには

1. **[スタート]** ボタンをクリックし、**[コントロール パネル]** をクリックします。

2. [**プログラム**] をクリックし、[**プログラムと機能**] をクリックします。

3. [**タスク**] メニューの [ **Windows の機能の有効化または無効化**] をクリックします。

4. WinFX ノードを見つけて、それを選択して展開します。

5. [ **WCF 非 Http アクティブ化コンポーネント**] チェックボックスをオンにして、設定を保存します。

## <a name="to-configure-the-was-to-support-tcp-activation"></a>TCP アクティベーションをサポートするように WAS を構成するには

1. net.tcp アクティベーションをサポートするには、既定の Web サイトをあらかじめ net.tcp ポートにバインドしておく必要があります。 これを行うには、IIS 7.0 管理ツールセットと共にインストールされる Appcmd.exe を使用します。 管理者レベルのコマンド プロンプト ウィンドウで、次のコマンドを実行します。

    ```console
    %windir%\system32\inetsrv\appcmd.exe set site "Default Web Site" -+bindings.[protocol='net.tcp',bindingInformation='808:*']
    ```

    > [!NOTE]
    > このコマンドはテキスト 1 行です。 このコマンドは、net.tcp サイト バインディングを、TCP ポート 808 で任意のホスト名をリッスンする既定の Web サイトに追加します。

2. サイト内のすべてのアプリケーションが同じ net.tcp バインディングを共有しますが、net.tcp サポートの有効化はアプリケーションごとに指定できます。 アプリケーションで net.tcp を有効にするには、管理者レベルのコマンド プロンプトから、次のコマンドを実行します。

    ```console
    %windir%\system32\inetsrv\appcmd.exe set app
    "Default Web Site/<WCF Application>" /enabledProtocols:http,net.tcp
    ```

    > [!NOTE]
    > このコマンドはテキスト 1 行です。 このコマンドは、 \<*WCF Application*> との両方を使用して、/アプリケーションにアクセスできるようにし `http://localhost/<WCF Application>` `net.tcp://localhost/<WCF Application>` ます。

     このサンプル用に追加した net.tcp サイト バインディングを削除します。

     便宜上次の 2 つの手順が、サンプル ディレクトリにある RemoveNetTcpSiteBinding.cmd というバッチ ファイルに実装されています。

    1. 管理者レベルのコマンド プロンプト ウィンドウで次のコマンドを実行して、有効なプロトコルの一覧から net.tcp を削除します。

        ```console
        %windir%\system32\inetsrv\appcmd.exe set app
        "Default Web Site/servicemodelsamples<WCF Application>" " /enabledProtocols:http
        ```

        > [!NOTE]
        > このコマンドはテキスト 1 行です。

    2. 権限のレベルが高いコマンド プロンプト ウィンドウで次のコマンドを実行して、net.tcp サイト バインディングを削除します。

        ```console
        %windir%\system32\inetsrv\appcmd.exe set site "Default Web Site"
        --bindings.[protocol='net.tcp',bindingInformation='808:*']
        ```

        > [!NOTE]
        > このコマンドはテキスト 1 行です。

## <a name="to-remove-nettcp-from-the-list-of-enabled-protocols"></a>有効なプロトコルの一覧から net.tcp を削除するには

1. 有効なプロトコルの一覧から net.tcp を削除するには、管理者レベルのコマンド プロンプト ウィンドウで次のコマンドを実行します。

    ```console
    %windir%\system32\inetsrv\appcmd.exe set app "Default Web Site/servicemodelsamples<WCF Application>" " /enabledProtocols:http
    ```

    > [!NOTE]
    > このコマンドはテキスト 1 行です。

## <a name="to-remove-the-nettcp-site-binding"></a>net.tcp サイト バインディングを削除するには

1. net.tcp サイト バインディングを削除するには、管理者レベルのコマンド プロンプト ウィンドウで次のコマンドを実行します。

    ```console
    %windir%\system32\inetsrv\appcmd.exe set site "Default Web Site"
    -bindings.[protocol='net.tcp',bindingInformation='808:*']
    ```

    > [!NOTE]
    > このコマンドはテキスト 1 行です。

## <a name="see-also"></a>関連項目

- [TCP アクティベーション](../samples/tcp-activation.md)
- [MSMQ アクティベーション](../samples/msmq-activation.md)
- [NamedPipe アクティベーション](../samples/namedpipe-activation.md)
- [AppFabric のホスティング機能](https://docs.microsoft.com/previous-versions/appfabric/ee677189(v=azure.10))
