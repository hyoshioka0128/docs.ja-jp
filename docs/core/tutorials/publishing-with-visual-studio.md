---
title: Visual Studio を使用して .NET Core コンソール アプリケーションを発行する
description: 発行では、.NET Core アプリケーションを実行するために必要なファイルのセットを作成します。
ms.date: 06/08/2020
dev_langs:
- csharp
- vb
ms.custom: vs-dotnet
ms.openlocfilehash: 44646a307d230db395b55b9dec5acfd168605940
ms.sourcegitcommit: 1cbd77da54405ea7dba343ac0334fb03237d25d2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/11/2020
ms.locfileid: "84701285"
---
# <a name="tutorial-publish-a-net-core-console-application-using-visual-studio"></a>チュートリアル: Visual Studio を使用して .NET Core コンソール アプリケーションを発行する

このチュートリアルでは、他のユーザーが実行できるコンソール アプリを発行する方法について説明します。 発行では、アプリケーションを実行するために必要なファイルのセットを作成します。 ファイルを配置するには、それをターゲット マシンにコピーします。

## <a name="prerequisites"></a>必須コンポーネント

- このチュートリアルでは、[Visual Studio 2019 での .NET Core コンソール アプリケーションの作成](with-visual-studio.md)に関するページで作成した、コンソール アプリを使用します。

## <a name="publish-the-app"></a>アプリの発行

1. Visual Studio を起動します。

1. [Visual Studio での .NET Core コンソール アプリケーションの作成](with-visual-studio.md)に関する記事で作成した *HelloWorld* プロジェクトを開きます。

1. Visual Studio でリリース ビルド構成が使用されていることを確認します。 必要に応じて、ツール バーのビルド構成の設定を **[デバッグ]** から **[リリース]** に変更します。

   ![リリース ビルドが選択された Visual Studio のツールバー](media/publishing-with-visual-studio/visual-studio-toolbar-release.png)

1. **HelloWorld** プロジェクト (HelloWorld ソリューションではなく) を右クリックし、メニューから **[発行]** を選びます。

   ![Visual Studio の [発行] コンテキスト メニュー](media/publishing-with-visual-studio/publish-context-menu.png)

1. **[発行]** ページの **[ターゲット]** タブで、 **[フォルダー]** 、 **[次へ]** の順に選択します。

   ![Visual Studio で発行先を選択します](media/publishing-with-visual-studio/pick-publish-target.png)

1. **[発行]** ページの **[場所]** タブで、 **[完了]** を選択します。

   ![Visual Studio の [発行] ページの [場所] タブ](media/publishing-with-visual-studio/publish-page-loc-tab.png)

1. **[発行]** ウィンドウの **[発行]** タブで、 **[発行]** を選択します。

   ![Visual Studio の [発行] ウィンドウ](media/publishing-with-visual-studio/publish-page.png)

## <a name="inspect-the-files"></a>ファイルを検査する

この発行プロセスでは、フレームワークに依存する配置が既定で作成されます。これは、.NET Core ランタイムがインストールされているコンピューター上で発行されたアプリケーションが実行される配置の種類です。 ユーザーは、実行可能ファイルをダブルクリックするか、コマンドプロンプトから `dotnet HelloWorld.dll` コマンドを実行することで、発行されたアプリを実行できます。

次の手順で、発行プロセスによって作成されるファイルを確認します。

1. **ソリューション エクスプローラー**で、 **[すべてのファイルを表示]** を選択します。

1. プロジェクト フォルダーで *bin/Release/netcoreapp3.1/publish* を展開します。

   :::image type="content" source="media/publishing-with-visual-studio/published-files-output.png" alt-text="発行されたファイルを表示しているソリューション エクスプローラー":::

   この図に示すように、発行された出力には次のファイルが含まれます。

   * *HelloWorld.deps.json*

      このファイルは、アプリケーションのランタイム依存関係ファイルです。 これは、アプリの実行に必要な .NET Core コンポーネントとライブラリ (アプリケーションが含まれる動的リンク ライブラリを含む) を定義します。 詳細については、「[ランタイム構成ファイル](https://github.com/dotnet/cli/blob/85ca206d84633d658d7363894c4ea9d59e515c1a/Documentation/specs/runtime-configuration-file.md)」を参照してください。

   * *HelloWorld.dll*

      これは、[フレームワークに依存する展開](../deploying/deploy-with-cli.md#framework-dependent-deployment)バージョンのアプリケーションです。 このダイナミック リンク ライブラリを実行するには、コマンド プロンプトで`dotnet HelloWorld.dll` を入力します。 アプリ実行のこの方法は、.NET Core ランタイムがインストールされている任意のプラットフォームで動作します。

   * *HelloWorld.exe*

      これは、[フレームワークに依存する実行可能ファイル](../deploying/deploy-with-cli.md#framework-dependent-executable) バージョンのアプリケーションです。 これを実行するには、コマンド プロンプトで `HelloWorld.exe` を入力します。 ファイルはオペレーティング システム固有のものです。

   * *HelloWorld.pdb* (配置は省略可能)

      これは、デバッグ シンボル ファイルです。 このファイルはアプリケーションと一緒に配置する必要はありませんが、発行されるバージョンのアプリケーションをデバッグする必要がある場合に保存しておく必要があります。

   * *HelloWorld.runtimeconfig.json*

      これは、アプリケーションのランタイム構成ファイルです。 ビルドされたアプリケーションが実行時に基盤とする .NET Core のバージョンを識別します。 構成オプションを追加することもできます。 詳細については、「[.NET Core ランタイム構成設定](../run-time-config/index.md#runtimeconfigjson)」を参照してください。

## <a name="run-the-published-app"></a>発行済みアプリを実行する

1. **ソリューション エクスプローラー**で、 *[publish]* フォルダーを右クリックし、 **[完全なパスのコピー]** を選択します。

1. コマンド プロンプトを開いて、*publish* フォルダーに移動します。 これを行うには、「`cd`」と入力して、完全なパスを貼り付けます。 次に例を示します。

   ```
   cd C:\Projects\HelloWorld\bin\Release\netcoreapp3.1\publish\
   ```

1. 実行可能ファイルを使用してアプリを実行します。

   1. 「`HelloWorld.exe`」と入力して、<kbd>Enter</kbd> キーを押します。

   1. プロンプトに応答して名前を入力し、任意のキーを押して終了します。

1. `dotnet` コマンドを使用して、アプリを実行します。

   1. 「`dotnet HelloWorld.dll`」と入力して、<kbd>Enter</kbd> キーを押します。

   1. プロンプトに応答して名前を入力し、任意のキーを押して終了します。

## <a name="additional-resources"></a>その他の技術情報

- [.NET Core アプリケーションの展開](../deploying/index.md)

## <a name="next-steps"></a>次の手順

このチュートリアルでは、コンソール アプリを発行しました。 次のチュートリアルでは、クラス ライブラリを作成します。

> [!div class="nextstepaction"]
> [Visual Studio で .NET Standard ライブラリを構築する](library-with-visual-studio.md)
