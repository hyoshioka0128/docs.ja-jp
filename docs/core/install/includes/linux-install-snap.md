---
ms.openlocfilehash: 5e77b7bd73c09e061a94a29703cf5286814d1ebb
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84602688"
---

[.NET Core は、Snap Store から入手できます。](https://snapcraft.io/dotnet-sdk)

Snap は、アプリとその依存関係のバンドルであり、さまざまな Linux ディストリビューション間で変更を加えることなく動作します。 Snap は、Snap Store で見つけてインストールできます。 Snap の詳細については、[Snap の概要](https://snapcraft.io/docs/getting-started)に関するページをご覧ください。

Snap では、サポートされているバージョンの .NET Core のみを利用できます。

### <a name="install-the-sdk"></a>SDK のインストール

.NET Core SDK の Snap パッケージは、すべて同じ識別子 (`dotnet-sdk`) で公開されます。 特定のバージョンの SDK は、チャネルを指定することによってインストールできます。 SDK には、対応するランタイムが含まれています。 次の表に、チャネルの一覧を示します。

| .NET Core バージョン | Snap パッケージ             |
|-------------------|--------------------------|
| 3.1 (LTS)         | `3.1` または `latest/stable` |
| 2.1 (LTS)         | `2.1`                    |
| .NET 5.0 preview  | `5.0/beta`               |

`snap install` コマンドを使用して、.NET Core SDK の Snap パッケージをインストールします。 `--channel` パラメーターを使用して、インストールするバージョンを指定します。 このパラメーターを省略すると、`latest/stable` が使用されます。 この例では、`3.1` が指定されています。

```bash
sudo snap install dotnet-sdk --classic --channel=3.1
```

次に、`snap alias` コマンドを使用して、システムの `dotnet` コマンドを登録します。

```bash
sudo snap alias dotnet-sdk.dotnet dotnet
```

このコマンドの形式は次のとおりです: `sudo snap alias {package}.{command} {alias}`。 `{alias}` の名前は自由に選択できます。 たとえば、snap によってインストールされた特定のバージョンにちなんでコマンドの名前を指定できます: `sudo snap alias dotnet-sdk.dotnet dotnet31`。 コマンド `dotnet31` を使用すると、この特定のバージョンの .NET が呼び出されます。 ただし、これはチュートリアルや例のほとんどと互換性がありません。それらでは `dotnet` コマンドが使用可能であることが想定されているためです。

### <a name="install-the-runtime"></a>ランタイムをインストールする

.NET Core ランタイムの Snap パッケージは、それぞれ独自のパッケージ識別子で公開されます。 次の表に、パッケージ識別子の一覧を示します。

| .NET Core バージョン | Snap パッケージ        |
|-------------------|---------------------|
| 3.1 (LTS)         | `dotnet-runtime-31` |
| 3.0               | `dotnet-runtime-30` |
| 2.2               | `dotnet-runtime-22` |
| 2.1 (LTS)         | `dotnet-runtime-21` |

`snap install` コマンドを使用して、.NET Core ランタイムの Snap パッケージをインストールします。 この例では、.NET Core 3.1 がインストールされます。

```bash
sudo snap install dotnet-runtime-31 --classic
```

次に、`snap alias` コマンドを使用して、システムの `dotnet` コマンドを登録します。

```bash
sudo snap alias dotnet-runtime-31.dotnet dotnet
```

このコマンドの形式は次のとおりです: `sudo snap alias {package}.{command} {alias}`。 `{alias}` の名前は自由に選択できます。 たとえば、snap によってインストールされた特定のバージョンにちなんでコマンドの名前を指定できます: `sudo snap alias dotnet-runtime-31.dotnet dotnet31`。 コマンド `dotnet31` を使用すると、この特定のバージョンの .NET が呼び出されます。 ただし、これはチュートリアルや例のほとんどと互換性がありません。それらでは `dotnet` コマンドが使用可能であることが想定されているためです。

### <a name="ssl-certificate-errors"></a>SSL 証明書のエラー

Snap を使用して .NET をインストールする場合、一部のディストリビューションでは .NET の SSL 証明書が見つからないことがあり、`restore` 中に次のようなエラーが表示されることがあります。

```bash
Processing post-creation actions...
Running 'dotnet restore' on /home/myhome/test/test.csproj...
  Restoring packages for /home/myhome/test/test.csproj...
/snap/dotnet-sdk/27/sdk/2.2.103/NuGet.targets(114,5): error : Unable to load the service index for source https://api.nuget.org/v3/index.json. [/home/myhome/test/test.csproj]
/snap/dotnet-sdk/27/sdk/2.2.103/NuGet.targets(114,5): error :   The SSL connection could not be established, see inner exception. [/home/myhome/test/test.csproj]
/snap/dotnet-sdk/27/sdk/2.2.103/NuGet.targets(114,5): error :   The remote certificate is invalid according to the validation procedure. [/home/myhome/test/test.csproj]
```

この問題を解決するには、いくつかの環境変数を設定します。

```bash
export SSL_CERT_FILE=[path-to-certificate-file]
export SSL_CERT_DIR=/dev/null
```

証明書の場所は、ディストリビューションによって異なります。 次に、問題が発生したディストリビューションの場所を示します。

* Fedora - `/etc/pki/ca-trust/extracted/pem/tls-ca-bundle.pem`
* OpenSUSE - `/etc/ssl/ca-bundle.pem`
* Solus - `/etc/ssl/certs/ca-certificates.crt`
