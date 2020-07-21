---
title: System.Data.SQLite との比較
ms.date: 12/13/2019
description: Microsoft.Data.Sqlite と System.Data.SQLite のライブラリーの相違点をいくつか紹介します。
ms.openlocfilehash: 076bbc6f746cf9296c96ec73047397a21a3b2558
ms.sourcegitcommit: 7088f87e9a7da144266135f4b2397e611cf0a228
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/11/2020
ms.locfileid: "75900711"
---
# <a name="comparison-to-systemdatasqlite"></a>System.Data.SQLite との比較

2005 年に、Robert Simpson は ADO.NET 2.0 用の SQLite プロバイダーである System.Data.SQLite を作成しました。 2010 年に、SQLite チームがプロジェクトのメンテナンスと開発を引き継ぎました。 また、2007 年に Mono チームがコードを Mono.Data.Sqlite としてフォークしたことも注目すべき点です。 System.Data.SQLite には長い歴史があり、Visual Studio ツールを備えた、安定したフル機能の ADO.NET プロバイダーに進化してきました。 新しいリリースでは引き続き、.NET Framework のすべてのバージョン (バージョン 2.0 や、.NET Compact Framework 3.5 も含む) と互換性のあるアセンブリが提供されています。

.NET Core の最初のバージョン (2016 年にリリース) は、軽量で最新、かつクロスプラットフォームの .NET の 1 つの実装でした。 古くなった API や、代わりとなる新しいものがある API は、意図的に削除されています。 ADO.NET には DataSet API (DataTable と DataAdapter を含む) は含まれていませんでした。

Entity Framework チームは、System.Data.SQLite コードベースについてある程度熟知していました。 EF チームのメンバーである Brice Lambson は、過去に SQLite チームが Entity Framework バージョン 5 と 6 のサポートを追加する作業を補助していました。 また Brice は、.NET Core が計画されていたときと同時期に、SQLite ADO.NET プロバイダーの独自の実装を実験していました。 長期にわたる話し合いの後、Entity Framework チームは、Brice のプロトタイプに基づいて Microsoft.Data.Sqlite を作成することを決定しました。 これにより、.NET Core の目標に沿った、軽量で最新の新たな実装を作成できるようになりました。

最新が意味するものを表す例として、以下に、System.Data.SQLite と Microsoft.Data.Sqlite の両方で[ユーザー定義関数](user-defined-functions.md)を作成するコードを示します。

```csharp
// System.Data.SQLite
connection.BindFunction(
    new SQLiteFunctionAttribute("ceiling", 1, FunctionType.Scalar),
    (Func<object[], object>)((object[] args) => Math.Ceiling((double)((object[])args[1])[0])),
    null);

// Microsoft.Data.Sqlite
connection.CreateFunction(
    "ceiling",
    (double arg) => Math.Ceiling(arg));
```

2017 年に、.NET Core 2.0 の戦略が変更されました。 .NET Core の成功には .NET Framework との互換性が不可欠であると判断したのです。 DataSet API など、削除されていた API の多くが再び追加されました。 他の多くのものと同様に、これによって System.Data.SQLite の障害となっていた要素が取り除かれ、.NET Core にも移植できるようになりました。 ただし、Microsoft.Data.Sqlite の当初の目標である軽量で最新という点も引き続き維持されています。 Microsoft.Data.Sqlite で実装されていない ADO.NET API の詳細については、「[ADO.NET の制限事項](adonet-limitations.md)」を参照してください。

Microsoft.Data.Sqlite に新機能が追加されるときは、System.Data.SQLite の設計が考慮されます。 Microsoft では、この 2 つの切り替えを容易にするため、できる限り、これらの間で行う変更を最小限に抑えるように努力しています。

## <a name="data-types"></a>データの種類

Microsoft.Data.Sqlite と System.Data.SQLite の最も大きな違いはデータ型の処理方法です。 「[データ型](types.md)」で説明しているように、Microsoft.Data.Sqlite では SQLite の根本にある特異な点、つまり、すべての任意文字列を列の型として指定でき、そのプリミティブ型は、INTEGER、REAL、TEXT、および BLOB の 4 つだけあるということを明らかにしています。

System.Data.SQLite では、追加のセマンティクスが列の型に適用され、それらが直接 .NET 型にマップされます。 これにより、このプロバイダーはより厳密に型指定されている印象を与えますが、改善が必要な点もあります。 たとえば、SELECT ステートメントで式の列の型を指定するために、新しい SQL ステートメント (TYPES) を導入する必要がありました。

## <a name="connection-strings"></a>接続文字列

Microsoft.Data.Sqlite の方が、[接続文字列](connection-strings.md)キーワードの数が大幅に少なくなります。 次の表に、使用できる代替手段を示します。

| キーワード          | 代替                                         |
| ---------------- | --------------------------------------------------- |
| Cache Size       | `PRAGMA cache_size = <pages>` を送信します                  |
| [Default Timeout]\(既定のタイムアウト\)  | SqliteConnection の DefaultTimeout プロパティを使用します |
| FailIfMissing    | `Mode=ReadWrite` を使用します                                |
| FullUri          | データ ソース キーワードを使用します                         |
| Journal Mode     | `PRAGMA journal_mode = <mode>` を送信します                 |
| Legacy Format    | `PRAGMA legacy_file_format = 1` を送信します                |
| Max Page Count   | `PRAGMA max_page_count = <pages>` を送信します              |
| Page Size        | `PRAGMA page_size = <bytes>` を送信します                   |
| [読み取り専用]        | `Mode=ReadOnly` を使用します                                 |
| 同期      | `PRAGMA synchronous = <mode>` を送信します                  |
| URI              | データ ソース キーワードを使用します                         |
| UseUTF16Encoding | `PRAGMA encoding = 'UTF-16'` を送信します                   |

## <a name="authorization"></a>承認

Microsoft.Data.Sqlite には、SQLite の認証コールバックを公開する API がありません。 この機能に関するフィードバックを送信するには、問題 [#13835](https://github.com/dotnet/efcore/issues/13835) を使用してください。

## <a name="data-change-notifications"></a>データ変更通知

Microsoft.Data.Sqlite には、SQLite のデータ変更通知を公開する API がありません。 この機能に関するフィードバックを送信するには、問題 [#13827](https://github.com/dotnet/efcore/issues/13827) を使用してください。

## <a name="virtual-table-modules"></a>仮想テーブル モジュール

Microsoft Data Sqlite には、仮想テーブル モジュールを作成するための API がありません。 この機能に関するフィードバックを送信するには、問題 [#13823](https://github.com/dotnet/efcore/issues/13823) を使用してください。

## <a name="see-also"></a>関連項目

* [データ型](types.md)
* [接続文字列](connection-strings.md)
* [暗号化](encryption.md)
* [ADO.NET の制限事項](adonet-limitations.md)
* [Dapper の制限事項](dapper-limitations.md)
