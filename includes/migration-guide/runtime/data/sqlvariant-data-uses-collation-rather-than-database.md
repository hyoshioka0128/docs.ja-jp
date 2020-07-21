---
ms.openlocfilehash: d606fbc4048421bc572cfe3db2e06bbcd4529e25
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85620290"
---
### <a name="sql_variant-data-uses-sql_variant-collation-rather-than-database-collation"></a>sql_variant データはデータベースの照合順序ではなく、sql_variant の照合順序を使用する

#### <a name="details"></a>説明

<code>sql_variant</code> データはデータベースの照合順序ではなく <code>sql_variant</code> の照合順序を使用します。

#### <a name="suggestion"></a>提案される解決策

この変更により、データベースの照合順序が <code>sql_variant</code> の照合順序と異なる場合にデータ破損が生じる可能性に対応できます。 破損したデータに依存するアプリケーションでは、エラーが発生する場合があります。

| 名前    | [値]       |
|:--------|:------------|
| スコープ   |透明|
|バージョン|4.5|
|種類|ランタイム|
