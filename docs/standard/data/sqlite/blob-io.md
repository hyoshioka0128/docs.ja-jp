---
title: BLOB の I/O
ms.date: 12/13/2019
description: SQLite の BLOB I/O 機能の使用方法について説明します。
ms.openlocfilehash: 0c133deacdc19684eca3a6724fb398dc01fda558
ms.sourcegitcommit: 30a558d23e3ac5a52071121a52c305c85fe15726
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/25/2019
ms.locfileid: "75450304"
---
# <a name="blob-io"></a>BLOB の I/O

データベースとの間でデータをストリーミングして、ラージ オブジェクトの読み取りと書き込み中のメモリ使用量を削減できます。 これは、データを解析または変換するときに特に有用です。

最初に、行を通常どおりに挿入します。 `zeroblob()` SQL 関数を使用して、ラージ オブジェクトを保持するデータベースの領域を割り当てます。 `last_insert_rowid()` 関数を使用すると、rowid を簡単に取得できます。

[!code-csharp[](../../../../samples/snippets/standard/data/sqlite/StreamingSample/Program.cs?name=snippet_Insert)]

行を挿入したら、<xref:Microsoft.Data.Sqlite.SqliteBlob> を使用してストリームを開き、ラージ オブジェクトを書き込みます。

[!code-csharp[](../../../../samples/snippets/standard/data/sqlite/StreamingSample/Program.cs?name=snippet_Write)]

データベースからラージ オブジェクトをストリーミングするには、ラージ オブジェクトの列のほか、ここに示すように、rowid またはその別名のいずれかを選択する必要があります。 rowid を選択しない場合、オブジェクト全体がメモリに読み込まれます。 正常に完了すると、`GetStream()` によって返されるオブジェクトは `SqliteBlob` になります。

[!code-csharp[](../../../../samples/snippets/standard/data/sqlite/StreamingSample/Program.cs?name=snippet_Read)]
