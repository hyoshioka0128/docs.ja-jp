---
title: 挿入、更新、および削除の各操作
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 26a43a4f-83c9-4732-806d-bb23aad0ff6b
ms.openlocfilehash: fac89f905b85493bc0ec36a85635f369bb354266
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2019
ms.locfileid: "70793057"
---
# <a name="insert-update-and-delete-operations"></a>挿入、更新、および削除の各操作

オブジェクト モデルに対してオブジェクトの追加、変更、および削除を行うには、`Insert` で `Update`、`Delete`、および [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] の各操作を実行します。 既定では、[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] によって SQL に対する操作が変換され、変更内容がデータベースに送信されます。

[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] では、オブジェクトに対して行った変更内容の操作と維持に関して、最大限の柔軟性が提供されます。 クエリによって取得するか新規に作成することによりエンティティ オブジェクトが使用可能になった後で、通常のオブジェクトと同じようにそれらのオブジェクトをアプリケーションで変更できます。 つまり、それらに対して、値の変更、コレクションへの追加、およびコレクションからの削除を行うことができます。 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] では変更履歴が保持されるため、<xref:System.Data.Linq.DataContext.SubmitChanges%2A> を呼び出すと、変更内容をデータベースに送信できます。

> [!NOTE]
> [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] は連鎖削除操作をサポートせず、認識もしません。 制約を持つテーブルの行を削除するには、データベース内の外部キー制約で `ON DELETE CASCADE` 規則を設定するか、独自のコードを使用して、親オブジェクトの削除を妨げる子オブジェクトを最初に削除する必要があります。 それ以外の場合は、例外がスローされます。 詳細については、[行をデータベースから削除する](how-to-delete-rows-from-the-database.md)」を参照してください。

次の例では、Northwind サンプル データベースの `Customer` クラスと `Order` クラスを使用します。 簡潔にするため、ここではクラス定義を省いています。

[!code-csharp[DLinqCRUDOps#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqCRUDOps/cs/Program.cs#1)]
[!code-vb[DLinqCRUDOps#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqCRUDOps/vb/Module1.vb#1)]

<xref:System.Data.Linq.DataContext.SubmitChanges%2A> を呼び出すと、変更内容をデータベースに送信する SQL コマンドが [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] によって自動的に生成され、実行されます。

> [!NOTE]
> 独自に作成したロジック (通常はストアド プロシージャ) を使用して、この動作をオーバーライドできます。 詳細については、「[既定の動作をオーバーライドするときの開発者の責任](responsibilities-of-the-developer-in-overriding-default-behavior.md)」を参照してください。
>
> Visual Studio を使用している開発者は、オブジェクト リレーショナル デザイナーを使用して、この目的のストアド プロシージャを開発できます。

## <a name="see-also"></a>関連項目

- [サンプル データベースのダウンロード](downloading-sample-databases.md)
- [挿入、更新、および削除の各操作のカスタマイズ](customizing-insert-update-and-delete-operations.md)
