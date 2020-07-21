---
title: 暗号化
ms.date: 12/13/2019
description: データベースファイルを暗号化する方法について説明します。
ms.openlocfilehash: ccdd4b6b8642b3cde1c2667c9ca432a9b0ef21f2
ms.sourcegitcommit: 30a558d23e3ac5a52071121a52c305c85fe15726
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/25/2019
ms.locfileid: "75450484"
---
# <a name="encryption"></a>暗号化

SQLite では、既定により、データベース ファイルの暗号化はサポートされません。 代わりに、修正した SQLite バージョンの [SEE](https://www.hwaci.com/sw/sqlite/see.html)、[SQLCipher](https://www.zetetic.net/sqlcipher/)、[SQLiteCrypt](http://www.sqlite-crypt.com/)、[wxSQLite3](https://utelle.github.io/wxsqlite3) などを使用する必要があります。 この記事では、SQLCipher のサポートされていないオープンソース ビルドの使用について説明しますが、他のソリューションにも当てはまります。これらも一般的に同じパターンに従っているためです。

## <a name="installation"></a>インストール

### <a name="net-core-cli"></a>[.NET Core CLI](#tab/netcore-cli)

```dotnetcli
dotnet remove package Microsoft.Data.Sqlite
dotnet add package Microsoft.Data.Sqlite.Core
dotnet add package SQLitePCLRaw.bundle_e_sqlcipher
```

### <a name="visual-studio"></a>[Visual Studio](#tab/visual-studio)

``` PowerShell
Remove-Package Microsoft.Data.Sqlite
Install-Package Microsoft.Data.Sqlite.Core
Install-Package SQLitePCLRaw.bundle_e_sqlcipher
```

---

暗号化に別のネイティブ ライブラリを使用する場合の詳細については、「[カスタム SQLite のバージョン](custom-versions.md)」を参照してください。

## <a name="specify-the-key"></a>キーを指定する

暗号化を有効にするには、`Password` 接続文字列キーワードを使用してキーを指定します。 <xref:Microsoft.Data.Sqlite.SqliteConnectionStringBuilder> を使用して、ユーザー入力の値を追加または更新し、接続文字列のインジェクション攻撃を回避します。

[!code-csharp[](../../../../samples/snippets/standard/data/sqlite/EncryptionSample/Program.cs?name=snippet_ConnectionStringBuilder)]

## <a name="rekeying-the-database"></a>データベースのキーを更新する

データベースの暗号化キーを変更する場合は、`PRAGMA rekey` ステートメントを実行します。 データベースの暗号化を解除するには、`NULL` を指定します。

ただし、SQLite では `PRAGMA` ステートメントのパラメーターはサポートされません。 代わりに、`quote()` 関数を使用して、SQL インジェクションを防止してください。

[!code-csharp[](../../../../samples/snippets/standard/data/sqlite/EncryptionSample/Program.cs?name=snippet_Rekey)]
