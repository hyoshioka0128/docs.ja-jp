---
ms.openlocfilehash: 23ba6064a283b47312a66f3636c2834a7d58106e
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85620187"
---
### <a name="adonet-now-attempts-to-automatically-reconnect-broken-sql-connections"></a>ADO.NET では、切断された SQL 接続の再接続が自動的に試行されるようになりました

#### <a name="details"></a>説明

.NET Framework 4.5.1 以降、.NET Framework では、切断された SQL 接続の再接続が自動的に試行されます。 通常、これはアプリの安定性を高めますが、再接続時に行動できるよう、接続が失われたことをアプリに認識させる必要があるという極端な状況があります。

#### <a name="suggestion"></a>提案される解決策

互換性の問題からこの機能が望ましくない場合、接続文字列 (または <xref:System.Data.SqlClient.SqlConnectionStringBuilder?displayProperty=fullName>) の <xref:System.Data.SqlClient.SqlConnectionStringBuilder.ConnectRetryCount?displayProperty=fullName> プロパティを 0 に設定することで無効にできます。

| 名前    | [値]       |
|:--------|:------------|
| スコープ   |エッジ|
|バージョン|4.5.1|
|種類|ランタイム

#### <a name="affected-apis"></a>影響を受ける API

-<xref:System.Data.IDbConnection.ConnectionString?displayProperty=nameWithType></li><li><xref:System.Data.SqlClient.SqlConnection.ConnectionString?displayProperty=nameWithType></li><li><xref:System.Configuration.ConnectionStringSettings.ConnectionString?displayProperty=nameWithType></li><li><xref:System.Data.Common.DbConnection.ConnectionString?displayProperty=nameWithType></li><li><xref:System.Data.Common.DbConnectionStringBuilder.ConnectionString?displayProperty=nameWithType></li><li><xref:System.Data.SqlClient.SqlConnectionStringBuilder.%23ctor></li><li><xref:System.Data.SqlClient.SqlConnectionStringBuilder.%23ctor(System.String)></li><li><xref:System.Data.Common.DbConnectionStringBuilder.%23ctor></li><li><xref:System.Data.Common.DbConnectionStringBuilder.%23ctor(System.Boolean)></li></ul>|
