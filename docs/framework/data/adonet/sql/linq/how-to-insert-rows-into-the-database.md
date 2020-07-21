---
title: '方法: 行をデータベースに挿入する'
description: テーブルに関連付けられたコレクションに LINQ to SQL オブジェクトを追加することによって、データベース内に行を挿入する方法について説明します。 LINQ to SQL は、追加内容を SQL INSERT コマンドに変換します。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 44d99680-69c7-4879-a732-f6771b334211
ms.openlocfilehash: 39eee6edf59d2adb7de41efd88899050fbe69fd8
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84286353"
---
# <a name="how-to-insert-rows-into-the-database"></a>方法: 行をデータベースに挿入する

関連付けられた [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] の <xref:System.Data.Linq.Table%601> コレクションにオブジェクトを追加し、その変更内容をデータベースに送信することで、データベースに行を挿入できます。 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] によって、変更内容が SQL の `INSERT` コマンドに適切に変換されます。

> [!NOTE]
> [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] の `Insert`、`Update`、および `Delete` の既定のデータベース操作メソッドはオーバーライドできます。 詳細については、「[挿入、更新、および削除の各操作のカスタマイズ](customizing-insert-update-and-delete-operations.md)」を参照してください。
>
> Visual Studio を使用している開発者は、オブジェクト リレーショナル デザイナーを使用して、同じ用途のストアド プロシージャを開発できます。

以下の手順では、有効な <xref:System.Data.Linq.DataContext> で Northwind データベースに接続されるものと想定しています。 詳細については、[データベースに接続する](how-to-connect-to-a-database.md)」を参照してください。

### <a name="to-insert-a-row-into-the-database"></a>行をデータベースに挿入するには

1. 送信する列データを含む新しいオブジェクトを作成します。

2. データベース内の挿入先テーブルに関連付けられた [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] の `Table` コレクションに新しいオブジェクトを追加します。

3. データベースに変更内容を送信します。

## <a name="example"></a>例

次のサンプル コードでは、`Order` 型の新しいオブジェクトを作成し、適切な値をこのオブジェクトに設定します。 その後で、新しいオブジェクトを `Order` コレクションに追加します。 最後にこの変更内容を `Orders` テーブルの新しい行としてデータベースに送信します。

[!code-csharp[System.Data.Linq.Table#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/system.data.linq.table/cs/program.cs#1)]
[!code-vb[System.Data.Linq.Table#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/system.data.linq.table/vb/module1.vb#1)]

## <a name="see-also"></a>関連項目

- [方法: 変更の競合を管理する](how-to-manage-change-conflicts.md)
- [DataContext メソッド (O/R デザイナー)](/visualstudio/data-tools/datacontext-methods-o-r-designer)
- [方法: 更新、挿入、および削除を実行するストアド プロシージャを割り当てる (O/R デザイナー)](/visualstudio/data-tools/how-to-assign-stored-procedures-to-perform-updates-inserts-and-deletes-o-r-designer)
- [データの変更と変更の送信](making-and-submitting-data-changes.md)
