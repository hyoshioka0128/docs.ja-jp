---
title: データの変更と変更の送信
ms.date: 03/30/2017
ms.assetid: d68c2dc3-99b3-49ab-b547-2ca5b386429a
ms.openlocfilehash: 18468c9a2018a28e85d87155d98b0853854013fd
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2019
ms.locfileid: "70792971"
---
# <a name="making-and-submitting-data-changes"></a>データの変更と変更の送信

このセクションのトピックでは、データベースを変更し、その変更を送信する方法と、オプティミスティック コンカレンシーの競合を処理する方法について説明します。

> [!NOTE]
> [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] の `Insert`、`Update`、および `Delete` の既定のデータベース操作メソッドはオーバーライドできます。 詳細については、「[挿入、更新、および削除の各操作のカスタマイズ](customizing-insert-update-and-delete-operations.md)」を参照してください。
>
> Visual Studio を使用している開発者は、オブジェクト リレーショナル デザイナーを使用して、同じ用途のストアド プロシージャを開発できます。

## <a name="in-this-section"></a>このセクションの内容

[方法: 行をデータベースに挿入する](how-to-insert-rows-into-the-database.md) \
オブジェクト モデルにオブジェクトを追加することにより、データベースに行を挿入する方法について説明します。

[方法: データベースの行を更新する](how-to-update-rows-in-the-database.md) \
オブジェクト モデルのオブジェクトを更新することにより、データベースの行を更新する方法について説明します。

[方法: 行をデータベースから削除する](how-to-delete-rows-from-the-database.md) \
オブジェクト モデルのオブジェクトを削除することにより、データベースの行を削除する方法について説明します。

[方法: データベースに変更内容を送信する](how-to-submit-changes-to-the-database.md) \
オブジェクト モデルに対する変更をデータベースに送信する方法について説明します。

[方法: データ送信をトランザクションで囲む](how-to-bracket-data-submissions-by-using-transactions.md) \
トランザクションに操作を含める方法について説明します。

[方法: データベースを動的に作成する](how-to-dynamically-create-a-database.md) \
動的にデータベースを生成する方法と、この方法を使用する一般的なシナリオについて説明します。

[方法: 変更の競合を管理する](how-to-manage-change-conflicts.md) \
オプティミスティック コンカレンシーの問題に対処する方法について説明します。
