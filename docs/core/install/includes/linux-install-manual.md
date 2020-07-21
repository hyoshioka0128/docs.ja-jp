---
ms.openlocfilehash: ea2883912907843e4b6d65db5ba186af43f27aaa
ms.sourcegitcommit: c23d9666ec75b91741da43ee3d91c317d68c7327
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85805714"
---

<!-- Note, this content is copied in ../macos.md. Any fixes should be applied there too, though content may be different -->

パッケージ マネージャーの代わりに、SDK とランタイムをダウンロードして手動でインストールすることもできます。 手動インストールは、通常、継続的インテグレーション テストの一環として、またはサポートされていない Linux ディストリビューションで実行されます。 開発者またはユーザーにとっては、通常はパッケージ マネージャーを使用することをお勧めします。

.NET Core SDK をインストールする場合、対応するランタイムをインストールする必要はありません。 まず、次のいずれかのサイトから SDK またはランタイムの**バイナリ** リリースをダウンロードします。

- ✔️ [.NET 5.0 preview のダウンロード](https://dotnet.microsoft.com/download/dotnet/5.0)
- ✔️ [.NET Core 3.1 のダウンロード](https://dotnet.microsoft.com/download/dotnet-core/3.1)
- ✔️ [.NET Core 2.1 のダウンロード](https://dotnet.microsoft.com/download/dotnet-core/2.1)
- [すべての .NET Core のダウンロード](https://dotnet.microsoft.com/download/dotnet-core)

次に、ダウンロードしたファイルを抽出し、`export` コマンドを使用して .NET Core で使用される変数を設定してから、.NET Core が PATH に含まれていることを確認します。

ランタイムを抽出し、.NET Core CLI コマンドをターミナルで使用できるようにするには、最初に .NET Core のバイナリ リリースをダウンロードします。 次に、ターミナルを開き、ファイルが保存されているディレクトリから次のコマンドを実行します。 アーカイブ ファイル名は、ダウンロードした内容によって異なる場合があります。

**次のコマンドを使用して、ランタイムを抽出します**。

```bash
mkdir -p "$HOME/dotnet" && tar zxf aspnetcore-runtime-3.1.0-linux-x64.tar.gz -C "$HOME/dotnet"
export DOTNET_ROOT=$HOME/dotnet
export PATH=$PATH:$HOME/dotnet
```

**次のコマンドを使用して、SDK を抽出します**。

```bash
mkdir -p "$HOME/dotnet" && tar zxf dotnet-sdk-3.1.301-linux-x64.tar.gz -C "$HOME/dotnet"
export DOTNET_ROOT=$HOME/dotnet
export PATH=$PATH:$HOME/dotnet
```

> [!TIP]
> 上記の `export` コマンドでは、それを実行したターミナル セッションでのみ .NET Core CLI コマンドを使用できるようになります。
>
> シェル プロファイルを編集して、コマンドを永続的に追加することができます。 Linux ではさまざまなシェルを使用でき、それぞれに異なるプロファイルがあります。 次に例を示します。
>
> - **Bash シェル**: *~/.bash_profile*、 *~/.bashrc*
> - **Korn シェル**: *~/.kshrc* または *.profile*
> - **Z シェル**: *~/.zshrc* または *.zprofile*
>
> シェルの適切なソース ファイルを編集し、既存の `PATH` ステートメントの末尾に `:$HOME/dotnet` を追加します。 `PATH` ステートメントが含まれていない場合は、`export PATH=$PATH:$HOME/dotnet` を含む新しい行を追加します。
>
> また、ファイルの末尾に `export DOTNET_ROOT=$HOME/dotnet` を追加します。

この方法では、別々の場所に異なるバージョンをインストールして、どのアプリケーションにどれを使用するかを明示的に選択できます。
