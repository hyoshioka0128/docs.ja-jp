---
title: SQL Server での借用を使用した権限のカスタマイズ
ms.date: 03/30/2017
ms.assetid: dc733d09-1d6d-4af0-9c4b-8d24504860f1
ms.openlocfilehash: 0d5e62019ae8806a7a182919fa06819a08d01301
ms.sourcegitcommit: ad800f019ac976cb669e635fb0ea49db740e6890
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/29/2019
ms.locfileid: "73040445"
---
# <a name="customizing-permissions-with-impersonation-in-sql-server"></a>SQL Server での借用を使用した権限のカスタマイズ
多くのアプリケーションでは、ベース テーブルへのアクセスを制限する組み合わせ所有権を利用して、ストアド プロシージャを使ってデータにアクセスします。 ストアド プロシージャに対して EXECUTE 権限を付与するとき、ベース テーブルに対する権限を取り消したり拒否したりできます。 ストアド プロシージャとテーブルの所有者が同じ場合、SQL Server では呼び出し元の権限をチェックしません。 ただし、オブジェクトの所有者が異なる場合や、動的 SQL の場合には、組み合わせ所有権が無効になります。  
  
 参照先オブジェクトに対する権限が呼び出し元になくても、ストアド プロシージャで EXECUTE AS 句を使用できます。 EXECUTE AS 句の効果は、実行コンテキストがプロキシ ユーザーに切り替えられることです。 入れ子になったストアド プロシージャやトリガーへの呼び出しを含め、すべてのコードがプロキシ ユーザーのセキュリティ コンテキストで実行されます。 プロシージャの実行後、または REVERT ステートメントが発行されたときにのみ、実行コンテキストが最初の呼び出し元に戻ります。  
  
## <a name="context-switching-with-the-execute-as-statement"></a>EXECUTE AS ステートメントを使用したコンテキスト切り替え  
 Transact-SQL の EXECUTE AS ステートメントを使用して、別のログインまたはデータベース ユーザーの権限を借用することで、ステートメントの実行コンテキストを切り替えることができます。 これは、クエリとプロシージャを別のユーザーとしてテストできる便利な手法です。  
  
```sql  
EXECUTE AS LOGIN = 'loginName';  
EXECUTE AS USER = 'userName';  
```  
  
 権限を借用するログインまたはユーザーに対する IMPERSONATE 権限が必要です。 この権限は、`sysadmin` にはすべてのデータベースに対して与えられ、`db_owner` ロールのメンバーには所有するデータベースに対して与えられます。  
  
## <a name="granting-permissions-with-the-execute-as-clause"></a>EXECUTE AS 句を使用した権限の許可  
 EXECUTE AS 句は、ストアド プロシージャ、トリガー、ユーザー定義関数 (インライン テーブル値関数を除く) の定義ヘッダーで使用できます。 そのため、EXECUTE AS 句で指定されたユーザー名またはキーワードのコンテキストでプロシージャが実行されます。 データベースに、ログインに割り当てられないプロキシ ユーザーを作成し、プロシージャがアクセスするオブジェクトに対して必要な権限のみを許可することができます。 EXECUTE AS 句で指定されたプロキシ ユーザーのみが、モジュールからアクセスされるすべてのオブジェクトに対する権限を持っている必要があります。  
  
> [!NOTE]
> TRUNCATE TABLE など、許可する権限のない操作もあります。 プロシージャ内にステートメントを組み込み、ALTER TABLE 権限を持つプロキシ ユーザーを指定することで、プロシージャに対する EXECUTE 権限のみを持つ呼び出し元に、テーブルを切り捨てる権限を追加することができます。  
  
 EXECUTE AS 句で指定されたコンテキストは、入れ子になったプロシージャやトリガーを含むプロシージャの実行中に有効となります。 実行が完了したとき、または REVERT ステートメントが発行されたときに、コンテキストが呼び出し元に戻ります。  
  
 プロシージャで EXECUTE AS 句を使用する際には、次の 3 つの手順を実行します。  
  
1. ログインに割り当てられていないプロキシ ユーザーをデータベースに作成します。 この操作は必須ではありませんが、権限を管理するときに役立ちます。  
  
```sql
CREATE USER proxyUser WITHOUT LOGIN  
```  
  
1. プロキシ ユーザーに必要な権限を与えます。  
  
2. ストアド プロシージャまたはユーザー定義関数に EXECUTE AS 句を追加します。  
  
```sql
CREATE PROCEDURE [procName] WITH EXECUTE AS 'proxyUser' AS ...  
```  
  
> [!NOTE]
> 呼び出し元の元のセキュリティ コンテキストが保持されないため、監査の必要なアプリケーションはブレークされる可能性があります。 SESSION_USER、USER、USER_NAME など、現在のユーザーの識別情報を返す組み込み関数では、最初の呼び出し元ではなく EXECUTE AS 句に関連付けられているユーザーが返されます。  
  
### <a name="using-execute-as-with-revert"></a>REVERT での EXECUTE AS の使用  
 Transact-SQL REVERT ステートメントを使用して、元の実行コンテキストに戻ることができます。  
  
 オプションの句である WITH NO REVERT COOKIE = @variableName を使用すると、@variableName 変数に正しい値が含まれていれば、実行コンテキストを呼び出し元に切り替えることができます。 これにより、接続プールが使用されている環境では実行コンテキストを呼び出し元に切り替えることができます。 @variableName の値は、EXECUTE AS ステートメントの呼び出し元のみが把握しているため、実行コンテキストがアプリケーションを呼び出したエンド ユーザーによって変更されることはありません。 接続は、閉じられるとプールに返されます。 ADO.NET での接続プールについて詳しくは、「[SQL Server の接続プール (ADO.NET)](../sql-server-connection-pooling.md)」をご覧ください。  
  
### <a name="specifying-the-execution-context"></a>実行コンテキストの指定  
 EXECUTE AS は、ユーザーを指定するだけでなく、次のキーワードを指定して使用することもできます。  
  
- CALLER :  既定で、CALLER として実行されます。他にオプションが指定されていない場合、プロシージャは呼び出し元のセキュリティ コンテキストで実行されます。  
  
- OWNER :  OWNER として実行すると、プロシージャがプロシージャ所有者のコンテキストで実行されます。 `dbo` すなわちデータベース所有者が所有するスキーマでプロシージャが作成されている場合、プロシージャは権限無制限で実行されます。  
  
- SELF :  SELF として実行すると、ストアド プロシージャの作成者のセキュリティ コンテキストで実行されます。 これは、指定されたユーザーとして実行することと同じです。指定されたユーザーとは、プロシージャを作成または変更した人物です。  
  
## <a name="see-also"></a>関連項目

- [ADO.NET アプリケーションのセキュリティ保護](../securing-ado-net-applications.md)
- [SQL Server セキュリティの概要](overview-of-sql-server-security.md)
- [SQL Server におけるアプリケーション セキュリティのシナリオ](application-security-scenarios-in-sql-server.md)
- [SQL Server でのストアド プロシージャを使用したアクセス許可の管理](managing-permissions-with-stored-procedures-in-sql-server.md)
- [SQL Server での安全な動的 SQL の作成](writing-secure-dynamic-sql-in-sql-server.md)
- [SQL Server でのストアド プロシージャの署名](signing-stored-procedures-in-sql-server.md)
- [ストアド プロシージャでのデータの変更](../modifying-data-with-stored-procedures.md)
- [ADO.NET の概要](../ado-net-overview.md)
