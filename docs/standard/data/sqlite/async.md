---
title: 非同期の制限事項
ms.date: 12/13/2019
description: 非同期 API の制限事項と、代わりに使用できるいくつかの代替手段について説明します。
ms.openlocfilehash: 350237dc5c03023f60e9680e8b9c94aabb62606f
ms.sourcegitcommit: 30a558d23e3ac5a52071121a52c305c85fe15726
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/25/2019
ms.locfileid: "75450334"
---
# <a name="async-limitations"></a>非同期の制限事項

SQLite では非同期 I/O はサポートされません。 非同期 ADO.NET メソッドは、Microsoft.Data.Sqlite では同期的に実行されます。 これらを呼び出すのは避けてください。

代わりに[先行書き込みログ](https://www.sqlite.org/wal.html)を使用して、パフォーマンスとコンカレンシーを向上させます。

[!code-csharp[](../../../../samples/snippets/standard/data/sqlite/AsyncSample/Program.cs?name=snippet_WAL)]

> [!TIP]
> [Entity Framework Core](/ef/core/) を使用して作成されたデータベースでは、先行書き込みログが既定で有効になっています。
