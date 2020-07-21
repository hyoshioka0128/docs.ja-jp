---
title: トランザクション
ms.date: 12/13/2019
description: トランザクションの使用方法について説明します。
ms.openlocfilehash: 4b72a1573a560ffd1bfd0f54d46ab3b135280976
ms.sourcegitcommit: 30a558d23e3ac5a52071121a52c305c85fe15726
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/25/2019
ms.locfileid: "75450382"
---
# <a name="transactions"></a>トランザクション

トランザクションを使用すると、複数の SQL ステートメントを 1 つの作業単位にまとめて、1 つのアトミック単位としてデータベースにコミットできます。 トランザクション内のいずれかのステートメントが失敗した場合は、前のステートメントによって行われた変更をロールバックできます。 トランザクションが開始されたときのデータベースの初期状態は保持されます。 トランザクションを使用すると、データベースに多数の変更を一度に加えるときの SQLite でのパフォーマンスを向上させることもできます。

## <a name="concurrency"></a>コンカレンシー

SQLite では、一度に 1 つのトランザクションだけがデータベース内で変更を保留にすることができます。 このため、別のトランザクションの完了に時間がかかりすぎると、<xref:Microsoft.Data.Sqlite.SqliteCommand> の <xref:Microsoft.Data.Sqlite.SqliteConnection.BeginTransaction%2A> メソッドと `Execute` メソッドの呼び出しがタイムアウトになる場合があります。

ロック、再試行、タイムアウトの詳細については、「[データベース エラー](database-errors.md)」を参照してください。

## <a name="isolation-levels"></a>分離レベル

SQLite では、トランザクションは既定で **serializable** です。 この分離レベルを使用すると、トランザクション内で行われたすべての変更が完全に分離されることが保証されます。 トランザクションの外部で実行される他のステートメントは、そのトランザクションの変更の影響を受けません。

SQLite では、共有キャッシュの使用時には、**read uncommitted** もサポートされます。 このレベルでは、ダーティ リード、反復不能読み取り、ファントムが可能です。

- "*ダーティ リード*" は、1 つのトランザクション内で保留中の変更がそのトランザクションの外部でクエリによって返される一方で、そのトランザクション内の変更がロールバックされるときに生じます。 結果には、実際にはデータベースにコミットされなかったデータが含まれます。

- "*反復不能読み取り*" は、トランザクションで同じ行に 2 回クエリが実行され、一方、、その 2 回のクエリの間に別のトランザクションによってその行が変更されたことが原因で、結果が異なっているときに生じます。

- "*ファントム*" は、トランザクション中にクエリの where 句に合わせて変更または追加された行です。 同じクエリが同じトランザクション内で 2 回実行されることが許可されている場合、そのようなクエリで異なる行が返されることがあります。

Microsoft.Data.Sqlite では、<xref:Microsoft.Data.Sqlite.SqliteConnection.BeginTransaction%2A> に渡される IsolationLevel は最小レベルとして扱われます。 実際の分離レベルは、read uncommitted または serializable に昇格されます。

次のコードは、ダーティ リードをシミュレートしています。 接続文字列には `Cache=Shared` を含める必要があるので注意してください。

[!code-csharp[](../../../../samples/snippets/standard/data/sqlite/DirtyReadSample/Program.cs?name=snippet_DirtyRead)]
