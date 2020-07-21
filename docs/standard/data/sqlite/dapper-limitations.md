---
title: Dapper の制限事項
ms.date: 12/13/2019
description: Dapper の使用時に生じる制限事項について説明します。
ms.openlocfilehash: 396507f25f591a9ab5c3bb07c0af6fd8d175e4ea
ms.sourcegitcommit: 7088f87e9a7da144266135f4b2397e611cf0a228
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/11/2020
ms.locfileid: "75901208"
---
# <a name="dapper-limitations"></a>Dapper の制限事項

Microsoft.Data.Sqlite を [Dapper](https://stackexchange.github.io/Dapper/) とともに使用する場合に、知っておく必要がある制限事項がいくつか存在します。

## <a name="parameters"></a>パラメーター

SQLite パラメーター名では大文字と小文字が区別されます。 SQL で使用されるパラメーター名と匿名オブジェクトのプロパティで、大文字と小文字が一致していることを確認してください。 問題 [#18861](https://github.com/dotnet/efcore/issues/18861) が、この動作の改善について取り上げています。

Dapper では、パラメーターに `@` プレフィックスを使用する必要もあります。 他のプレフィックスは機能しません。

[!code-csharp[](../../../../samples/snippets/standard/data/sqlite/DapperSample/Program.cs?name=snippet_Parameter)]

## <a name="data-types"></a>データの種類

Dapper では、SqliteDataReader インデクサーを使用して値が読み取られます。 このインデクサーの戻り値の型は object です。つまり、long、double、string、または byte [] の値のみが返されます。 詳細については、「[データ型](types.md)」を参照してください。 これらの型と他のプリミティブ型との間の変換は、ほとんどが Dapper によって処理されます。 ただし、`DateTimeOffset`、`Guid`、`TimeSpan` は処理されません。 これらの型を結果で使用する場合は、型ハンドラーを作成してください。

[!code-csharp[](../../../../samples/snippets/standard/data/sqlite/DapperSample/Program.cs?name=snippet_TypeHandlers)]

この型ハンドラーは、クエリを実行する前に忘れずに追加してください。

[!code-csharp[](../../../../samples/snippets/standard/data/sqlite/DapperSample/Program.cs?name=snippet_AddTypeHandlers)]

## <a name="see-also"></a>関連項目

* [データ型](types.md)
* [非同期の制限事項](async.md)
