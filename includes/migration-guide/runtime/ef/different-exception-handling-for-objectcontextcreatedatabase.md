---
ms.openlocfilehash: 687118157020ede200f97a0125c4740a06bf4b5e
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85620305"
---
### <a name="different-exception-handling-for-objectcontextcreatedatabase-and-dbproviderservicescreatedatabase-methods"></a>ObjectContext.CreateDatabase メソッドと DbProviderServices.CreateDatabase メソッドで異なる例外処理

#### <a name="details"></a>説明

.NET Framework 4.5 から、データベースの作成が失敗した場合、<code>CreateDatabase</code> メソッドは、空のデータベースの削除を試みます。 その操作が成功した場合、元の <xref:System.Data.SqlClient.SqlException?displayProperty=fullName> は伝播されます (.NET Framework 4.0 で常にスローされていた <xref:System.InvalidOperationException?displayProperty=fullName> の代わりに)

#### <a name="suggestion"></a>提案される解決策

<xref:System.Data.Objects.ObjectContext.CreateDatabase> または <xref:System.Data.Common.DbProviderServices.CreateDatabase(System.Data.Common.DbConnection,System.Nullable{System.Int32},System.Data.Metadata.Edm.StoreItemCollection)> の実行中に <xref:System.InvalidOperationException?displayProperty=fullName> をキャッチするときには、SQLExceptions もキャッチする必要があります。

| 名前    | [値]       |
|:--------|:------------|
| スコープ   |マイナー|
|バージョン|4.5|
|種類|ランタイム

#### <a name="affected-apis"></a>影響を受ける API

-<xref:System.Data.Objects.ObjectContext.CreateDatabase?displayProperty=nameWithType></li><li><xref:System.Data.Common.DbProviderServices.CreateDatabase(System.Data.Common.DbConnection,System.Nullable{System.Int32},System.Data.Metadata.Edm.StoreItemCollection)?displayProperty=nameWithType></li></ul>|
