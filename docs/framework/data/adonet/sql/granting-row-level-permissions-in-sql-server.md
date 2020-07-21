---
title: SQL Server における行レベルの権限の付与
ms.date: 03/30/2017
ms.assetid: a55aaa12-34ab-41cd-9dec-fd255b29258c
ms.openlocfilehash: df5fcb4a6c73e12bec2ab17501fdfb02cf672324
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2019
ms.locfileid: "70782354"
---
# <a name="granting-row-level-permissions-in-sql-server"></a>SQL Server における行レベルの権限の付与

権限を単に付与、取り消し、拒否するよりも細かなレベルで、データに対するアクセスを制御することが必要な場合があります。 たとえば、医療施設のデータベース アプリケーションでは、各医師がアクセスできるのは、自分が担当している患者の情報のみに制限する必要があります。 同様の要件は、金融機関、司法機関、政府機関、軍事機関のアプリケーションなど、さまざまな環境で考えられます。 こうしたシナリオに対処するため SQL Server 2016 には、 [行レベルのセキュリティ](/sql/relational-databases/security/row-level-security) 機能が備わっています。この機能は、セキュリティ ポリシーにおける行レベルのアクセス ロジックを簡略化および一元化します。 従来の SQL Server バージョンでは、同様の機能は行レベルのフィルター処理を行うビューを使用して実現できます。

## <a name="implementing-row-level-filtering"></a>行レベルのフィルター処理の実装

行レベルのフィルター処理は、前述の病院の例などのように、1 つのテーブルに情報を格納するアプリケーションで使用されます。 行レベルのフィルター処理を実装するため、それぞれの行には、ユーザー名、ラベル、識別子など、区別するパラメーターを定義する列があります。 対象テーブルでセキュリティ ポリシーまたはビューを作成し、ユーザーがアクセスできる行をフィルター処理します。 その後、パラメーター化されたストアド プロシージャを作成し、ユーザーが実行できるクエリの種類を制御します。

次の例は、ユーザー名またはログイン名に基づいて行レベルのフィルター処理を構成する方法を示しています。

- テーブルを作成し、名前を格納するための列を追加します。

- 行レベルのフィルター処理を以下のように有効にします。

  - SQL Server 2016 以降または [Azure SQL Database](https://docs.microsoft.com/azure/sql-database/)を使用している場合は、表に関する述語を追加するセキュリティー ポリシーを作成します。このセキュリティー・ポリシーは、現在のデータベース ユーザー (CURRENT_USER() 組み込み関数を使用) または現在のログイン名 (SUSER_SNAME() 組み込み関数を使用) のいずれかに一致する行のみが返されるように制限します。

      ```sql
      CREATE SCHEMA Security
      GO

      CREATE FUNCTION Security.userAccessPredicate(@UserName sysname)
          RETURNS TABLE
          WITH SCHEMABINDING
      AS
          RETURN SELECT 1 AS accessResult
          WHERE @UserName = SUSER_SNAME()
      GO

      CREATE SECURITY POLICY Security.userAccessPolicy
          ADD FILTER PREDICATE Security.userAccessPredicate(UserName) ON dbo.MyTable,
          ADD BLOCK PREDICATE Security.userAccessPredicate(UserName) ON dbo.MyTable
      GO
      ```

  - SQL Server 2016 より前のバージョンを使用している場合、同様の機能はビューを使用して実現できます。

      ```sql
      CREATE VIEW vw_MyTable
      AS
          RETURN SELECT * FROM MyTable
          WHERE UserName = SUSER_SNAME()
      GO
      ```

- データを選択、挿入、更新、削除するストアド プロシージャを作成します。 フィルター処理を行うのにセキュリティ ポリシーを使用する場合には、ストアド プロシージャが基本テーブルでこれらの操作を直接実行する必要があります。フィルター処理がビューによって行われる場合、ストアド プロシージャがビューのためにビューに対して操作を行わなければなりません。 セキュリティ ポリシーまたはビューは、ユーザーのクエリによって返される行または変更された行を自動的にフィルター処理します。ストアド プロシージャは堅固なセキュリティ境界を設け、クエリに対して直接アクセスできるユーザーが、クエリを正常に実行し、フィルター対象データの存在を推論できてしまうという事態を回避します。

- データの挿入を行うストアド プロシージャの場合、セキュリティ ポリシーまたはビューで指定したのと同じ関数を使用してユーザー名を取得し、その値を UserName 列に挿入します。

- テーブル (該当する場合にはビューも) に設定されている `public` ロールの権限をすべて拒否します。 フィルター処理の述語には、ロールではなくユーザー名またはログイン名が使用されているため、ユーザーは、他のデータベース ロールから権限を継承することはできなくなります。

- データベース ロールにストアド プロシージャの EXECUTE 権限を付与します。 ユーザーは、提供されているストアド プロシージャを使ってのみ、データにアクセスできるようになります。

## <a name="see-also"></a>関連項目

- [行レベルのセキュリティ](/sql/relational-databases/security/row-level-security)
- [ADO.NET アプリケーションのセキュリティ保護](../securing-ado-net-applications.md)
- [SQL Server セキュリティの概要](overview-of-sql-server-security.md)
- [SQL Server におけるアプリケーション セキュリティのシナリオ](application-security-scenarios-in-sql-server.md)
- [SQL Server でのストアド プロシージャを使用したアクセス許可の管理](managing-permissions-with-stored-procedures-in-sql-server.md)
- [SQL Server での安全な動的 SQL の作成](writing-secure-dynamic-sql-in-sql-server.md)
- [ADO.NET の概要](../ado-net-overview.md)
