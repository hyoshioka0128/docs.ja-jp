---
title: Docker を使用してアプリをコンテナー化するチュートリアル
description: このチュートリアルでは、Docker を使って .NET Core アプリケーションをコンテナー化する方法を学習します。
ms.date: 04/27/2020
ms.topic: tutorial
ms.custom: mvc
ms.openlocfilehash: c5e6648539af45f3ce615bfc183e6f95a62b085a
ms.sourcegitcommit: 5988e9a29cedb8757320817deda3c08c6f44a6aa
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2020
ms.locfileid: "82200029"
---
# <a name="tutorial-containerize-a-net-core-app"></a>チュートリアル: NET Core アプリのコンテナー化

このチュートリアルでは、Docker を使って .NET Core アプリケーションをコンテナー化する方法を学習します。 コンテナーには、変更できないインフラストラクチャになったり、移植可能なアーキテクチャを提供したり、スケーラビリティを可能にしたりといった、さまざまな特徴とベネフィットがあります。 そのイメージを使って、ローカル開発環境、プライベート クラウド、またはパブリック クラウド用にコンテナーを作成することができます。

このチュートリアルでは、次の作業を行いました。

> [!div class="checklist"]
>
> - 簡単な .NET Core アプリを作成して発行する
> - .NET Core 用の Dockerfile を作成して構成する
> - Docker イメージの構築
> - Docker コンテナーを作成して実行する

.NET Core アプリケーション用に Docker コンテナーを構築してデプロイするタスクを理解できます。 "*Docker プラットフォーム*" では、"*Docker エンジン*" を使用して、すばやくアプリがビルドされ、"*Docker イメージ*" としてパッケージ化されます。 これらのイメージは、階層型コンテナーに展開されて実行される *Dockerfile* 形式で記述されています。

> [!NOTE]
> このチュートリアルは ASP.NET Core アプリ向けのものでは**ありません**。 ASP.NET Core を使用している場合は、[ASP.NET Core アプリケーションをコンテナー化する方法](/aspnet/core/host-and-deploy/docker/building-net-docker-images)に関するチュートリアルを参照してください。

## <a name="prerequisites"></a>必須コンポーネント

次の前提条件をインストールします。

- [.NET Core 3.1 SDK](https://dotnet.microsoft.com/download)\
.NET Core をインストールしてある場合、どの SDK を使っているか確認するには、`dotnet --info` コマンドを使います。
- [Docker Community Edition](https://www.docker.com/products/docker-desktop)
- *Dockerfile* と .NET Core サンプル アプリ用の一時作業フォルダー。 このチュートリアルでは、作業フォルダーに *docker-working* の名前が使用されます。

## <a name="create-net-core-app"></a>.NET Core アプリを作成する

Docker コンテナーで実行される .NET Core アプリが必要です。 ターミナルを開き、作業フォルダーがまだない場合は作成して、移動します。 作業フォルダーで次のコマンドを実行し、*app* という名前のサブディレクトリに新しいプロジェクトを作成します。

```dotnetcli
dotnet new console -o App -n NetCore.Docker
```

フォルダー ツリーは次のように表示されます。

```
docker-working
    └──App
        ├──NetCore.Docker.csproj
        ├──Program.cs
        └──obj
            ├──NetCore.Docker.csproj.nuget.dgspec.json
            ├──NetCore.Docker.csproj.nuget.g.props
            ├──NetCore.Docker.csproj.nuget.g.targets
            ├──project.assets.json
            └──project.nuget.cache
```

`dotnet new` コマンドでは、"*App*" という名前の新しいフォルダーが作成され、"Hello World" コンソール アプリケーションが生成されます。 ディレクトリを変更し、ターミナル セッションから "*App*" フォルダーに移動します。 `dotnet run` コマンドを使用してアプリを起動します。 アプリケーションが実行され、コマンドの下に `Hello World!` が出力されます。

```dotnetcli
dotnet run
Hello World!
```

既定のテンプレートでは、ターミナルに出力した後、すぐに終了するアプリが作成されます。 このチュートリアルでは、無限にループするアプリを使います。 テキスト エディターで *Program.cs* ファイルを開きます。

> [!TIP]
> Visual Studio Code を使用している場合は、前のターミナル セッションで次のコマンドを入力します。
>
> ```
> code .
> ```
>
> これにより、Visual Studio Code のプロジェクトを含む "*App*" フォルダーが開きます。

"*Program.cs*" は次のような C# コードになります。

```csharp
using System;

namespace NetCore.Docker
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("Hello World!");
        }
    }
}
```

1 秒ごとに数をカウントする次のコードにファイルを置き換えます。

```csharp
using System;
using System.Threading.Tasks;

namespace NetCore.Docker
{
    class Program
    {
        static async Task Main(string[] args)
        {
            var counter = 0;
            var max = args.Length != 0 ? Convert.ToInt32(args[0]) : -1;
            while (max == -1 || counter < max)
            {
                Console.WriteLine($"Counter: {++counter}");
                await Task.Delay(1000);
            }
        }
    }
}
```

ファイルを保存し、`dotnet run` で再びプログラムをテストします。 このアプリは無限に実行されることに注意してください。 停止するにはキャンセル コマンド <kbd>Ctrl + C</kbd> を使用します。 次に出力例を示します。

```dotnetcli
dotnet run
Counter: 1
Counter: 2
Counter: 3
Counter: 4
^C
```

コマンド ラインでアプリに数値を渡すと、アプリはその値までカウント アップしただけで終了します。 `dotnet run -- 5` で 5 までカウントしてみてください。

> [!IMPORTANT]
> `--` より後のパラメーターは `dotnet run` コマンドに渡されず、代わりにアプリケーションに渡されます。

## <a name="publish-net-core-app"></a>.NET Core アプリを発行する

.NET Core アプリを Docker イメージに追加するには、まず発行する必要があります。 アプリの発行済みバージョンをコンテナーで実行することをお勧めします。 アプリを発行するには、次のコマンドを実行します。

```dotnetcli
dotnet publish -c Release
```

このコマンドでは、*publish* フォルダーにアプリがコンパイルされます。 作業フォルダーから *publish* フォルダーへのパスは `.\App\bin\Release\netcoreapp3.1\publish\` です

#### <a name="windows"></a>[Windows](#tab/windows)

"*App*" フォルダーから、publish フォルダーのディレクトリ一覧を表示し、"*NetCore.Docker.dll*" ファイルが作成されたことを確認します。

```powershell
dir .\bin\Release\netcoreapp3.1\publish\

    Directory: C:\Users\dapine\App\bin\Release\netcoreapp3.1\publish

Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----        4/27/2020   8:27 AM            434 NetCore.Docker.deps.json
-a----        4/27/2020   8:27 AM           6144 NetCore.Docker.dll
-a----        4/27/2020   8:27 AM         171520 NetCore.Docker.exe
-a----        4/27/2020   8:27 AM            860 NetCore.Docker.pdb
-a----        4/27/2020   8:27 AM            154 NetCore.Docker.runtimeconfig.json
```

#### <a name="linux"></a>[Linux](#tab/linux)

`ls` コマンドを使用してディレクトリ一覧を表示し、"*NetCore.Docker.dll*" ファイルが作成されたことを確認します。

```bash
me@DESKTOP:/docker-working/app$ ls bin/Release/netcoreapp3.1/publish
NetCore.Docker.deps.json  NetCore.Docker.dll  NetCore.Docker.pdb  NetCore.Docker.runtimeconfig.json
```

---

## <a name="create-the-dockerfile"></a>Dockerfile を作成する

*Dockerfile* ファイルは、コンテナー イメージを作成するために `docker build` コマンドによって使用されます。 このファイルは *Dockerfile* という名前のテキスト ファイルで、拡張子はありません。

" *.csproj*" が含まれるディレクトリに "*Dockerfile*" という名前のファイルを作成し、テキスト エディターで開きます。 このチュートリアルでは、(.NET Core ランタイム イメージを含む) ASP.NET Core ランタイム イメージを使用して、.NET Core コンソール アプリケーションに対応します。

```dockerfile
FROM mcr.microsoft.com/dotnet/core/aspnet:3.1
```

> [!NOTE]
> `mcr.microsoft.com/dotnet/core/runtime:3.1` イメージが使用されている可能性もありますが、ここでは ASP.NET Core ランタイム イメージを意図的に使用します。

`FROM` キーワードには、完全修飾 Docker コンテナー イメージ名が必要です。 Microsoft Container Registry (MCR、mcr.microsoft.com) は、パブリック アクセスが可能なコンテナーをホストする Docker Hub のシンジケートです。 `dotnet/core` セグメントはコンテナー リポジトリで、`aspnet` セグメントはコンテナー イメージの名前です。 イメージには `3.1` のタグが付けられ、バージョン管理に使用されます。 このため、`mcr.microsoft.com/dotnet/core/aspnet:3.1` は .NET Core 3.1 ランタイムです。 必ず、SDK のターゲットのランタイムと一致するランタイム バージョンをプルしてください。 たとえば、前のセクションで作成したアプリは .NET Core 3.1 SDK を使用しているため、*Dockerfile* で参照される基本イメージは **3.1** でタグ付けされます。

*Dockerfile* ファイルを保存します。 作業フォルダーのディレクトリ構造は次のようになります。 一部のより深いレベルのファイルとフォルダーは、スペース削減のためこの記事では省略されています。

```
docker-working
    └──App
        ├──Dockerfile
        ├──NetCore.Docker.csproj
        ├──Program.cs
        ├──bin
        │   └──Release
        │       └──netcoreapp3.1
        │           └──publish
        │               ├──NetCore.Docker.deps.json
        │               ├──NetCore.Docker.exe
        │               ├──NetCore.Docker.dll
        │               ├──NetCore.Docker.pdb
        │               └──NetCore.Docker.runtimeconfig.json
        └──obj
            └──...
```

ターミナルから、次のコマンドを実行します。

```Docker
docker build -t counter-image -f Dockerfile .
```

Docker により *Dockerfile* 内の各行が処理されます。 `docker build` コマンドの `.` は、現在のフォルダーで *Dockerfile* を検索するよう Docker に指示します。 このコマンドでは、イメージがビルドされて、そのイメージを指す **counter-image** という名前のローカル リポジトリが作成されます。 このコマンドが終了したら、`docker images` を実行し、インストールされているイメージの一覧を表示します。

```Docker
docker images
REPOSITORY                              TAG                 IMAGE ID            CREATED             SIZE
counter-image                           latest              e6780479db63        4 days ago          190MB
mcr.microsoft.com/dotnet/core/aspnet    3.1                 e6780479db63        4 days ago          190MB
```

2 つのイメージで同じ **IMAGE ID** 値が共有されていることに注意してください。 *Dockerfile* での唯一のコマンドが既存のイメージを新しいイメージの基にするものであったため、両方のイメージで値が同じになっています。 3 つのコマンドを "*Dockerfile*" に追加してみましょう。 各コマンドでは、**counter-image** リポジトリ エントリが指し示すイメージを表す最後のコマンドで新しいイメージ レイヤーが作成されます。

```dockerfile
COPY bin/Release/netcoreapp3.1/publish/ App/
WORKDIR /App
ENTRYPOINT ["dotnet", "NetCore.Docker.dll"]
```

`COPY` コマンドは、自分のコンピューターの指定したフォルダーをコンテナー内のフォルダーにコピーするよう Docker に指示します。 この例では、"*publish*" フォルダーが、コンテナーの "*App*" という名前のフォルダーにコピーされます。

`WORKDIR` コマンドでは、コンテナー内の**現在のディレクトリ**が、"*App*" に変更されます。

次のコマンド `ENTRYPOINT` は、実行可能ファイルとして実行するためにコンテナーを構成するよう Docker に指示します。 コンテナーの起動時に、`ENTRYPOINT` コマンドが実行されます。 このコマンドが終了すると、コンテナーは自動的に停止します。

ターミナルから `docker build -t counter-image -f Dockerfile .` を実行し、そのコマンドが終了したら `docker images` を実行します。

```Docker
docker build -t counter-image -f Dockerfile .
Sending build context to Docker daemon  1.117MB
Step 1/4 : FROM mcr.microsoft.com/dotnet/core/aspnet:3.1
 ---> e6780479db63
Step 2/4 : COPY bin/Release/netcoreapp3.1/publish/ App/
 ---> d1732740eed2
Step 3/4 : WORKDIR /App
 ---> Running in b1701a42f3ff
Removing intermediate container b1701a42f3ff
 ---> 919aab5b95e3
Step 4/4 : ENTRYPOINT ["dotnet", "NetCore.Docker.dll"]
 ---> Running in c12aebd26ced
Removing intermediate container c12aebd26ced
 ---> cd11c3df9b19
Successfully built cd11c3df9b19
Successfully tagged counter-image:latest

docker images
REPOSITORY                              TAG                 IMAGE ID            CREATED             SIZE
counter-image                           latest              cd11c3df9b19        41 seconds ago      190MB
mcr.microsoft.com/dotnet/core/aspnet    3.1                 e6780479db63        4 days ago          190MB
```

*Dockerfile* 内の各コマンドによってレイヤーが生成され、**IMAGE ID** が作成されます。 最後の **IMAGE ID** は **cd11c3df9b19** であり (個々に異なります)、次にこのイメージを基にしてコンテナーを作成します。

## <a name="create-a-container"></a>コンテナーの作成

アプリを含むイメージができたので、コンテナーを作成することができます。 2 つの方法でコンテナーを作成することができます。 最初に、停止している新しいコンテナーを作成します。

```Docker
docker create --name core-counter counter-image
0f281cb3af994fba5d962cc7d482828484ea14ead6bfe386a35e5088c0058851
```

上の `docker create` コマンドでは、**counter-image** イメージに基づくコンテナーが作成されます。 そのコマンドの出力では、作成されたコンテナーの **CONTAINER ID** (個々に異なります) が示されます。 "*すべて*" のコンテナーの一覧を表示するには、`docker ps -a` コマンドを使います。

```Docker
docker ps -a
CONTAINER ID    IMAGE            COMMAND                   CREATED           STATUS     PORTS    NAMES
0f281cb3af99    counter-image    "dotnet NetCore.Dock…"    40 seconds ago    Created             core-counter
```

### <a name="manage-the-container"></a>コンテナーを管理する

コンテナーが特定の名前 `core-counter` で作成されました。この名前を使用してコンテナーを管理します。 次の例では、`docker start` コマンドを使ってコンテナーを起動した後、`docker ps` コマンドを使って、実行されているコンテナーのみを表示します。

```Docker
docker start core-counter
core-counter

docker ps
CONTAINER ID    IMAGE            COMMAND                   CREATED          STATUS          PORTS    NAMES
2f6424a7ddce    counter-image    "dotnet NetCore.Dock…"    2 minutes ago    Up 11 seconds            core-counter
```

同様に、`docker stop` コマンドではコンテナーが停止されます。 次の例では、`docker stop` コマンドを使ってコンテナーを停止した後、`docker ps` コマンドを使って、実行されているコンテナーがないことを示します。

```Docker
docker stop core-counter
core-counter

docker ps
CONTAINER ID    IMAGE    COMMAND    CREATED    STATUS    PORTS    NAMES
```

### <a name="connect-to-a-container"></a>コンテナーへの接続

コンテナーが実行状態になった後、それに接続して出力を確認できます。 `docker start` コマンドを使ってコンテナーを起動し、`docker attach` コマンドを使って出力ストリームを表示します。 この例では、<kbd>Ctrl+C</kbd> キー入力を使用して、実行中のコンテナーからデタッチします。 このキー入力では、コンテナーを停止するように指定されている場合を除き、コンテナー内のプロセスが終了します。 `--sig-proxy=false` パラメーターを指定すると、<kbd>Ctrl+C</kbd> キーを押してもコンテナー内のプロセスが停止しないことが保証されます。

コンテナーからデタッチした後、再アタッチして、まだ実行されていてカウントが行われていることを確認します。

```Docker
docker start core-counter
core-counter

docker attach --sig-proxy=false core-counter
Counter: 7
Counter: 8
Counter: 9
^C

docker attach --sig-proxy=false core-counter
Counter: 17
Counter: 18
Counter: 19
^C
```

### <a name="delete-a-container"></a>コンテナーを削除する

この記事の目的では、何も行っていないコンテナーをそのままにするのは望ましくありません。 前に作成したコンテナーを削除します。 コンテナーが実行されている場合は、それを停止します。

```Docker
docker stop core-counter
```

次の例では、すべてのコンテナーを一覧表示します。 次に、`docker rm` コマンドを使ってコンテナーを削除した後、もう一度実行中のコンテナーを確認します。

```Docker
docker ps -a
CONTAINER ID    IMAGE            COMMAND                   CREATED          STATUS                        PORTS    NAMES
2f6424a7ddce    counter-image    "dotnet NetCore.Dock…"    7 minutes ago    Exited (143) 20 seconds ago            core-counter

docker rm core-counter
core-counter

docker ps -a
CONTAINER ID    IMAGE    COMMAND    CREATED    STATUS    PORTS    NAMES
```

### <a name="single-run"></a>単一実行

Docker では、1 つのコマンドとしてコンテナーを作成して実行するための `docker run` コマンドが提供されています。 このコマンドでは、`docker create` を実行してから `docker start` を実行する必要がありません。 コンテナーが停止したら自動的にコンテナーを削除するように、このコマンドを設定することもできます。 たとえば、`docker run -it --rm` を使うと 2 つのことが行われます。つまり、最初に現在のターミナルを使ってコンテナーに自動的に接続し、次にコンテナーが終了したらそれを削除します。

```Docker
docker run -it --rm counter-image
Counter: 1
Counter: 2
Counter: 3
Counter: 4
Counter: 5
^C
```

また、コンテナーは .NET Core アプリの実行にパラメーターを渡します。 .NET Core アプリに対して 3 つまでしかカウントしないように指示するには、3 を渡します。

```Docker
docker run -it --rm counter-image 3
Counter: 1
Counter: 2
Counter: 3
```

`docker run -it` では、<kbd>Ctrl+C</kbd> キーを押すと、コンテナーで実行されているプロセスが停止し、さらにコンテナーが停止されます。 `--rm` パラメーターを指定したので、プロセスが停止するとコンテナーは自動的に削除されます。 それが存在しないことを確認します。

```Docker
docker ps -a
CONTAINER ID    IMAGE    COMMAND    CREATED    STATUS    PORTS    NAMES
```

### <a name="change-the-entrypoint"></a>ENTRYPOINT を変更する

`docker run` コマンドでは、*Dockerfile* から `ENTRYPOINT` コマンドを変更し、そのコンテナーに対してのみ何か他のことを実行することもできます。 たとえば、次のコマンドを使うと `bash` または `cmd.exe` を実行できます。 必要に応じて、コマンドを編集します。

#### <a name="windows"></a>[Windows](#tab/windows)

この例では、`ENTRYPOINT` が `cmd.exe` に変更されています。 プロセスを終了してコンテナーを停止するには、<kbd>Ctrl+C</kbd> キーを押します。

```Docker
docker run -it --rm --entrypoint "cmd.exe" counter-image

Microsoft Windows [Version 10.0.17763.379]
(c) 2018 Microsoft Corporation. All rights reserved.

C:\>dir
 Volume in drive C has no label.
 Volume Serial Number is 3005-1E84

 Directory of C:\

04/09/2019  08:46 AM    <DIR>          app
03/07/2019  10:25 AM             5,510 License.txt
04/02/2019  01:35 PM    <DIR>          Program Files
04/09/2019  01:06 PM    <DIR>          Users
04/02/2019  01:35 PM    <DIR>          Windows
               1 File(s)          5,510 bytes
               4 Dir(s)  21,246,517,248 bytes free

C:\>^C
```

#### <a name="linux"></a>[Linux](#tab/linux)

この例では、`ENTRYPOINT` が `bash` に変更されています。 `exit` コマンドが実行されると、プロセスが終了してコンテナーが停止されます。

```bash
docker run -it --rm --entrypoint "bash" counter-image
root@b735b9799abf:/App# ls
NetCore.Docker.deps.json  NetCore.Docker.dll  NetCore.Docker.exe  NetCore.Docker.pdb  NetCore.Docker.runtimeconfig.json
root@b735b9799abf:/App# dotnet NetCore.Docker.dll 3
Counter: 1
Counter: 2
Counter: 3
root@b735b9799abf:/App# exit
exit
```

---

## <a name="essential-commands"></a>重要なコマンド

Docker には、コンテナーとイメージを作成、管理、操作するさまざまなコマンドが用意されています。 コンテナーの管理に不可欠な Docker コマンドは次のとおりです。

- [docker build](https://docs.docker.com/engine/reference/commandline/build/)
- [docker run](https://docs.docker.com/engine/reference/commandline/run/)
- [docker ps](https://docs.docker.com/engine/reference/commandline/ps/)
- [docker stop](https://docs.docker.com/engine/reference/commandline/stop/)
- [docker rm](https://docs.docker.com/engine/reference/commandline/rm/)
- [docker rmi](https://docs.docker.com/engine/reference/commandline/rmi/)
- [docker image](https://docs.docker.com/engine/reference/commandline/image/)

## <a name="clean-up-resources"></a>リソースをクリーンアップする

このチュートリアルでは、コンテナーとイメージを作成しました。 必要な場合は、これらのリソースを削除します。 次のコマンドを使います

01. すべてのコンテナーを一覧表示します

    ```Docker
    docker ps -a
    ```

02. 実行しているコンテナーを名前で選んで停止します。

    ```Docker
    docker stop counter-image
    ```

03. コンテナーを削除します

    ```Docker
    docker rm counter-image
    ```

次に、コンピューターに残しておきたくないイメージを削除します。 *Dockerfile* によって作成されたイメージを削除した後、*Dockerfile* が基にした .NET Core イメージを削除します。 **IMAGE ID** または **REPOSITORY:TAG** の書式に設定された文字列を使うことができます。

```Docker
docker rmi counter-image:latest
docker rmi mcr.microsoft.com/dotnet/core/aspnet:3.1
```

インストールされているイメージの一覧を表示するには、`docker images` コマンドを使います。

> [!TIP]
> イメージ ファイルは大きくなることがあります。 普通、アプリのテスト中および開発中に作成した一時的なコンテナーは削除します。 通常、ランタイムがインストールされた基本イメージは、そのランタイムを基にして他のイメージをビルドする予定がある場合は、残しておきます。

## <a name="next-steps"></a>次の手順

- [ASP.NET Core アプリケーションをコンテナー化する方法を学習します。](/aspnet/core/host-and-deploy/docker/building-net-docker-images)
- [ASP.NET Core マイクロサービスのチュートリアルを試します。](https://dotnet.microsoft.com/learn/web/aspnet-microservice-tutorial/intro)
- [コンテナーをサポートする Azure サービスを確認します。](https://azure.microsoft.com/overview/containers/)
- [Dockerfile のコマンドについて読みます。](https://docs.docker.com/engine/reference/builder/)
- [Visual Studio 向けのコンテナー ツールを調べます](/visualstudio/containers/overview)
