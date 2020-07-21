---
title: Docker アプリの開発環境
description: Docker 開発ライフサイクルをサポートする最も重要な開発ツールのオプションについて説明します。
ms.date: 04/16/2020
ms.openlocfilehash: b1df16db88fa85f794407c989f5428030c4cddf7
ms.sourcegitcommit: 046a9c22487551360e20ec39fc21eef99820a254
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/14/2020
ms.locfileid: "83394897"
---
# <a name="development-environment-for-docker-apps"></a>Docker アプリの開発環境

## <a name="development-tools-choices-ide-or-editor"></a>開発ツールの選択:IDE またはエディター

完全で強力な IDE または軽量でアジャイルなエディターのどちらを選んでも、Microsoft は Docker アプリケーションの開発時に対応できます。

### <a name="visual-studio-code-and-docker-cli-cross-platform-tools-for-mac-linux-and-windows"></a>Visual Studio Code と Docker CLI (Mac、Linux および Windows 用のクロスプラットフォーム ツール)

任意の開発言語をサポートする軽量なクロスプラットフォーム エディターを選択すると、Visual Studio Code と Docker CLI を使用することができます。 これらの製品は、シンプルかつ堅牢性の高いエクスペリエンスを提供しますが、このことは開発者のワークフローを効率化するために不可欠です。 Docker 開発者は、"Docker for Mac" または "Docker for Windows" (開発環境) をインストールすることで、1 つの Docker CLI を使用して Windows と Linux (実行時環境) 用の両方のアプリを構築することができます。 さらに、Visual Studio Code は、Dockerfile 用の IntelliSense を含む Docker の拡張機能や、エディターから Docker コマンドを実行するショートカット タスクをサポートします。

> [!NOTE]
> Visual Studio Code をダウンロードするには <https://code.visualstudio.com/download> を参照してください。
>
> Mac および Windows 用 Docker をダウンロードするには <https://www.docker.com/products/docker> を参照してください。

### <a name="visual-studio-with-docker-tools-windows-development-machine"></a>Docker ツールを備えた Visual Studio (Windows の開発用コンピューター)

組み込みの Docker ツールが有効にされた Visual Studio 2019 を使用することをお勧めします。 Visual Studio により、選択した Docker 環境で、直接アプリケーションの開発、実行、および検証ができます。 F5 キーを押すと、Docker ホスト内で直接アプリケーション (1 つのコンテナー、または複数のコンテナー) をデバッグできます。または、Ctrl キーを押しながら F5 キーを押すと、コンテナーを再構築しなくても、アプリケーションを編集して更新できます。 これは、Linux または Windows の Docker コンテナーを作成する Windows 開発者にとって最も簡単で最も強力な選択肢です。

### <a name="visual-studio-for-mac-mac-development-machine"></a>Visual Studio for Mac (Mac の開発用コンピューター)

Docker ベースのアプリケーションを開発するときに、[Visual Studio for Mac](https://visualstudio.microsoft.com/vs/mac/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link) を使用できます。 Visual Studio for Mac は、Visual Studio Code for Mac と比較した場合、より豊富な IDE を備えています。

## <a name="language-and-framework-choices"></a>言語とフレームワークの選択肢

最新の言語で Microsoft のツールを使用して Docker アプリケーションを開発できます。 次が初期一覧ですが、これに限定されているわけではありません。

- .NET Core および ASP.NET Core
- Node.js
- 移動
- Java
- Ruby
- Python

基本的に、Linux または Windows で Docker によってサポートされている任意の最新の言語を使用できます。

>[!div class="step-by-step"]
>[前へ](deploy-azure-kubernetes-service.md)
>[次へ](docker-apps-inner-loop-workflow.md)
