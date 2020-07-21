---
title: SQL Server での複数データベースにまたがるアクセスの有効化
ms.date: 03/30/2017
ms.assetid: 10663fb6-434c-4c81-8178-ec894b9cf895
ms.openlocfilehash: bf46d43f5ac9b0a385e9bc6da1546af1d67a282d
ms.sourcegitcommit: ad800f019ac976cb669e635fb0ea49db740e6890
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/29/2019
ms.locfileid: "73040245"
---
# <a name="enabling-cross-database-access-in-sql-server"></a>SQL Server での複数データベースにまたがるアクセスの有効化
複数データベースの組み合わせ所有権は、あるデータベースのプロシージャが、別のデータベースのオブジェクトに依存している場合に作用します。 複数データベースの組み合わせ所有権は、単一データベースの組み合わせ所有権とほぼ同じように機能しますが、所有権の連鎖性を保つために、すべてのオブジェクトの所有者が同じログイン アカウントにマップされていることが必要です。 ソース データベース内のソース オブジェクトおよびターゲット データベース内のターゲット オブジェクトが同じログイン アカウントによって所有されている場合、ターゲット オブジェクトに対する権限は SQL Server によってチェックされません。  
  
## <a name="off-by-default"></a>既定で無効の機能  
 複数データベースにまたがる組み合わせ所有権は、既定では無効になっています。 次に示したように、複数データベースの組み合わせ所有権はセキュリティ上のリスクを伴うため無効にすることをお勧めします。  
  
- `db_ddladmin` データベース ロールまたは `db_owners` データベース ロールのデータベース所有者およびメンバーは、他のユーザーによって所有されたオブジェクトを作成できます。 これらのオブジェクトが、他のデータベースのオブジェクトに依存している可能性もあります。 これは、複数データベースの組み合わせ所有権を有効にした場合、すべてのデータベースのデータについて、これらのユーザーを完全に信頼する必要があることを意味します。  
  
- CREATE DATABASE 権限を持つユーザーは、新しいデータベースを作成したり、既存のデータベースをアタッチしたりできます。 複数データベースの組み合わせ所有権を有効にした場合、これらのユーザーが、新たに作成したデータベースから (または、アタッチしたデータベースから)、権限を持たない他のデータベース内のオブジェクトにアクセスできます。  
  
## <a name="enabling-cross-database-ownership-chaining"></a>複数データベースの組み合わせ所有権の有効化  
 高い権限が与えられたユーザーを完全に信頼できる環境であれば、複数データベースの組み合わせ所有権を有効にすることができます。 複数データベースの組み合わせ所有権は、セットアップ時にすべてのデータベースを対象に構成できるほか、Transact-SQL コマンドの `sp_configure` および `ALTER DATABASE` を使用することで、特定のデータベースを対象に構成することもできます。  
  
 複数データベースの組み合わせ所有権を個別に構成するには、`sp_configure` を使用し、サーバーに対してこの機能を無効にします。 次に、ALTER DATABASE コマンドで SET DB_CHAINING ON を指定し、必要なデータベースに対してのみ、複数データベースの組み合わせ所有権を構成します。  
  
 次のサンプルでは、すべてのデータベースに対して複数データベースの組み合わせ所有権を有効にします。  
  
```sql
EXECUTE sp_configure 'show advanced', 1;  
RECONFIGURE;  
EXECUTE sp_configure 'cross db ownership chaining', 1;  
RECONFIGURE;  
```  
  
 次のサンプルでは、特定のデータベースに対して複数データベースの組み合わせ所有権を有効にします。  
  
```sql
ALTER DATABASE Database1 SET DB_CHAINING ON;  
ALTER DATABASE Database2 SET DB_CHAINING ON;  
```  
  
### <a name="dynamic-sql"></a>動的 SQL  
 動的に生成された SQL ステートメントの実行では、同じユーザーが両方のデータベースに存在しない限り、複数データベースの組み合わせ所有権は機能しません。 SQL Server では、別のデータベースのデータにアクセスするストアド プロシージャを作成し、両方のデータベースに存在する証明書でそのプロシージャに署名することによって、この制限を回避できます。 これにより、ユーザーは、データベースへのアクセス許可が付与されていなくても、そのプロシージャによって使用されるデータベース リソースにアクセスできるようになります。  
  
## <a name="external-resources"></a>外部リソース  
 詳細については、次のリソースを参照してください。  
  
|リソース|説明|  
|--------------|-----------------|  
|「[EXECUTE AS の使用によるデータベースの権限借用の拡張](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/ms188304(v=sql.105))」および「[cross db ownership chaining サーバー構成オプション](/sql/database-engine/configure-windows/cross-db-ownership-chaining-server-configuration-option)」。|SQL Server のインスタンスに対して、複数データベースの組み合わせ所有権を構成する方法が説明されています。|  
  
## <a name="see-also"></a>関連項目

- [ADO.NET アプリケーションのセキュリティ保護](../securing-ado-net-applications.md)
- [SQL Server セキュリティの概要](overview-of-sql-server-security.md)
- [SQL Server でのストアド プロシージャを使用したアクセス許可の管理](managing-permissions-with-stored-procedures-in-sql-server.md)
- [SQL Server での安全な動的 SQL の作成](writing-secure-dynamic-sql-in-sql-server.md)
- [SQL Server でのストアド プロシージャの署名](signing-stored-procedures-in-sql-server.md)
- [ADO.NET の概要](../ado-net-overview.md)
