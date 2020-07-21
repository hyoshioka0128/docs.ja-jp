---
ms.openlocfilehash: 809ca85b347fabc44573e2e0c5a43261d68590d3
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85621248"
---
### <a name="workflow-sql-persistence-adds-primary-key-clusters-and-disallows-null-values-in-some-columns"></a>Workflow SQL の永続化で主キー クラスターが追加され、一部の列の null 値が許可されない

#### <a name="details"></a>説明

.NET Framework 4.7 以降では、SqlWorkflowInstanceStoreSchema.sql スクリプトで SQL Workflow Instance Store (SWIS) に作成されたテーブルにはクラスター化された主キーが使用されます。 そのため、ID では <code>null</code> 値はサポートされません。 SWIS の操作には、この変更による影響はありません。 SQL Server トランザクション レプリケーションをサポートするように更新されました。

#### <a name="suggestion"></a>提案される解決策

この変更では、SQL ファイルの SqlWorkflowInstanceStoreSchemaUpgrade.sql を既存のインストールに適用する必要があります。 新しいデータベースのインストールは自動的に変更されます。

| 名前    | 値       |
|:--------|:------------|
| スコープ   |エッジ|
|バージョン|4.7|
|種類|ランタイム|
