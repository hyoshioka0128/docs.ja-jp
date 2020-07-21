---
title: Visual Studio Code を使用して .NET Core コンソール アプリケーションを発行する
description: 発行では、.NET Core アプリケーションを実行するために必要なファイルのセットを作成します。
ms.date: 07/04/2020
ms.openlocfilehash: 8fd9975e8a88704b9dea45b40127c8dc03f7d09f
ms.sourcegitcommit: 0edbeb66d71b8df10fcb374cfca4d731b58ccdb2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/07/2020
ms.locfileid: "86051884"
---
# <a name="tutorial-publish-a-net-core-console-application-using-visual-studio-code"></a>チュートリアル: Visual Studio Code を使用して .NET Core コンソール アプリケーションを発行する

このチュートリアルでは、他のユーザーが実行できるコンソール アプリを発行する方法について説明します。 発行では、アプリケーションを実行するために必要なファイルのセットを作成します。 ファイルを配置するには、それをターゲット マシンにコピーします。

.NET Core CLI はアプリの発行に使用されるため、必要に応じて、Visual Studio Code 以外のコード エディターを使用してこのチュートリアルを実行することができます。

## <a name="prerequisites"></a>必須コンポーネント

- このチュートリアルでは、[Visual Studio Code での .NET Core コンソール アプリケーションの作成](with-visual-studio-code.md)に関するページで作成した、コンソール アプリを使用します。

## <a name="publish-the-app"></a>アプリの発行

1. Visual Studio Code を開始します。

1. [Visual Studio Code での .NET Core コンソール アプリケーションの作成](with-visual-studio-code.md)に関する記事で作成した *HelloWorld* プロジェクト フォルダーを開きます。

1. メイン メニューから **[表示]**  >  **[ターミナル]** の順に選択します。

   *[HelloWorld]* フォルダーでターミナルが開きます。

1. 次のコマンドを実行します。

   ```dotnetcli
   dotnet publish --configuration Release
   ```

   既定のビルド構成は "*デバッグ*" であるため、このコマンドでは "*リリース*" ビルド構成を指定します。 リリース ビルド構成の出力には、最小限のシンボリック デバッグ情報が含まれており、完全に最適化されています。

   コマンドの出力は次の例のようになります。

   ```
   Microsoft (R) Build Engine version 16.6.0+5ff7b0c9e for .NET Core
   Copyright (C) Microsoft Corporation. All rights reserved.

   Determining projects to restore...
   All projects are up-to-date for restore.
   HelloWorld -> C:\Projects\HelloWorld\bin\Release\netcoreapp3.1\HelloWorld.dll
   HelloWorld -> C:\Projects\HelloWorld\bin\Release\netcoreapp3.1\publish\
   ```

## <a name="inspect-the-files"></a>ファイルを検査する

この発行プロセスでは、フレームワークに依存する配置が既定で作成されます。これは、.NET Core のランタイムがインストールされているコンピューターで、発行されたアプリケーションが実行される配置の種類です。 発行されたアプリを実行するには、実行可能ファイルを使用するか、コマンド プロンプトから `dotnet HelloWorld.dll` コマンドを実行します。

次の手順で、発行プロセスによって作成されるファイルを確認します。

1. 左側のナビゲーション バーで **[エクスプローラー]** を選択します。

1. *bin/Release/netcoreapp3.1/publish* を展開します。

   :::image type="content" source="media/publishing-with-visual-studio-code/published-files-output.png" alt-text="発行されたファイルを表示しているエクスプローラー":::

   この図に示すように、発行された出力には次のファイルが含まれます。

   * *HelloWorld.deps.json*

      このファイルは、アプリケーションのランタイム依存関係ファイルです。 これは、アプリの実行に必要な .NET Core コンポーネントとライブラリ (アプリケーションが含まれる動的リンク ライブラリを含む) を定義します。 詳細については、「[ランタイム構成ファイル](https://github.com/dotnet/cli/blob/85ca206d84633d658d7363894c4ea9d59e515c1a/Documentation/specs/runtime-configuration-file.md)」を参照してください。

   * *HelloWorld.dll*

      これは、[フレームワークに依存する展開](../deploying/deploy-with-cli.md#framework-dependent-deployment)バージョンのアプリケーションです。 このダイナミック リンク ライブラリを実行するには、コマンド プロンプトで`dotnet HelloWorld.dll` を入力します。 アプリ実行のこの方法は、.NET Core ランタイムがインストールされている任意のプラットフォームで動作します。

   * *HelloWorld.exe* (Linux では *HelloWorld*、macOS では作成されません。)

      これは、[フレームワークに依存する実行可能ファイル](../deploying/deploy-with-cli.md#framework-dependent-executable) バージョンのアプリケーションです。 ファイルはオペレーティング システム固有のものです。

   * *HelloWorld.pdb* (配置は省略可能)

      これは、デバッグ シンボル ファイルです。 このファイルはアプリケーションと一緒に配置する必要はありませんが、発行されるバージョンのアプリケーションをデバッグする必要がある場合に保存しておく必要があります。

   * *HelloWorld.runtimeconfig.json*

      これは、アプリケーションのランタイム構成ファイルです。 ビルドされたアプリケーションが実行時に基盤とする .NET Core のバージョンを識別します。 構成オプションを追加することもできます。 詳細については、「[.NET Core ランタイム構成設定](../run-time-config/index.md#runtimeconfigjson)」を参照してください。

## <a name="run-the-published-app"></a>発行済みアプリを実行する

1. **エクスプローラー**で、*publish* フォルダーを右クリック (macOS では <kbd>Ctrl</kbd> キーを押しながらクリック) して、 **[ターミナルで開く]** を選択します。

   :::image type="content" source="media/publishing-with-visual-studio-code/open-in-terminal.png" alt-text="[ターミナルで開く] を表示しているコンテキスト メニュー":::

1. Windows または Linux では、実行可能ファイルを使用してアプリを実行します。

   1. Windows では、`.\HelloWorld.exe` を入力して、<kbd>Enter</kbd> キーを押します。

   1. Linux では、`./HelloWorld` を入力して、<kbd>Enter</kbd> キーを押します。

   1. プロンプトに応答して名前を入力し、任意のキーを押して終了します。

1. 任意のプラットフォームで、[`dotnet`](../tools/dotnet.md) コマンドを使用してアプリを実行します。

   1. 「`dotnet HelloWorld.dll`」と入力して、<kbd>Enter</kbd> キーを押します。

   1. プロンプトに応答して名前を入力し、任意のキーを押して終了します。

## <a name="additional-resources"></a>その他の技術情報

- [.NET Core アプリケーションの展開](../deploying/index.md)

## <a name="next-steps"></a>次の手順

このチュートリアルでは、コンソール アプリを発行しました。 次のチュートリアルでは、クラス ライブラリを作成します。

> [!div class="nextstepaction"]
> [Visual Studio Code で .NET Standard ライブラリを作成する](library-with-visual-studio-code.md)
