---
title: カスタム SQLite のバージョン
ms.date: 05/14/2020
description: ネイティブ SQLite ライブラリのカスタム バージョンを使用する方法について説明します。
ms.openlocfilehash: 15db10db26bc7c5017313ca020a0e1e528ba207a
ms.sourcegitcommit: 7b1497c1927cb449cefd313bc5126ae37df30746
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/16/2020
ms.locfileid: "83440838"
---
# <a name="custom-sqlite-versions"></a>カスタム SQLite のバージョン

`Microsoft.Data.Sqlite` は、`SQLitePCLRaw` に基づいています。 カスタム バージョンのネイティブ SQLite ライブラリを使用するには、バンドルを使用するか、`SQLitePCLRaw` プロバイダーを構成します。

## <a name="bundles"></a>バンドル

`SQLitePCLRaw` には利便性に基づくバンドル パッケージが用意されているため、さまざまなプラットフォームで適切な依存関係を簡単に取り込むことができます。 メインの `Microsoft.Data.Sqlite` パッケージでは、既定で `SQLitePCLRaw.bundle_e_sqlite3` が取り込まれます。 別のバンドルを使用するには、使用するバンドル パッケージとともに、`Microsoft.Data.Sqlite.Core` パッケージを代わりにインストールします。 バンドルは、`Microsoft.Data.Sqlite` によって自動的に初期化されます。

| バンドル | 説明 |
|--|--|
| [SQLitePCLRaw.bundle_e_sqlite3](https://www.nuget.org/packages/SQLitePCLRaw.bundle_e_sqlite3) | すべてのプラットフォームで同じバージョンの SQLite を提供します。 FTS4、FTS5、JSON1、R*Tree 拡張機能を含みます。 既定値です。 |
| [SQLitePCLRaw.bundle_e_sqlcipher](https://www.nuget.org/packages/SQLitePCLRaw.bundle_e_sqlcipher) | オープン ソースの非公式の `SQLCipher` ビルドを提供します。 |
| [SQLitePCLRaw.bundle_green](https://www.nuget.org/packages/SQLitePCLRaw.bundle_green) | `bundle_e_sqlite3` と同じですが、iOS の場合はシステム SQLite ライブラリが使用されます。 |
| [SQLitePCLRaw.bundle_winsqlite3](https://www.nuget.org/packages/SQLitePCLRaw.bundle_winsqlite3) | Windows 10 のシステム SQLite ライブラリである `winsqlite3.dll` が使用されます。 |
| [SQLitePCLRaw.bundle_zetetic](https://www.nuget.org/packages/SQLitePCLRaw.bundle_zetetic) | Zetetic の公式の `SQLCipher` ビルドが使用されます (含まれていません)。 |

たとえば、オープン ソースの非公式の `SQLCipher` ビルドを使用するには、次のコマンドを使用します。

### <a name="net-core-cli"></a>[.NET Core CLI](#tab/netcore-cli)

```dotnetcli
dotnet add package Microsoft.Data.Sqlite.Core
dotnet add package SQLitePCLRaw.bundle_e_sqlcipher
```

### <a name="visual-studio"></a>[Visual Studio](#tab/visual-studio)

``` PowerShell
Install-Package Microsoft.Data.Sqlite.Core
Install-Package SQLitePCLRaw.bundle_e_sqlcipher
```

---

## <a name="sqlitepclraw-available-providers"></a>SQLitePCLRaw を利用できるプロバイダー

バンドルに依存しない場合は、コア アセンブリで SQLite の利用可能なプロバイダーを使用できます。

| プロバイダー | 説明 |
|--|--|
| [SQLitePCLRaw.provider.dynamic](https://www.nuget.org/packages/SQLitePCLRaw.provider.dynamic) | `dynamic` プロバイダーでは <xref:System.Runtime.InteropServices.DllImportAttribute?displayProperty=nameWithType> 属性を使用する代わりにネイティブ ライブラリが読み込まれます。 このプロバイダーの使用方法の詳細については、「[動的プロバイダーを使用する](#use-the-dynamic-provider)」をご覧ください。 |
| [SQLitePCLRaw.provider.e_sqlite3](https://www.nuget.org/packages/SQLitePCLRaw.provider.e_sqlite3) | `e_sqlite3` は既定のプロバイダーです。 |
| [SQLitePCLRaw.provider.e_sqlcipher](https://www.nuget.org/packages/SQLitePCLRaw.provider.e_sqlcipher) | `e_sqlcipher` プロバイダーは、非公式でサポートされていない `SQLCipher` です。 |
| [SQLitePCLRaw.provider.sqlite3](https://www.nuget.org/packages/SQLitePCLRaw.provider.sqlite3) | `sqlite3` プロバイダーは、iOS、macOS、Linux 用のシステム提供の `SQLite` です。 |
| [SQLitePCLRaw.provider.sqlcipher](https://www.nuget.org/packages/SQLitePCLRaw.provider.sqlcipher) | `sqlcipher` プロバイダーは、`Zetetic` からの公式 `SQLCipher` ビルド用です。 |
| [SQLitePCLRaw.provider.winsqlite3](https://www.nuget.org/packages/SQLitePCLRaw.provider.winsqlite3) | `winsqlite3` プロバイダーは Windows 10 環境用です。 |

`sqlite3` プロバイダーを使用するには、次のコマンドを使用します。

### <a name="net-core-cli"></a>[.NET Core CLI](#tab/netcore-cli)

```dotnetcli
dotnet add package Microsoft.Data.Sqlite.Core
dotnet add package SQLitePCLRaw.core
dotnet add package SQLitePCLRaw.provider.sqlite3
```

### <a name="visual-studio"></a>[Visual Studio](#tab/visual-studio)

``` PowerShell
Install-Package Microsoft.Data.Sqlite.Core
Install-Package SQLitePCLRaw.core
Install-Package SQLitePCLRaw.provider.sqlite3
```

---

パッケージをインストールしたら、プロバイダーを `sqlite3` インスタンスに設定します。

[!code-csharp[](../../../../samples/snippets/standard/data/sqlite/SqliteProviderSample/Program.cs)]

## <a name="use-the-dynamic-provider"></a>動的プロバイダーを使用する

`SQLitePCLRaw.provider.dynamic_cdecl` パッケージを利用すると、独自の SQLite ビルドを使用できます。 この場合、アプリとともにネイティブ ライブラリをデプロイする必要があります。 ただし、アプリとともにネイティブ ライブラリをデプロイする場合の詳細は、使用している .NET プラットフォームとランタイムによって大きく異なります。

まず、`IGetFunctionPointer` を実装する必要があります。 .NET Core での実装は次のようになります。

[!code-csharp[](../../../../samples/snippets/standard/data/sqlite/SystemLibrarySample/Program.cs?name=snippet_NativeLibraryAdapter)]

次に、`SQLitePCLRaw` プロバイダーを構成します。 これは、アプリで `Microsoft.Data.Sqlite` が使用される前に行ってください。 また、プロバイダーがオーバーライドされる可能性のある `SQLitePCLRaw` バンドル パッケージを使用しないようにしてください。

[!code-csharp[](../../../../samples/snippets/standard/data/sqlite/SystemLibrarySample/Program.cs?name=snippet_SetProvider)]
