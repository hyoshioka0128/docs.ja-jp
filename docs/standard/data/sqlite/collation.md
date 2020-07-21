---
title: 照合順序
ms.date: 12/13/2019
description: カスタムの照合順序を作成する方法について説明します。
ms.openlocfilehash: 9879846cc191a62c4cb47a0fbaa47c59153ba61c
ms.sourcegitcommit: 7980a91f90ae5eca859db7e6bfa03e23e76a1a50
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/13/2020
ms.locfileid: "81242973"
---
# <a name="collation"></a>照合順序

照合順序は、SQLite によって TEXT 値を比較して順序と等価性を判断するときに使用されます。 SQL クエリで列の作成時または操作ごとに、使用する照合順序を指定できます。 SQLite には、既定で 3 つの照合順序があります。

| 照合順序 | 説明                               |
| --------- | ----------------------------------------- |
| RTRIM     | 末尾の空白を無視します               |
| NOCASE    | ASCII 文字 A から Z の大文字と小文字を区別しません |
| BINARY    | 大文字と小文字を区別します。 バイトを直接比較します   |

## <a name="custom-collation"></a>カスタム照合順序

<xref:Microsoft.Data.Sqlite.SqliteConnection.CreateCollation%2A> を使用して、独自の照合シーケンスを定義したり、組み込みの照合順序をオーバーライドしたりすることもできます。 次の例では、Unicode 文字をサポートするように NOCASE 照合順序をオーバーライドする方法を示しています。 [コード サンプル全体](https://github.com/dotnet/docs/blob/master/samples/snippets/standard/data/sqlite/CollationSample/Program.cs)は GitHub で入手できます。

[!code-csharp[](../../../../samples/snippets/standard/data/sqlite/CollationSample/Program.cs?name=snippet_Collation)]

## <a name="like-operator"></a>Like 演算子

SQLite の LIKE 演算子では照合順序が考慮されません。 既定の実装には、NOCASE 照合順序と同じセマンティクスがあります。 ASCII 文字 A から Z の場合に限り、大文字と小文字が区別されません。

次の pragma ステートメントを使用すると、簡単に LIKE 演算子で大文字と小文字が区別されるようにすることができます。

```sql
PRAGMA case_sensitive_like = 1
```

LIKE 演算子の実装のオーバーライドの詳細については、「[ユーザー定義関数](user-defined-functions.md)」を参照してください。

## <a name="see-also"></a>関連項目

* [ユーザー定義関数](user-defined-functions.md)
* [SQL 構文](https://www.sqlite.org/lang.html)
