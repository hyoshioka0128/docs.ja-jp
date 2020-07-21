---
title: バッチ
ms.date: 12/13/2019
description: 1 つのコマンドで複数の SQL ステートメントをバッチで実行する方法について説明します。
ms.openlocfilehash: 0799784471520bb279db6a4b5879ad30945bdebb
ms.sourcegitcommit: 30a558d23e3ac5a52071121a52c305c85fe15726
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/25/2019
ms.locfileid: "75450310"
---
# <a name="batching"></a>バッチ

SQLite では、1 つのコマンドで複数の SQL ステートメントをまとめて実行するバッチ処理はネイティブではサポートされていません。 しかし、ネットワークは関与していないので、いずれにしても実際にパフォーマンスが向上することはありません。 ただし、Microsoft.Data.Sqlite では、他の ADO.NET プロバイダーと同様に動作するよう、便宜的にステートメントのバッチ処理が実装されています。

<xref:System.Data.Common.DbCommand.ExecuteReader%2A?displayProperty=nameWithType> を呼び出すと、ステートメントは、結果を返す最初のステートメントまで実行されます。 <xref:System.Data.Common.DbDataReader.NextResult%2A?displayProperty=nameWithType> を呼び出すと、結果を返す次のステートメントまで、またはバッチの終わりに達するまで、ステートメントの実行が続けられます。 <xref:System.Data.Common.DbDataReader.Dispose%2A?displayProperty=nameWithType> または <xref:System.Data.Common.DbDataReader.Close%2A> を呼び出すと、`NextResult()` によって使用されていない残りのステートメントがすべて実行されます。 データ リーダーを破棄しない場合、ファイナライザーによって残りのステートメントの実行が試みられますが、エラーが発生しても無視されます。 このため、バッチを使用するときは `DbDataReader` オブジェクトを破棄することが重要です。

[!code-csharp[](../../../../samples/snippets/standard/data/sqlite/BatchingSample/Program.cs?name=snippet_Batching)]

## <a name="see-also"></a>関連項目

* [一括挿入](bulk-insert.md)
