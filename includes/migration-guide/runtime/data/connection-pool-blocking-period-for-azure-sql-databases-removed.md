---
ms.openlocfilehash: d7a18a0b457c2a38f40c1da3b2f0bfc578259475
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85621176"
---
### <a name="connection-pool-blocking-period-for-azure-sql-databases-is-removed"></a>Azure SQL データベースの接続プールのブロック期間が削除される

#### <a name="details"></a>説明

.NET Framework 4.6.2 以降では、既知の Azure SQL データベースへの接続確立要求の場合 (\*.database.windows.net、\*.database.chinacloudapi.cn、\*.database.usgovcloudapi.net、\*.database.cloudapi.de)、接続プールのブロック期間が削除され、接続確立のエラーがキャッシュされません。 接続オープン要求の再試行は、一時的な接続エラーのほぼすぐ後に発生します。 この変更により、Azure SQL データベースへの接続確立がすぐに再試行するされるため、クラウド対応アプリケーションのパフォーマンスが向上します。 他のすべての接続を試みる場合は、接続プールのブロック期間が引き続き適用されます。<p/>.NET Framework 4.6.1 以前のバージョンでは、データベースへの接続時にアプリで一時的な接続エラーが発生した場合、接続はすぐに再試行されません。接続プールがエラーをキャッシュし、5 秒 ～ 1 分の間にエラーを再スローするためです。 詳しくは、「[SQL Server の接続プール (ADO.NET)](~/docs/framework/data/adonet/sql-server-connection-pooling.md)」をご覧ください。 この動作は、Azure SQL データベースへの接続時に問題となります。多くの場合、一時的なエラーが発生し、通常数秒内に回復します。 接続プールのブロック機能を使うと、データベースが使用可能で、アプリが数秒以内にレンダリングする必要がある場合でも、アプリは長期間データベースに接続できません。

#### <a name="suggestion"></a>提案される解決策

この動作が望ましくない場合は、.NET Framework 4.6.2 で導入された <xref:System.Data.SqlClient.SqlConnectionStringBuilder.PoolBlockingPeriod?displayProperty=fullName> プロパティを設定することで、接続プールのブロック期間を構成できます。 プロパティ値が <xref:System.Data.SqlClient.PoolBlockingPeriod?displayProperty=fullName> 列挙型のメンバーである場合、次の 3 つの値のいずれかを使用できます。<ul><li><xref:System.Data.SqlClient.PoolBlockingPeriod.AlwaysBlock></li><li><xref:System.Data.SqlClient.PoolBlockingPeriod.Auto></li><li><xref:System.Data.SqlClient.PoolBlockingPeriod.NeverBlock></li></ul><xref:System.Data.SqlClient.SqlConnectionStringBuilder.PoolBlockingPeriod?displayProperty=fullName> プロパティを <xref:System.Data.SqlClient.PoolBlockingPeriod.AlwaysBlock> に設定して、以前の動作を復元することができます。

| 名前    | 値       |
|:--------|:------------|
| スコープ   |マイナー|
|バージョン|4.6.2|
|種類|ランタイム

#### <a name="affected-apis"></a>影響を受ける API

-<xref:System.Data.Common.DbConnection.OpenAsync?displayProperty=nameWithType></li><li><xref:System.Data.SqlClient.SqlConnection.Open?displayProperty=nameWithType></li><li><xref:System.Data.SqlClient.SqlConnection.OpenAsync(System.Threading.CancellationToken)?displayProperty=nameWithType></li></ul>|
