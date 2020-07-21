---
title: 新着記事
description: SqlClient データ プロバイダーや ADO.NET Entity Framework の新機能など、.NET Framework 4.5 の ADO.NET の新機能について説明します。
ms.date: 03/30/2017
ms.assetid: 3bb65d38-cce2-46f5-b979-e5c505e95e10
ms.openlocfilehash: 536b9314dd83366202f7fd9b489759681021fd9e
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84286172"
---
# <a name="whats-new-in-adonet"></a>ADO.NET の新機能

以下の機能は、.NET Framework 4.5 で ADO.NET に新しく追加されたものです。

## <a name="sqlclient-data-provider"></a>SqlClient Data Provider

.NET Framework 4.5 での .NET Framework Data Provider for SQL Server における新機能は次のとおりです。

- ConnectRetryCount と ConnectRetryInterval の接続文字列キーワード (<xref:System.Data.SqlClient.SqlConnection.ConnectionString%2A>) を使用すると、アイドル状態の接続の復元機能を制御できます。

- SQL Server からアプリケーションへのストリーミング サポートで、サーバー上のデータが構造化されていないシナリオがサポートされます。  詳しくは、「[SqlClient ストリーミング サポート](sqlclient-streaming-support.md)」をご覧ください。

- 非同期のプログラミングにサポートが追加されています。  詳しくは、「[非同期プログラミング](asynchronous-programming.md)」をご覧ください。

- 接続エラーは、拡張イベント ログに記録されるようになりました。 詳細については、「[ADO.NET のデータ追跡](data-tracing.md)」を参照してください。

- SqlClient では、SQL Server の高可用性、ディザスター リカバリー機能である AlwaysOn がサポートされるようになりました。 詳しくは、「[高可用性障害復旧のための SqlClient サポート](./sql/sqlclient-support-for-high-availability-disaster-recovery.md)」をご覧ください。

- SQL Server 認証を使用している場合は、<xref:System.Security.SecureString> としてパスワードを渡すことができます。 詳細については、「<xref:System.Data.SqlClient.SqlCredential>」を参照してください。

- `TrustServerCertificate` が false であり、`Encrypt` が true の場合は、SQL Server SSL 証明書のサーバー名 (または IP アドレス) が、接続文字列で指定されているサーバー名 (または IP アドレス) と正確に一致する必要があります。 それ以外の場合、接続試行は失敗します。 詳細については、「`Encrypt`」の <xref:System.Data.SqlClient.SqlConnection.ConnectionString%2A> 接続オプションの説明を参照してください。

  この変更によって既存のアプリケーションが接続しなくなる場合、次のいずれかを使用してアプリケーションを修正できます。

  - 共通名 (CN) またはサブジェクト代替名 (SAN) フィールドに短い名前を指定する証明書を発行します。 このソリューションは、データベース ミラーリングをする場合に有効です。

  - 短い名前を完全修飾ドメイン名にマップする別名を追加します。

  - 接続文字列では完全修飾ドメイン名を使用します。

- SqlClient は拡張保護をサポートしています。 拡張保護に関する詳細については、「[拡張保護を使用したデータベース エンジンへの接続](/sql/database-engine/configure-windows/connect-to-the-database-engine-using-extended-protection)」を参照してください。

- SqlClient は LocalDB データベースへの接続をサポートします。 詳しくは、「[SqlClient による LocalDB のサポート](./sql/sqlclient-support-for-localdb.md)」をご覧ください。

- `Type System Version=SQL Server 2012;` は、`Type System Version` 接続プロパティに渡す新しい値です。 `Type System Version=Latest;` 値は廃止されており、`Type System Version=SQL Server 2008;` と同等になっています。 詳細については、「<xref:System.Data.SqlClient.SqlConnection.ConnectionString%2A>」を参照してください。

- SqlClient は、スパース列に追加のサポートを提供します。このサポートは SQL Server 2008 で追加された機能です。 アプリケーションがスパース列を使用するテーブルのデータに既にアクセスしていると、パフォーマンスが向上します。 <xref:System.Data.SqlClient.SqlDataReader.GetSchemaTable%2A> の IsColumnSet 列は、列が列セットのメンバーであるスパース列であるかどうかを示します。 <xref:System.Data.SqlClient.SqlConnection.GetSchema%2A> では、列がスパース列であるかどうかが示されています (詳しくは「[SQL Server スキーマ コレクション](sql-server-schema-collections.md)」を参照)。 スパース列の詳細については、「[スパース列の使用](/sql/relational-databases/tables/use-sparse-columns)」を参照してください。

- 空間データ型を含むアセンブリ Microsoft.SqlServer.Types.dll は、Version 10.0 から Version 11.0 にアップグレードされました。 このアセンブリを参照するホスト アプリケーションでは、エラーが発生する可能性があります。 詳細については、「[データベース エンジン機能の重大な変更](https://docs.microsoft.com/previous-versions/sql/sql-server-2012/ms143179(v=sql.110))」を参照してください。

## <a name="adonet-entity-framework"></a>ADO.NET Entity Framework

.NET Framework 4.5 では、Entity Framework 5.0 を使用するときに新しいシナリオを有効にする API が追加されています。 Entity Framework 5.0 に追加された機能および機能強化に関する詳細については、「[新機能](https://docs.microsoft.com/previous-versions/gg696190(v=vs.103))」および [Entity Framework のリリースとバージョン管理](/ef/ef6/what-is-new/past-releases)に関する記事をご覧ください。

## <a name="see-also"></a>関連項目

- [ADO.NET](index.md)
- [ADO.NET の概要](ado-net-overview.md)
- [SQL Server と ADO.NET](./sql/index.md)
- [WCF Data Services 5.0 の新機能](https://docs.microsoft.com/previous-versions/dotnet/wcf-data-services/ee373845(v=vs.103))
