---
title: WCF 開発者向け Docker-gRPC
description: ASP.NET Core gRPC アプリケーション用の Docker イメージの作成
ms.date: 09/02/2019
ms.openlocfilehash: d23dc46526183b459c36f11bae4def8b1c9b9410
ms.sourcegitcommit: 5fb5b6520b06d7f5e6131ec2ad854da302a28f2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/03/2019
ms.locfileid: "74711302"
---
# <a name="create-docker-images"></a>Docker イメージを作成する

このセクションでは、ASP.NET Core gRPC アプリケーション用の Docker イメージを作成する方法について説明します。 Docker、Kubernetes、またはその他のコンテナー環境で実行できます。 ASP.NET Core MVC web アプリおよび gRPC サービスと共に使用されるサンプルアプリケーションは、GitHub の[dotnet/grpc-wcf 開発者](https://github.com/dotnet-architecture/grpc-for-wcf-developers/tree/master/KubernetesSample)リポジトリで入手できます。

## <a name="microsoft-base-images-for-aspnet-core-applications"></a>ASP.NET Core アプリケーション用の Microsoft 基本イメージ

Microsoft では、.NET Core アプリケーションをビルドして実行するためのさまざまな基本イメージを提供しています。 ASP.NET Core 3.0 イメージを作成するには、次の2つの基本イメージを使用します。 

- アプリケーションをビルドして発行するための SDK イメージ。
- 配置のランタイムイメージ。

| Image | 説明 |
| ----- | ----------- |
| [mcr.microsoft.com/dotnet/core/sdk](https://hub.docker.com/_/microsoft-dotnet-core-sdk/) | `docker build`を使用してアプリケーションをビルドする場合。 運用環境では使用されません。 |
| [mcr.microsoft.com/dotnet/core/aspnet](https://hub.docker.com/_/microsoft-dotnet-core-aspnet/) | ランタイムと ASP.NET Core の依存関係を含みます。 運用環境の場合。 |

各イメージには、タグによって識別される、異なる Linux ディストリビューションに基づく4つのバリエーションがあります。

| イメージタグ | Linux | メモ |
| --------- | ----- | ----- |
| 3.0-buster、3.0 | Debian 10 | OS バリアントが指定されていない場合の既定のイメージ。 |
| 3.0-アルペン | Alpine 3.9 | Alpine base イメージは Debian または Ubuntu よりもはるかに小さいものです。 |
| 3.0-disco | Ubuntu 19.04 | |
| 3.0-bionic | Ubuntu 18.04 | |

Alpine base イメージは約 100 MB であり、Debian および Ubuntu イメージでは 200 MB と比較しています。 一部のソフトウェアパッケージまたはライブラリは、アルペンのパッケージ管理では利用できない場合があります。 使用するイメージがわからない場合は、既定の Debian を選択することをお勧めします。

> [!IMPORTANT]
> ビルドとランタイムに同じ形式の Linux を使用していることを確認します。 1つのバリアントでビルドおよび発行されたアプリケーションが、別のバリアントで動作しない可能性があります。

## <a name="create-a-docker-image"></a>Docker イメージを作成する

Docker イメージは、 *Dockerfile*によって定義されます。 これは、アプリケーションを構築するために必要なすべてのコマンドを含むテキストファイルで、アプリケーションをビルドまたは実行するために必要なすべての依存関係をインストールします。 次の例は、ASP.NET Core 3.0 アプリケーションの最も単純な Dockerfile を示しています。

```dockerfile
# Application build steps
FROM mcr.microsoft.com/dotnet/core/sdk:3.0 as builder

WORKDIR /src

COPY . .

RUN dotnet restore

RUN dotnet publish -c Release -o /published src/StockData/StockData.csproj

# Runtime image creation
FROM mcr.microsoft.com/dotnet/core/aspnet:3.0

# Uncomment the line below if running with HTTPS
# ENV ASPNETCORE_URLS=https://+:443

WORKDIR /app

COPY --from=builder /published .

ENTRYPOINT [ "dotnet", "StockData.dll" ]
```

Dockerfile は2つの部分で構成されています。最初の部分では、アプリケーションをビルドして発行するために `sdk` 基本イメージを使用します。2つ目は、`aspnet` ベースからランタイムイメージを作成します。 これは、`sdk` イメージは約 900 MB であり、ランタイムイメージでは約 200 MB と比較され、そのほとんどの内容は実行時には不要であるためです。

### <a name="the-build-steps"></a>ビルドステップ

| 手順 | 説明 |
| ---- | ----------- |
| `FROM ...` | 基本イメージを宣言し、`builder` エイリアスを割り当てます。 |
| `WORKDIR /src` | `/src` ディレクトリを作成し、現在の作業ディレクトリとして設定します。 |
| `COPY . .` | ホスト上の現在のディレクトリの下にあるものをすべて、イメージの現在のディレクトリにコピーします。 |
| `RUN dotnet restore` | 外部パッケージを復元します (ASP.NET Core 3.0 framework は SDK と共にプレインストールされています)。 |
| `RUN dotnet publish ...` | リリースビルドをビルドして発行します。 `--runtime` フラグは必須ではないことに注意してください。 |

### <a name="the-runtime-image-steps"></a>ランタイムイメージの手順

| 手順 | 説明 |
| ---- | ----------- |
| `FROM ...` | 新しい基本イメージを宣言します。 |
| `WORKDIR /app` | `/app` ディレクトリを作成し、現在の作業ディレクトリとして設定します。 |
| `COPY --from=builder ...` | 最初の `FROM` 行の `builder` エイリアスを使用して、発行されたアプリケーションを前のイメージからコピーします。 |
| `ENTRYPOINT [ ... ]` | コンテナーの起動時に実行するコマンドを設定します。 ランタイムイメージの `dotnet` コマンドは、DLL ファイルのみを実行できます。 |

### <a name="https-in-docker"></a>Docker での HTTPS

Docker 用の Microsoft 基本イメージは、`ASPNETCORE_URLS` 環境変数を `http://+:80`に設定します。これは、Kestrel がそのポートで HTTPS を使用せずに実行されることを意味します。 ([自己ホスト型 gRPC アプリケーション](self-hosted.md)で説明されているように) カスタム証明書と共に HTTPS を使用している場合は、これをオーバーライドする必要があります。 Dockerfile のランタイムイメージ作成部分で環境変数を設定します。

```dockerfile
# Runtime image creation
FROM mcr.microsoft.com/dotnet/core/aspnet:3.0

ENV ASPNETCORE_URLS=https://+:443
```

### <a name="the-dockerignore-file"></a>Dockerignore ファイル

ソース管理から特定のファイルやディレクトリを除外する `.gitignore` ファイルと同様に、`.dockerignore` ファイルを使用して、ビルド時にファイルやディレクトリをイメージにコピーしないようにすることができます。 これにより、時間を節約できるだけでなく、PC の `obj` ディレクトリをイメージにコピーすることによって発生するエラーを回避することもできます。 少なくとも、`bin` のエントリと `obj` `.dockerignore` ファイルに追加する必要があります。

```console
bin/
obj/
```

## <a name="build-the-image"></a>イメージのビルド

単一のアプリケーションと1つの Dockerfile を持つソリューションでは、Dockerfile を基本ディレクトリに配置するのが最も簡単です。 つまり、`.sln` ファイルと同じディレクトリに配置します。 その場合は、イメージをビルドするために、Dockerfile が格納されているディレクトリから次の `docker build` コマンドを使用します。

```console
docker build --tag stockdata .
```

紛らわしいという名前の `--tag` フラグ (`-t`に短縮できます) は、指定されている場合は、実際のタグを含むイメージの完全な名前を指定します。 最後の `.` は、ビルドが実行されるコンテキストを指定します。Dockerfile 内の `COPY` コマンドの現在の作業ディレクトリ。

1つのソリューション内に複数のアプリケーションがある場合は、各アプリケーションの Dockerfile を、`.csproj` ファイルの横にある独自のフォルダーに保持できます。 引き続き、ベースディレクトリから `docker build` コマンドを実行して、ソリューションとすべてのプロジェクトがイメージにコピーされるようにする必要があります。 `--file` (または `-f`) フラグを使用して、現在のディレクトリの下に Dockerfile を指定できます。

```console
docker build --tag stockdata --file src/StockData/Dockerfile .
```

## <a name="run-the-image-in-a-container-on-your-machine"></a>コンピューターのコンテナーでイメージを実行する

ローカルの Docker インスタンスでイメージを実行するには、`docker run` コマンドを使用します。

```console
docker run -ti -p 5000:80 stockdata
```

`-ti` フラグは、現在のターミナルをコンテナーのターミナルに接続し、対話モードで実行します。 `-p 5000:80` は、コンテナー上のポート80を localhost ネットワークインターフェイスのポート80に発行 (リンク) します。

## <a name="push-the-image-to-a-registry"></a>レジストリにイメージをプッシュする

イメージが動作することを確認したら、それを Docker レジストリにプッシュして、他のシステムで使用できるようにします。 内部ネットワークでは、Docker レジストリをプロビジョニングする必要があります。 これは、 [docker の独自の `registry` イメージ](https://docs.docker.com/registry/deploying/)(docker コンテナーで実行される docker レジストリ) を実行するのと同じように簡単ですが、さまざまな包括的なソリューションを利用できます。 外部共有とクラウド使用については、 [Azure Container Registry](https://docs.microsoft.com/azure/container-registry/)や[Docker Hub](https://docs.docker.com/docker-hub/repos/)などのさまざまな管理対象レジストリを利用できます。

Docker Hub にプッシュするには、イメージ名の前にユーザー名または組織名を付けます。

```console
docker tag stockdata myorg/stockdata
docker push myorg/stockdata
```

プライベートレジストリにプッシュするには、イメージ名の前にレジストリのホスト名と組織名を付けます。

```console
docker tag stockdata internal-registry:5000/myorg/stockdata
docker push internal-registry:5000/myorg/stockdata
```

イメージがレジストリに格納された後、個々の Docker ホスト、または Kubernetes のようなコンテナーオーケストレーションエンジンにイメージを展開できます。

>[!div class="step-by-step"]
>[前へ](self-hosted.md)
>[次へ](kubernetes.md)
