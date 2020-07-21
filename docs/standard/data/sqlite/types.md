---
title: データの種類
ms.date: 12/13/2019
description: サポートされているデータ型と、それらに関する制限事項について説明します。
ms.openlocfilehash: a11ff382f80cd979506d6195c299c8234c3eb8ea
ms.sourcegitcommit: c91110ef6ee3fedb591f3d628dc17739c4a7071e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/15/2020
ms.locfileid: "81389037"
---
# <a name="data-types"></a>データの種類

SQLite には、INTEGER、REAL、TEXT、BLOB の 4 つのプリミティブ データ型のみが存在します。 データベースの値が `object` として返される API では、この 4 つの型のいずれかのみが返されます。 Microsoft.Data.Sqlite では他の .NET 型がサポートされていますが、最終的には、それらの型と 4 つのいずれかのプリミティブ型との間で値が強制的に変換されます。

| .NET           | SQLite  | Remarks                                                       |
| -------------- | ------- | ------------------------------------------------------------- |
| ブール型        | INTEGER | `0` または `1`                                                    |
| Byte           | INTEGER |                                                               |
| Byte[]         | BLOB    |                                                               |
| Char           | TEXT    | UTF-8                                                         |
| DateTime       | TEXT    | yyyy-MM-dd HH:mm:ss.FFFFFFF                                   |
| DateTimeOffset | TEXT    | yyyy-MM-dd HH:mm:ss.FFFFFFFzzz                                |
| Decimal (10 進数型)        | TEXT    | `0.0###########################` 形式。 REAL は情報の損失を伴います。 |
| Double         | real    |                                                               |
| GUID           | TEXT    | 00000000-0000-0000-0000-000000000000                          |
| Int16          | INTEGER |                                                               |
| Int32          | INTEGER |                                                               |
| Int64          | INTEGER |                                                               |
| SByte          | INTEGER |                                                               |
| Single         | real    |                                                               |
| String         | TEXT    | UTF-8                                                         |
| TimeSpan       | TEXT    | d.hh:mm:ss.fffffff                                            |
| UInt16         | INTEGER |                                                               |
| UInt32         | INTEGER |                                                               |
| UInt64         | INTEGER | 大きな値のオーバーフロー                                         |

## <a name="alternative-types"></a>代替型

一部の .NET 型は、代替の SQLite 型から読み取ることができます。 これらの代替型を使用するようにパラメーターを構成することもできます。 詳しくは、「[パラメーター](parameters.md#alternative-types)」をご覧ください。

| .NET           | SQLite  | Remarks          |
| -------------- | ------- | ---------------- |
| Char           | INTEGER | UTF-16           |
| DateTime       | real    | ユリウス日の値 |
| DateTimeOffset | real    | ユリウス日の値 |
| GUID           | BLOB    |                  |
| TimeSpan       | real    | 日数          |

たとえば、次のクエリでは、結果セット内の REAL 列から TimeSpan 値が読み取られます。

[!code-csharp[](../../../../samples/snippets/standard/data/sqlite/DateAndTimeSample/Program.cs?name=snippet_AlternativeType)]

## <a name="column-types"></a>列の型

SQLite では、動的な型システムが使用されており、値の型がその格納先の列ではなく値自体に関連付けられています。 列の型名には任意の名前を使用できます。 Microsoft.Data.Sqlite ではそれらの名前に追加のセマンティクスは適用されません。

列の型名は、[型のアフィニティ](https://www.sqlite.org/datatype3.html#type_affinity)に影響します。 一般的な注意事項として、列の型 STRING を使用すると、値に対して INTEGER または REAL への変換が試みられ、予期しない結果を招く可能性があります。 INTEGER、REAL、TEXT、BLOB の 4 つのプリミティブ SQLite 型名だけを使用することをお勧めします。

SQLite では、長さ、有効桁数、小数点以下桁数などの型のファセットを指定できますが、これらはデータベース エンジンによって適用されません。 これらは使用しているアプリによって適用されます。

## <a name="see-also"></a>関連項目

- [SQLite のデータ型](https://www.sqlite.org/datatype3.html)
