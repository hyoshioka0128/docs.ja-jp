---
title: Docker アプリの内部ループ開発ワークフロー
description: Docker アプリケーションの開発の "内部ループ" ワークフローについて説明します。
ms.date: 02/15/2019
ms.openlocfilehash: 04e1b29e6a0cef89df05cc9124806c74a38b5249
ms.sourcegitcommit: 56f1d1203d0075a461a10a301459d3aa452f4f47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/24/2019
ms.locfileid: "71214360"
---
# <a name="inner-loop-development-workflow-for-docker-apps"></a>Docker アプリの内部ループ開発ワークフロー

DevOps サイクル全体にまたがる外部ループ ワークフローをトリガーする前に、各内部ループが各開発者のコンピューターで開始され、アプリ自体をコード化し、希望する言語またはプラットフォームを使用し、ローカルでテストされます (図 4-21)。 ただし、すべての場合において、選択する言語、フレームワーク、プラットフォームに関係なく、共通する重要な点が 1 つあります。 この特定のワークフローでは、常に Docker コンテナーを開発し、テストしますが、ローカルで行われます。

![手順 1 - コード/実行/デバッグ](./media/image18.png)

**図 4-21** 内部ループの開発コンテキスト

Docker イメージのコンテナーまたはインスタンスには、以下のコンポーネントが含まれます。

- 選択したオペレーティング システム (Linux ディストリビューションや Windows など)

- 開発者が追加したファイル (アプリのバイナリなど)

- 構成 (環境の設定や依存関係など)

- Docker でどのプロセスを実行するかに関する指示

Docker をプロセスとして活用する内部ループ開発ワークフローを設定できます (詳細は次のセクションにあります)。 環境設定の初回手順は含まれていません。それは一度だけ実行すれば良いからです。

## <a name="building-a-single-app-within-a-docker-container-using-visual-studio-code-and-docker-cli"></a>Visual Studio Code と Docker CLI を使用し、Docker コンテナー内で 1 つのアプリをビルドする

アプリは自分のサービスと追加のライブラリ (依存関係) から構成されます。

図 4-22 では、Docker アプリをビルドするときに通常行う基本手順と各手順の詳細を確認できます。

![ワークフローの概要:手順 1 - コード、手順 2 - Dockerfile を記述する、手順 3 - Dockerfile で定義されたイメージを作成する、手順 4 - docker-compose ファイルでサービスを定義する、手順 5 - コンテナーまたは作られたアプリを実行する、手順 6 - アプリをテストする、手順 7 - プッシュして外部ループを開始する (CI/CD パイプライン) か、開発を続ける](./media/image19.png)

**図 4-22** Docker CLI を利用し、Docker でコンテナー化されたアプリケーションのワークフローの概要

### <a name="step-1-start-coding-in-visual-studio-code-and-create-your-initial-appservice-baseline"></a>手順 1: Visual Studio Code でコーディングを開始し、初回アプリ/サービス ベースラインを作成する

アプリケーションの開発方法は、Docker を使用しない場合と同じです。 違いは、開発中、ローカル環境 (Linux VM や Windows など) に配置されている Docker コンテナー内で実行されているアプリケーションやサービスを展開し、テストするということです。

**ローカル環境を設定する**

Mac または Windows 向けの最新版 Docker を使用すると、Docker アプリケーションをもっと簡単に開発できます。設定も簡単です。

> [!TIP]
> Docker for Windows の設定方法については、<https://docs.docker.com/docker-for-windows/> にお進みください。
>
>Docker for Mac の設定方法については、<https://docs.docker.com/docker-for-mac/> にお進みください。

また、Docker CLI の使用時、実際にアプリケーションを開発できるよう、コード エディターが必要です。

Microsoft からは Visual Studio Code が提供されます。これは Mac、Windows、Linux でサポートされている軽量のコード エディターであり、IntelliSense、[さまざまな言語のサポート](https://code.visualstudio.com/docs/languages/overview) (JavaScript、.NET、Go、Java、Ruby、Python、ほとんどの新しい言語)、[デバッグ](https://code.visualstudio.com/Docs/editor/debugging)、[Git との統合](https://code.visualstudio.com/Docs/editor/versioncontrol)、[拡張機能サポート](https://code.visualstudio.com/docs/extensions/overview)を提供します。 このエディターは、Mac および Linux の開発者に最適です。 Windows でも、完全な Visual Studio アプリケーションを使用できます。

> [!TIP]
> Windows、Mac、Linux 向けの Visual Studio Code をインストールする方法については、<https://code.visualstudio.com/docs/setup/setup-overview/> にお進みください。
>
> Docker for Mac の設定方法については、<https://docs.docker.com/docker-for-mac/> にお進みください。

Docker CLI を使用して、あらゆるコード エディターでコードを記述できますが、Docker 拡張機能と共に Visual Studio Code を使用すると、ワークスペースで `Dockerfile` ファイルや `docker-compose.yml` ファイルを簡単に作成できます。 Visual Studio Code IDE からタスクやスクリプトを実行し、下部の Docker CLI を使用して Docker コマンドを実行することもできます。

VS Code 用 Docker 拡張機能からは次の機能が提供されます。

- `Dockerfile` および `docker-compose.yml` ファイルの自動生成

- `docker-compose.yml` および `Dockerfile` ファイルの構文強調表示とツールチップ

- `Dockerfile` および `docker-compose.yml` ファイルの IntelliSense (入力候補)

- `Dockerfile` ファイルの Lint 処理 (エラーと警告)

- 最も一般的な Docker コマンドのコマンド パレット (F1) 統合

- イメージとコンテナーを管理するためのエクスプローラー統合

- DockerHub と Azure Container Registry から Azure App Service へのイメージのデプロイ

Docker 拡張機能をインストールするには、Ctrl + Shift + P キーを押しながら、「`ext install`」と入力し、Install Extension コマンドを実行して Marketplace 拡張機能一覧を表示します。 次に、図 4-23 のように、「**docker**」と入力して結果にフィルターを適用し、Docker Support 拡張機能を選択します。

![VS Code 用 Docker 拡張機能の表示。](./media/image20.png)

**図 4-23**. Visual Studio Code で Docker 拡張機能をインストールする

### <a name="step-2-create-a-dockerfile-related-to-an-existing-image-plain-os-or-dev-environments-like-net-core-nodejs-and-ruby"></a>手順 2: 既存のイメージ (プレーンな OS か、.NET Core、Node.js、Ruby などの開発環境) に関連する DockerFile を作成する

ビルドするカスタム イメージごとと、展開するコンテナーごとに `DockerFile` が必要になります。 アプリが 1 つのカスタム サービスで構成される場合、`DockerFile` が 1 つ必要になります。 ただし、(マイクロサービス アーキテクチャの場合のように) アプリが複数のサービスで構成される場合、サービスごとに `Dockerfile` が 1 つ必要になります。

`DockerFile` は通常、アプリまたはサービスのルート フォルダーに配置され、そのアプリまたはサービスを設定し、実行する方法を Docker に認識させるための必須のコマンドが含まれています。 `DockerFile` を作成し、コード (node.js や .NET Core など) とともにプロジェクトに追加できます。この環境が初めての場合、次のヒントをご覧ください。

> [!TIP]
> Docker コンテナーに関連する `Dockerfile` および `docker-compose.yml` ファイルを使用するとき、Docker 拡張機能を利用してガイドを表示することができます。 最終的には、このツールなしでこの種類のファイルを記述することになるでしょうが、Docker 拡張機能の使用は学習曲線を加速するので、開始点として推奨されます。

図 4-24 では、VS Code 用 Docker 拡張機能で docker-compose ファイルが追加される様子を確認できます。

![VS Code 用 Docker 拡張機能のコンソール表示。](./media/image24.png)

**図 4-24** **Add Docker files to Workspace コマンド**で追加された Docker ファイル

DockerFile を追加するとき、(`FROM mcr.microsoft.com/dotnet/core/aspnet` を使用するなどして) 使用する基本の Docker イメージを指定します。 通常、[Docker Hub レジストリ](https://hub.docker.com/)にある公式リポジトリから得られる基本イメージ ([.NET Core 用のイメージ](https://hub.docker.com/_/microsoft-dotnet-core/)や [Node.js 用のイメージ](https://hub.docker.com/_/node/)など) を基礎にしてカスタム イメージをビルドします。

***既存の公式 Docker イメージを使用する***

バージョン番号を持つ言語スタックの公式イメージ リポジトリを使うと、同じ言語機能が (開発、テスト、運用環境など) すべてのコンピューターで使用できるようになります。

次は .NET Core コンテナー向けサンプル DockerFile です。

```Dockerfile
# Base Docker image to use  
FROM mcr.microsoft.com/dotnet/core/aspnet:2.2
  
# Set the Working Directory and files to be copied to the image  
ARG source  
WORKDIR /app  
COPY ${source:-bin/Release/PublishOutput} .  
  
# Configure the listening port to 80 (Internal/Secured port within Docker host)  
EXPOSE 80  
  
# Application entry point  
ENTRYPOINT ["dotnet", "MyCustomMicroservice.dll"]
```

この場合、イメージは、`FROM mcr.microsoft.com/dotnet/core/aspnet:2.2` の行から、公式の ASP.NET Core Docker イメージ (Linux および Windows 用マルチアーキテクチャ) のバージョン 2.2 に基づいています。 (このトピックの詳細については、[ASP.NET Core Docker イメージ](https://hub.docker.com/_/microsoft-dotnet-core-aspnet/)に関するページと [.NET Core Docker イメージ](https://hub.docker.com/_/microsoft-dotnet-core/)に関するページを参照してください)。

DockerFile では、実行時に使用する TCP ポートをリッスンするように Docker に指示することもできます (ポート 80 など)。

使用している言語とフレームワークによっては、Dockerfile に別の構成設定を指定できます。 たとえば、`["dotnet", "MySingleContainerWebApp.dll"]` を含む `ENTRYPOINT` 行では、.NET Core アプリケーションを実行するように Docker に指示します。 SDK と .NET Core CLI (`dotnet CLI`) を使用して .NET アプリケーションをビルドし、実行する場合、この設定は異なるものになります。 ここで重要なことは、ENTRYPOINT 行とその他の設定はアプリケーションに選択した言語とプラットフォームに依存するということです。

> [!TIP]
> .NET Core アプリケーション向け Docker イメージのビルド方法については、<https://docs.microsoft.com/dotnet/core/docker/building-net-docker-images> にお進みください。
>
> 独自のイメージをビルドする方法については、<https://docs.docker.com/engine/tutorials/dockerimages/> にお進みください。

**マルチアーキテクチャ イメージ リポジトリを使用する**

リポジトリの単一のイメージ名には、Linux イメージや Windows イメージなどのプラットフォーム バリアントを含めることができます。 この機能では、Microsoft (基本イメージの作成者) などのベンダーが、複数のプラットフォーム (つまり、Linux および Windows) に対応できるリポジトリを 1 つ作成できます。 たとえば、Docker Hub レジストリにある [dotnet/core/aspnet](https://hub.docker.com/_/microsoft-dotnet-core-aspnet/) リポジトリでは、同じイメージ名を使用して Linux および Windows Nano Server をサポートしています。

Windows ホストから [dotnet/core/aspnet](https://hub.docker.com/_/microsoft-dotnet-core-aspnet/) イメージをプルした場合、Windows バリアントがプルされ、同じイメージ名が Linux ホストからプルされた場合、Linux バリアントがプルされます。

***基本イメージを一から作成する***

Docker の[この記事](https://docs.docker.com/engine/userguide/eng-image/baseimages/)で説明されているように、独自の Docker 基本イメージを一から作成できます。 Docker を初めて使用するユーザーにはおそらく推奨されませんが、独自の基本イメージを設定するならそれは可能です。

### <a name="step-3-create-your-custom-docker-images-embedding-your-service-in-it"></a>手順 3: カスタム Docker イメージを作成し、それにサービスを埋め込む

アプリを構成するカスタム サービスごとに、関連イメージを作成する必要があります。 アプリが 1 つのサービスまたは Web アプリで構成されている場合、イメージは 1 つのみ必要です。

> [!NOTE]
> "外部ループ DevOps ワークフロー" を考慮すると、イメージがソース コードからそのグローバル環境で作成されるよう、ソース コードを Git リポジトリにプッシュするたびに (継続的インテグレーション)、自動化されたビルド プロセスによってイメージが作成されます。
>
> ただし、その外部ループ ルートに進むことを検討する前に、正しく動作しないコードがソース コントロール システム (Git など) にプッシュされることがないよう、Docker アプリケーションが実際に正しく動作することを確認する必要があります。
>
> そのため、各開発者はまず、内部ループ プロセス全体を行ってローカル テストし、それから、完全な機能または変更をソース コントロール システムにプッシュするまで開発を続けます。

DockerFile を使用し、ローカル環境でイメージを作成するには、図 4-25 にあるように、docker build コマンドを使用できます (いくつかのコンテナー/サービスで構成されるアプリケーションに `docker-compose up --build` を実行することもできます)。

![docker-compose ビルドのコンソール出力。ダウンロード進捗状況を確認できます。](./media/image25.png)

**図 4-25** docker build の実行

任意で、プロジェクト フォルダーから `docker build` を直接実行する代わりに、`dotnet publish` 実行コマンドを使用し、それから `docker build` を実行することで、まず、必要な .NET ライブラリで展開可能なフォルダーを生成できます。

この例では、`cesardl/netcore-webapi-microservice-docker:first` という名前で Docker イメージが作成されます (`:first` は特定のバージョンのようなタグです)。 いくつかのコンテナーで作成した Docker アプリケーション用に作成する必要のあるカスタム イメージごとにこの手順を行うことができます。

図 4-26 にあるように、docker images コマンドを使用し、ローカル リポジトリ (開発コンピューター) の既存のイメージを検索できます。

![コマンド docker イメージからのコンソール出力。既存のイメージを確認できます。](./media/image26.png)

**図 4-26** docker images を使用した既存のイメージの表示

### <a name="step-4-define-your-services-in-docker-composeyml-when-building-a-composed-docker-app-with-multiple-services"></a>手順 4: 複数のサービスで Docker アプリケーションを構築するときに docker-compose.yml でサービスを定義する

`docker-compose.yml` ファイルを利用すると、次のセクションで説明するように、展開コマンドで構成済みアプリケーションとして展開する一連の関連サービスを定義できます。

メインまたはルート ソリューション フォルダーでそのファイルを作成します。この `docker-compose.yml` ファイルで確認できるものと同様のコンテンツが含まれているはずです。

```yml
version: '3.4'
services:
  web:
    build: .
    ports:
     - "81:80"
    volumes:
     - .:/code
    depends_on:
     - redis
  redis:
    image: redis
```

この特定のケースでは、このファイルにより、Web サービス (カスタム サービス) と redis サービス (人気のキャッシュ サービス) という 2 つのサービスが定義されます。 各サービスはコンテナーとして展開されます。そのため、それぞれに具体的な Docker イメージを使用する必要があります。 この特定の Web サービスの場合、イメージでは次を行う必要があります。

- 現在のディレクトリで DockerFile からビルドする

- コンテナー上の公開されているポート 80 をホスト コンピューター上の外部ポート 81 に転送する

- コンテナー内の /code にホストのプロジェクト ディレクトリをマウントする (イメージを再ビルドしなくてもコードを変更できるようになります)

- Web サービスと redis サービスをリンクする

redis サービスでは、Docker Hub レジストリからプルされた[最新のパブリック redis イメージ](https://hub.docker.com/_/redis/)が使用されます。 [redis](https://redis.io/) はサーバー側アプリケーションとして人気のキャッシュ システムです。

### <a name="step-5-build-and-run-your-docker-app"></a>手順 5: Docker アプリをビルドし、実行する

アプリにコンテナーが 1 つしかない場合、必要な作業は Docker ホスト (VM または物理サーバー) にそれを展開して実行することだけになります。 ただし、アプリが複数のサービスで構成されている場合、*それを作成する*必要もあります。 別のオプションを見てみましょう。

***オプション A: 1 つのコンテナーまたはサービスを実行する***

次に示すように docker run コマンドを使用し、Docker イメージを実行できます。

```console
docker run -t -d -p 80:5000 cesardl/netcore-webapi-microservice-docker:first
```

この特定の展開の場合、ポート 80 に送信された要求を内部ポート 5000 にリダイレクトします。 これでアプリケーションは、ホスト レベルで外部ポート 80 をリッスンします。

***オプション B: 複数コンテナー アプリケーションを作成し、実行する***

ほとんどの企業のシナリオでは、Docker アプリケーションは複数のサービスから構成されます。 そのとき、`docker-compose up` コマンドを実行できますが (図 4-27)、このコマンドでは、前に作成した docker-compose.yml ファイルが使用されます。 このコマンドを実行すると、作成されたアプリケーションがそのすべての関連コンテナーと共に展開されます。

![docker-compose up コマンドからのコンソール出力。](./media/image27.png)

**図 4-27** "docker-compose up" コマンドの実行結果

VM を表現する図 4-28 で示すように、`docker-compose up` の実行後、Docker ホストにアプリケーションとその関連コンテナーを展開します。

![マルチコンテナー アプリケーションを実行する VM](./media/image28.png)

**図 4-28** Docker コンテナーが展開された VM

### <a name="step-6-test-your-docker-application-locally-in-your-local-cd-vm"></a>手順 6: Docker アプリケーションをローカル テストする (ローカル、CD VM で)

この手順は、アプリで何が実行されているかによって異なります。

1 つのコンテナーまたはサービスとして展開される単純な .NET Core Web API "Hello World" の場合、DockerFile に指定されている TCP ポートを指定し、サービスにアクセスするだけです。

localhost がオンになっていない場合、サービスに移動し、次のコマンドを使用してコンピューターの IP アドレスを見つけます。

```console
docker-machine {IP} {YOUR-CONTAINER-NAME}
```

Docker ホストでブラウザーを開き、そのサイトに移動します。図 4-29 に示すように、アプリ/サービスが実行中であることを確認できるはずです。

![ブラウザーに表示される localhost/API/values からの応答](./media/image29.png)

**図 4-29** localhost を使用し、Docker アプリケーションをローカル テストする

ポート 80 を使用していますが、内部ではポート 5000 にリダイレクトされていることにご注意ください。これは、前に説明したように、`docker run` でこのように展開されたためです。

ターミナルから CURL を使用することでこれをテストできます。 Windows への Docker インストールの場合、図 4-30 に示すように、既定の IP は 10.0.75.1 です。

![CURL で http://10.0.75.1/API/values を取得したときのコンソール出力](./media/image30.png)

**図 4-30** CURL を使用した Docker アプリケーションのローカル テスト

**Docker で実行されているコンテナーをデバッグする**

Visual Studio Code では、Node.js かその他のプラットフォーム (.NET Core コンテナーなど) を使用している場合、Docker をデバッグできます。

次のセクションで説明するように、Windows または Mac 向けの Visual Studio の使用時、Docker で .NET Core または .NET Framework コンテナーをデバッグすることもできます。

> [!情報]
>
> Node.js Docker コンテナーのデバッグに関する詳細については、<https://blog.docker.com/2016/07/live-debugging-docker/> と <https://blogs.msdn.microsoft.com/user_ed/2016/02/27/visual-studio-code-new-features-13-big-debugging-updates-rich-object-hover-conditional-breakpoints-node-js-mono-more/> にお進みください。

>[!div class="step-by-step"]
>[前へ](docker-apps-development-environment.md)
>[次へ](visual-studio-tools-for-docker.md)
