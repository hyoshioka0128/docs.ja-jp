---
title: WCF 開発者向け Docker-gRPC
description: ASP.NET Core gRPC アプリケーション用の Docker イメージの作成
ms.date: 09/02/2019
ms.openlocfilehash: a5aceb4b5270cb828965e990a62db4147012adff
ms.sourcegitcommit: f348c84443380a1959294cdf12babcb804cfa987
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/12/2019
ms.locfileid: "73967837"
---
# <a name="docker"></a>Docker

このセクションでは ASP.NET Core gRPC アプリケーション用の Docker イメージの作成について説明し、Docker、Kubernetes、またはその他のコンテナー環境で実行できるようにします。 ASP.NET Core MVC web アプリおよび gRPC サービスと共に使用されるサンプルアプリケーションは、GitHub の[dotnet/grpc-wcf 開発者](https://github.com/dotnet-architecture/grpc-for-wcf-developers/tree/master/KubernetesSample)リポジトリで入手できます。

## <a name="microsoft-base-images-for-aspnet-core-applications"></a>ASP.NET Core アプリケーション用の Microsoft 基本イメージ

Microsoft では、.NET Core アプリケーションをビルドして実行するためのさまざまな基本イメージを提供しています。 ASP.NET Core 3.0 イメージを作成するには、アプリケーションをビルドして発行するための SDK イメージと配置用のランタイムイメージという2つの基本イメージが使用されます。

| イメージ | 説明 |
| ----- | ----------- |
| [mcr.microsoft.com/dotnet/core/sdk](https://hub.docker.com/_/microsoft-dotnet-core-sdk/) | `docker build`を使用してアプリケーションをビルドする場合。 運用環境では使用されません。 |
| [mcr.microsoft.com/dotnet/core/aspnet](https://hub.docker.com/_/microsoft-dotnet-core-aspnet/) | ランタイムと ASP.NET Core の依存関係を含みます。 運用環境の場合。 |

各イメージには、タグによって識別される、異なる Linux ディストリビューションに基づく4つのバリエーションがあります。

| イメージタグ | Linux | 説明 |
| --------- | ----- | ----- |
| 3.0-buster、3.0 | Debian 10 | OS バリアントが指定されていない場合の既定のイメージ。 |
| 3.0-アルペン | Alpine 3.9 | Alpine base イメージは Debian または Ubuntu よりもはるかに小さいものです。 |
| 3.0-disco | Ubuntu 19.04 | |
| 3.0-bionic | Ubuntu 18.04 | |

Alpine base イメージは約 100 MB であり、Debian および Ubuntu イメージでは 200 MB と比較していますが、一部のソフトウェアパッケージまたはライブラリは Alpine のパッケージ管理では利用できない可能性があります。 使用するイメージがわからない場合は、別のディストリビューションを使用する必要がある場合を除き、既定の Debian にすることをお勧めします。

> [!IMPORTANT]
> ビルドとランタイムに同じ形式の Linux を使用していることを確認します。 あるバリアントでビルドおよび発行されたアプリケーションは、別のバリアントでは機能しない可能性があります。

## <a name="create-a-docker-image"></a>Docker イメージを作成する

Docker イメージは、 *Dockerfile*(アプリケーションのビルドに必要なすべてのコマンドを含むテキストファイル) と、アプリケーションをビルドまたは実行するために必要な依存関係をインストールするために定義されます。 次の例は、ASP.NET Core 3.0 アプリケーションの最も単純な Dockerfile を示しています。

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

Dockerfile は2つの部分で構成されています。最初の部分では、アプリケーションをビルドして発行するために `sdk` 基本イメージを使用します。2つ目は、`aspnet` ベースからランタイムイメージを作成します。 これは、`sdk` のイメージは、ランタイムイメージの約 200 MB と比較して約 900 MB であり、その内容のほとんどは実行時には不要であるためです。

### <a name="the-build-steps"></a>ビルドステップ

| 手順 | 説明 |
| ---- | ----------- |
| `FROM ...` | 基本イメージを宣言し、`builder` エイリアスを割り当てます (説明については、次のセクションを参照してください)。 |
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

Docker 用の Microsoft の基本イメージは、`ASPNETCORE_URLS` 環境変数を `http://+:80`に設定します。これは、Kestrel がそのポートで HTTPS を使用せずに実行されることを意味します。 ([前のセクション](self-hosted.md)で説明したように) カスタム証明書と共に HTTPS を使用している場合は、Dockerfile の**ランタイムイメージ作成部分で**環境変数を設定することにより、これをオーバーライドする必要があります。

```dockerfile
# Runtime image creation
FROM mcr.microsoft.com/dotnet/core/aspnet:3.0

ENV ASPNETCORE_URLS=https://+:443
```

### <a name="the-dockerignore-file"></a>Dockerignore ファイル

ソース管理から特定のファイルやディレクトリを除外する `.gitignore` ファイルと同様に、`.dockerignore` ファイルを使用して、ビルド時にファイルやディレクトリをイメージにコピーしないようにすることができます。 これにより、コピー時間が短縮されるだけでなく、PC からの `obj` ディレクトリがイメージにコピーされたことによって発生する混乱したエラーを回避することもできます。 少なくとも `bin` のエントリを追加し、`.dockerignore` ファイルに `obj` する必要があります。

```console
bin/
obj/
```

## <a name="build-the-image"></a>イメージのビルド

単一のアプリケーションと1つの Dockerfile を持つソリューションでは、Dockerfile を基本ディレクトリに配置するのが最も簡単です。つまり、`.sln` ファイルと同じディレクトリになります。 その場合は、イメージをビルドするために、Dockerfile が格納されているディレクトリから次の `docker build` コマンドを使用します。

```console
docker build --tag stockdata .
```

紛らわしいという名前の `--tag` フラグ (`-t`に短縮できます) は、指定されている場合は、実際のタグを*含む*イメージの完全な名前を指定します。 最後の `.` は、ビルドが実行される*コンテキスト*を指定します。Dockerfile 内の `COPY` コマンドの現在の作業ディレクトリ。

1つのソリューション内に複数のアプリケーションがある場合は、各アプリケーションの Dockerfile を `.csproj` ファイルの隣にある独自のフォルダーに保持できますが、ソリューションとすべてのプロジェクトがイメージにコピーされるようにするには、ベースディレクトリから `docker build` コマンドを実行する必要があります。 `--file` (または `-f`) フラグを使用して、現在のディレクトリの下に Dockerfile を指定できます。

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

イメージが動作することを確認したら、それを Docker レジストリにプッシュして、他のシステムで使用できるようにする必要があります。 内部ネットワークでは、Docker レジストリをプロビジョニングする必要があります。 これは、 [docker 独自の `registry` イメージ](https://docs.docker.com/registry/deploying/)(つまり、docker レジストリは docker コンテナーで実行されます) を実行するのと同じように簡単ですが、さまざまな包括的なソリューションを利用できます。 外部共有とクラウド使用については、 [Azure Container Registry](https://docs.microsoft.com/azure/container-registry/)や[Docker Hub](https://docs.docker.com/docker-hub/repos/)などのさまざまな管理対象レジストリを利用できます。

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

イメージがレジストリに登録されたら、それを個々の Docker ホストまたは Kubernetes のようなコンテナーオーケストレーションエンジンに展開できます。

>[!div class="step-by-step"]
>[前へ](self-hosted.md)
>[次へ](kubernetes.md)
