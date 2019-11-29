---
title: 自己ホスト型 gRPC アプリケーション-WCF 開発者向け gRPC
description: ASP.NET Core gRPC アプリケーションを自己ホスト型サービスとして展開する。
ms.date: 09/02/2019
ms.openlocfilehash: 59f6275dbf85442bca3a98a1521597ef40e9675b
ms.sourcegitcommit: f348c84443380a1959294cdf12babcb804cfa987
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/12/2019
ms.locfileid: "73967214"
---
# <a name="self-hosted-grpc-applications"></a>自己ホスト型 gRPC アプリケーション

ASP.NET Core 3.0 アプリケーションは Windows Server の IIS でホストできますが、HTTP/2 機能の一部がまだサポートされていないため、IIS で gRPC アプリケーションをホストすることはできません。 この機能は、Windows Server の今後の更新プログラムで想定されています。

.NET Core 3.0 ホスト拡張機能のいくつかの新機能により、アプリケーションを Windows サービスとして、または[systemd](https://en.wikipedia.org/wiki/Systemd)によって制御される Linux サービスとして実行できます。

## <a name="run-your-app-as-a-windows-service"></a>Windows サービスとしてのアプリの実行

Windows サービスとして実行するように ASP.NET Core アプリケーションを構成する[には、NuGet からパッケージを](https://www.nuget.org/packages/Microsoft.Extensions.Hosting.WindowsServices)インストールします。 次に、`Program.cs`の `CreateHostBuilder` メソッドに `UseWindowsService` の呼び出しを追加します。

```csharp
public static IHostBuilder CreateHostBuilder(string[] args) =>
    Host.CreateDefaultBuilder(args)
        .UseWindowsService() // Enable running as a Windows service
        .ConfigureWebHostDefaults(webBuilder =>
        {
            webBuilder.UseStartup<Startup>();
        });
```

> [!NOTE]
> アプリケーションが Windows サービスとして実行されていない場合、`UseWindowsService` 方法では何も実行されません。

次に、Visual Studio でプロジェクトを右クリックし、コンテキストメニューから [発行] を選択するか、.NET Core CLI から [*発行*] を選択して、アプリケーションを発行します。

.NET Core アプリケーションを発行するときに、*フレームワークに依存*する展開と*自己完結*型の展開のどちらを作成するかを選択できます。 フレームワークに依存する展開では、.NET Core 共有ランタイムが実行されているホストにインストールされている必要があります。 自己完結型の展開は、.NET Core ランタイムとフレームワークの完全なコピーを使用して発行され、任意のホストで実行できます。 各方法の長所と短所を含む詳細については、 [.Net Core アプリケーションの展開](https://docs.microsoft.com/dotnet/core/deploying/)に関するドキュメントを参照してください。

.NET Core 3.0 ランタイムをホストにインストールする必要がないアプリケーションの自己完結型のビルドを発行するには、`-r` (または `--runtime`) フラグを使用して、アプリケーションに含めるランタイムを指定します。

```console
dotnet publish -c Release -r win-x64 -o ./publish
```

フレームワークに依存するビルドを発行するには、`-r` フラグを省略します。

```console
dotnet publish -c Release -o ./publish
```

`publish` ディレクトリの完全な内容をインストールフォルダーにコピーし、 [sc ユーティリティ](https://docs.microsoft.com/windows/desktop/services/controlling-a-service-using-sc)を使用して、実行可能ファイルの Windows サービスを作成します。

```console
sc create MyService binPath=C:\MyService\MyService.exe
```

### <a name="log-to-windows-event-log"></a>Windows イベントログに記録する

`UseWindowsService` メソッドは、ログメッセージを Windows イベントログに書き込むログ[記録](https://docs.microsoft.com/aspnet/core/fundamentals/logging/?view=aspnetcore-3.0)プロバイダーを自動的に追加します。 `appsettings.json` またはその他の構成ソースの `Logging` セクションに `EventLog` エントリを追加することによって、このプロバイダーのログ記録を構成できます。 イベントログで使用されるソース名は、これらの設定の `SourceName` プロパティを設定することによってオーバーライドできます。名前を指定しない場合は、既定のアプリケーション名 (通常は実行可能アセンブリ名) が使用されます。

ログ記録の詳細については、この章の最後を参照してください。

## <a name="run-your-app-as-a-linux-service-with-systemd"></a>Systemd を使用してアプリを Linux サービスとして実行する

Linux サービス (Linux 用語の*デーモン*) として実行するように ASP.NET Core アプリケーションを構成するには、NuGet から[パッケージをインストールします](https://www.nuget.org/packages/Microsoft.Extensions.Hosting.Systemd)。 次に、`Program.cs`の `CreateHostBuilder` メソッドに `UseSystemd` の呼び出しを追加します。

```csharp
public static IHostBuilder CreateHostBuilder(string[] args) =>
    Host.CreateDefaultBuilder(args)
        .UseSystemd() // Enable running as a Systemd service
        .ConfigureWebHostDefaults(webBuilder =>
        {
            webBuilder.UseStartup<Startup>();
        });
```

> [!NOTE]
> アプリケーションが Linux サービスとして実行されていない場合、`UseSystemd` 方法では何も実行されません。

次に、Visual Studio からプロジェクトを右クリックし、コンテキストメニューから [*発行*] を選択して、または .NET Core CLI から次のコマンドを使用して、アプリケーション (フレームワークに依存する、または、`linux-x64`など) を発行します。

```console
dotnet publish -c Release -r linux-x64 -o ./publish
```

`publish` ディレクトリの完全な内容を、Linux ホストのインストールフォルダーにコピーします。 サービスを登録するには、"ユニットファイル" と呼ばれる特殊なファイルを `/etc/systemd/system` ディレクトリに追加する必要があります。 このフォルダーにファイルを作成するには、ルートアクセス許可が必要です。 使用する `systemd` する識別子と `.service` 拡張子をファイルに付けます。 たとえば、`/etc/systemd/system/myapp.service` のようにします。

この例に示すように、サービスファイルは INI 形式を使用します。

```ini
[Unit]
Description=My gRPC Application

[Service]
Type=notify
ExecStart=/usr/sbin/myapp

[Install]
WantedBy=multi-user.target
```

`Type=notify` プロパティは、アプリケーションが起動時およびシャットダウン時に通知する `systemd` を示します。 `WantedBy=multi-user.target` 設定を行うと、Linux システムが "ランレベル 2" に達したときにサービスが開始されます。これは、グラフィカルでないマルチユーザーシェルがアクティブであることを意味します。

`systemd` がサービスを認識する前に、その構成を再読み込みする必要があります。 `systemctl` コマンドを使用して、`systemd` を制御します。 再読み込みが完了したら、`status` サブコマンドを使用して、アプリケーションが正常に登録されたことを確認します。

```console
sudo systemctl daemon-reload
sudo systemctl status myapp
```

サービスが正しく構成されている場合は、次の出力が表示されます。

```text
myapp.service - My gRPC Application
 Loaded: loaded (/etc/systemd/system/myapp.service; disabled; vendor preset: enabled)
 Active: inactive (dead)
```

サービスを開始するには、`start` コマンドを使用します。

```console
sudo systemctl start myapp.service
```

> [!TIP]
> `systemctl start`を使用する場合、`.service` の拡張機能は省略可能です。

システムの起動時にサービスを自動的に開始するように `systemd` するには、`enable` コマンドを使用します。

```console
sudo systemctl enable myapp
```

### <a name="log-to-journald"></a>Journald にログを記録する

Linux と同等の Windows イベントログは `journald`であり、`systemd`に含まれる構造化されたログ記録システムサービスです。 Linux デーモンによって標準出力に書き込まれたログメッセージは `journald`に自動的に書き込まれます。そのため、ログ記録レベルを構成するには、ログ構成の `Console` セクションを使用します。 `UseSystemd` host builder メソッドは、journal に合わせてコンソールの出力形式を自動的に構成します。

`journald` は Linux ログの標準であるため、統合されたさまざまなツールがあり、`journald` から外部ログシステムにログを簡単にルーティングできます。 ホストでローカルに作業している場合は、`journalctl` コマンドを使用して、コマンドラインからのログを表示できます。

```console
sudo journalctl -u myapp
```

> [!TIP]
> ホストで使用できる GUI 環境がある場合は、 *QJournalctl*や*gnome ログ*など、Linux で使用できるグラフィカルなログビューアーがいくつかあります。

`journalctl`を使用してコマンドラインから systemd journal にクエリを実行する方法の詳細については、 [man ページ](https://manpages.debian.org/buster/systemd/journalctl.1)を参照してください。

## <a name="https-certificates-for-self-hosted-applications"></a>自己ホスト型アプリケーションの HTTPS 証明書

運用環境で gRPC アプリケーションを実行する場合は、信頼された証明機関 (CA) からの TLS 証明書を使用する必要があります。 この CA は、パブリック CA、または組織の内部の ca のいずれかになります。

Windows ホストでは、 [X509Store クラス](https://docs.microsoft.com/dotnet/api/system.security.cryptography.x509certificates.x509store?view=netcore-3.0)を使用して、セキュリティで保護された[証明書ストア](https://docs.microsoft.com/windows/win32/seccrypto/managing-certificates-with-certificate-stores)から証明書を読み込むことができます。 `X509Store` クラスは、一部の Linux ホスト上の OpenSSL キーストアでも使用できます。

証明書は、 [X509Certificate2 コンストラクター](https://docs.microsoft.com/dotnet/api/system.security.cryptography.x509certificates.x509certificate.-ctor?view=netcore-3.0)のいずれかを使用して作成することもできます。これには、ファイル (強力なパスワードで保護されたファイル `.pfx` など) から、またはセキュリティで保護されたストレージサービスから取得したバイナリデータ (たとえば、 [Azure Key Vault](https://azure.microsoft.com/services/key-vault/)) を使用します。

Kestrel は、構成から、またはコード内の2つの方法で証明書を使用するように構成できます。

### <a name="set-https-certificates-using-configuration"></a>構成を使用して HTTPS 証明書を設定する

構成方法では、証明書 `.pfx` ファイルのパスと Kestrel 構成セクションのパスワードを設定する必要があります。 `appsettings.json` では、次のようになります。

```json
{
  "Kestrel": {
    "Certificates": {
      "Default": {
        "Path": "cert.pfx",
        "Password": "DO NOT STORE PLAINTEXT PASSWORDS IN APPSETTINGS FILES"
      }
    }
  }
}
```

パスワードは、Azure KeyVault や Hashicorp Vault などのセキュリティで保護された構成ソースを使用して指定する必要があります。

暗号化されていないパスワードを構成ファイルに格納しないでください。

### <a name="set-https-certificates-in-code"></a>コードでの HTTPS 証明書の設定

コードで Kestrel の HTTPS を構成するには、`Program` クラスの `IWebHostBuilder` で `ConfigureKestrel` メソッドを使用します。

```csharp
public static IHostBuilder CreateHostBuilder(string[] args) =>
    Host.CreateDefaultBuilder(args)
        .ConfigureWebHostDefaults(webBuilder =>
        {
            webBuilder.UseStartup<Startup>();
            webBuilder.ConfigureKestrel(kestrel =>
            {
                kestrel.ConfigureHttpsDefaults(https =>
                {
                    https.ServerCertificate = new X509Certificate2("mycert.pfx", "password");
                });
            });
        });
```

ここでも、`.pfx` ファイルのパスワードを格納し、セキュリティで保護された構成ソースから取得する必要があります。

>[!div class="step-by-step"]
>[前へ](grpc-in-production.md)
>[次へ](docker.md)
