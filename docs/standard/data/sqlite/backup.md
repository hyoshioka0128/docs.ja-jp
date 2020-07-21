---
title: オンライン バックアップ
ms.date: 12/13/2019
description: SQLite のオンライン バックアップ機能を使用する方法について説明します。
ms.openlocfilehash: d857dcb69f2b2d10b034a0abf222b30c2e20bb41
ms.sourcegitcommit: 7088f87e9a7da144266135f4b2397e611cf0a228
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/11/2020
ms.locfileid: "75901283"
---
# <a name="online-backup"></a>オンライン バックアップ

SQLite では、アプリの実行中にデータベース ファイルをバックアップできます。 この機能は、Microsoft.Data.Sqlite で `SqliteConnection` の <xref:Microsoft.Data.Sqlite.SqliteConnection.BackupDatabase%2A> メソッドとして用意されています。

[!code-csharp[](../../../../samples/snippets/standard/data/sqlite/BackupSample/Program.cs?name=snippet_Backup)]

現時点では、`BackupDatabase` を使用すると、データベースができるだけ迅速にバックアップされ、他の接続によってそのデータベースへの書き込みが行われないようになります。 問題 [#13834](https://github.com/dotnet/efcore/issues/13834) では、バックグラウンドでデータベースをバックアップするための代替 API が提供され、他の接続によってバックアップを中断し、データベースに書き込むことができます。 関心がある場合は、この問題に関するフィードバックをお寄せください。
