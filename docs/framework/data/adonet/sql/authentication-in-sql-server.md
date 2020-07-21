---
title: SQL Server での認証
description: Windows 認証モードや混合モードなど、ADO.NET の SQL Server での認証について説明します。
ms.date: 05/22/2018
ms.assetid: 646ddbf5-dd4e-4285-8e4a-f565f666c5cc
ms.openlocfilehash: e9915598acfbdefb59069d6a9c6ef4b7c824e4c6
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84286547"
---
# <a name="authentication-in-sql-server"></a>SQL Server での認証
SQL Server は、Windows 認証モードと混合モードの 2 つの認証モードをサポートしています。  
  
- Windows 認証は既定の認証モードです。この SQL Server セキュリティ モデルは、Windows と緊密に統合されていることから統合セキュリティと呼ばれることもあります。 特定の Windows ユーザー アカウントとグループ アカウントは、SQL Server へのログインが信頼されています。 すでに認証されている Windows ユーザーは、追加の資格情報を提示する必要はありません。  
  
- 混合モードは、Windows による認証と SQL Server による認証の両方がサポートされます。 SQL Server 内でユーザー名とパスワードのペアが管理されます。  
  
> [!IMPORTANT]
> 可能な限り、Windows 認証を使用することが推奨されます。 Windows 認証では、暗号化された一連のメッセージを使用して SQL Server のユーザーを認証します。 SQL Server ログインを使用した場合、SQL Server のログイン名と暗号化されたパスワードがネットワーク経由で渡されるためセキュリティが低下します。  
  
 Windows 認証では、既に Windows にログオンしているユーザーが別途 SQL Server にログオンする必要はありません。 次の `SqlConnection.ConnectionString` では Windows 認証が指定されるため、ユーザー名もパスワードもユーザーに要求させません。  
  
```csharp  
"Server=MSSQL1;Database=AdventureWorks;Integrated Security=true;"
```  
  
> [!NOTE]
> ログインはデータベース ユーザーとは異なります。 ログインまたは Windows グループは、別の操作でデータベース ユーザーまたはロールにマップする必要があります。 その後、ユーザーまたはロールに対してデータベース オブジェクトにアクセスするための権限を付与することになります。  
  
## <a name="authentication-scenarios"></a>認証のシナリオ  
 通常、以下の状況では Windows 認証が最良の選択肢です。  
  
- ドメイン コントローラーがある。  
  
- アプリケーションとデータベースが同じコンピューター上にある。  
  
- SQL Server Express または LocalDB のインスタンスを使用している。  
  
 SQL Server のログインは、次の状況でよく使われます。  
  
- ワークグループがある場合。  
  
- ユーザーが、信頼されていない別のドメインから接続する。  
  
- ASP.NET などのインターネット アプリケーション。  
  
> [!NOTE]
> Windows 認証を指定しても、SQL Server ログインは無効になりません。 高い権限を持つ SQL Server ログインを無効にするには、Transact-SQL ステートメント ALTER LOGIN DISABLE を使用します。  
  
## <a name="login-types"></a>ログインの種類  
 SQL Server では、次の 3 種類のログインがサポートされています。  
  
- ローカル Windows ユーザー アカウントまたは信頼される側のドメイン アカウント。 SQL Server が Windows に依存する形で Windows ユーザー アカウントを認証します。  
  
- Windows グループ。 Windows グループへのアクセス権を付与すると、そのグループのメンバーであるすべての Windows ユーザー ログインへのアクセス権が付与されます。  
  
- SQL Server ログイン。 SQL Server はユーザー名およびパスワードのハッシュを master データベースに格納し、内部の認証方法を使ってログイン試行を検証します。  
  
> [!NOTE]
> SQL Server では、証明書または非対称キーから作成されたログインが提供されています。このログインはコード署名にのみ使用されます。 SQL Server への接続には使用できません。  
  
## <a name="mixed-mode-authentication"></a>混合モード認証  
 混合モード認証を使用する場合は、SQL Server に格納される SQL Server ログインを作成する必要があります。 さらに、SQL Server のユーザー名とパスワードを実行時に指定する必要があります。  
  
> [!IMPORTANT]
> SQL Server は、`sa` ("system administrator" の略) という名前の SQL Server ログインでインストールされます。 `sa` ログインに強力なパスワードを割り当て、アプリケーションで `sa` ログインを使用しないでください。 `sa` ログインは `sysadmin` 固定サーバー ロールにマップされます。このロールには、サーバー全体に対する取り消し不可能な管理者資格情報が割り当てられています。 攻撃者がシステム管理者としてアクセス権を獲得した場合、損害の可能性はとどまることがありません。 既定では、Windows `BUILTIN\Administrators` グループ (ローカル管理者のグループ) のすべてのメンバーが `sysadmin` ロールに所属しますが、sysadmin ロールから Windows の Administrators グループのメンバーを削除することもできます。  
  
 SQL Server では、SQL Server ログインのための Windows パスワード ポリシー メカニズムが提供されています。 パスワードの複雑性のポリシーは、考えられるパスワードの数を増やすことにより、総当たり攻撃を防ぐようにデザインされています。 SQL Server では、SQL Server 内部で使用されるパスワードに、同じ複雑性ポリシーおよび有効期限ポリシーを適用できます。  
  
> [!IMPORTANT]
> ユーザー入力から文字列を連結することによって接続文字列を構築している場合、接続文字列のインジェクション攻撃に対して脆弱になります。 <xref:System.Data.SqlClient.SqlConnectionStringBuilder> を使用すると、構文的に正しい接続文字列を実行時に作成できます。 詳細については、「[接続文字列ビルダー](../connection-string-builders.md)」をご覧ください。  
  
## <a name="external-resources"></a>外部リソース  
 詳細については、次のリソースを参照してください。  
  
|リソース|説明|  
|--------------|-----------------|  
|[プリンシパル](/sql/relational-databases/security/authentication-access/principals-database-engine)|SQL Server のログインおよびその他のセキュリティ プリンシパルについて説明します。|  
  
## <a name="see-also"></a>関連項目

- [ADO.NET アプリケーションのセキュリティ保護](../securing-ado-net-applications.md)
- [SQL Server におけるアプリケーション セキュリティのシナリオ](application-security-scenarios-in-sql-server.md)
- [データ ソースへの接続](../connecting-to-a-data-source.md)
- [接続文字列](../connection-strings.md)
- [ADO.NET の概要](../ado-net-overview.md)
