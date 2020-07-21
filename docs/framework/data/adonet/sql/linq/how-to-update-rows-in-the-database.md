---
title: '方法: データベースの行を更新する'
description: テーブルに関連付けられたコレクションの LINQ to SQL オブジェクトを変更することによって、データベース内の行を更新する方法について説明します。 LINQ to SQL は、追加内容を SQL UPDATE コマンドに変換します。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: a2b5c90f-6cc3-4128-bfab-1db488d5af26
ms.openlocfilehash: f25efb91fb5a83fb1c7c109bd018c8210edaec8b
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84286340"
---
# <a name="how-to-update-rows-in-the-database"></a>方法: データベースの行を更新する

[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] の <xref:System.Data.Linq.Table%601> コレクションに関連付けられたオブジェクトのメンバーの値を変更し、その変更内容をデータベースに送信することで、データベースの行を更新できます。 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] によって、変更内容が SQL の `UPDATE` コマンドに適切に変換されます。

> [!NOTE]
> [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] の `Insert`、`Update`、および `Delete` の既定のデータベース操作メソッドはオーバーライドできます。 詳細については、「[挿入、更新、および削除の各操作のカスタマイズ](customizing-insert-update-and-delete-operations.md)」を参照してください。
>
> Visual Studio を使用している開発者は、オブジェクト リレーショナル デザイナーを使用して、同じ用途のストアド プロシージャを開発できます。

以下の手順では、有効な <xref:System.Data.Linq.DataContext> で Northwind データベースに接続されるものと想定しています。 詳細については、[データベースに接続する](how-to-connect-to-a-database.md)」を参照してください。

### <a name="to-update-a-row-in-the-database"></a>データベースの行を更新するには

1. データベースで更新する行をクエリします。

2. 結果として得られた [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] オブジェクトのメンバー値に、必要な変更を加えます。

3. データベースに変更内容を送信します。

## <a name="example"></a>例

次の例では、データベースの注文 #11000 をクエリし、結果として得られた `ShipName` オブジェクトの `ShipVia` と `Order` の値を変更します。 次に、これらのメンバー値の変更内容を、`ShipName` 列と `ShipVia` 列に対する変更としてデータベースに送信します。

[!code-csharp[System.Data.Linq.Table#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/system.data.linq.table/cs/program.cs#2)]
[!code-vb[System.Data.Linq.Table#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/system.data.linq.table/vb/module1.vb#2)]

## <a name="see-also"></a>関連項目

- [方法: 変更の競合を管理する](how-to-manage-change-conflicts.md)
- [方法: 更新、挿入、および削除を実行するストアド プロシージャを割り当てる (O/R デザイナー)](/visualstudio/data-tools/how-to-assign-stored-procedures-to-perform-updates-inserts-and-deletes-o-r-designer)
- [データの変更と変更の送信](making-and-submitting-data-changes.md)
