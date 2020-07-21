---
title: SqlDependency を使用した変更の検出
description: SqlDependency オブジェクトを SqlCommand に関連付けて、クエリ結果が ADO.NET で最初に取得したものと異なる場合を検出することができます。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: e6a58316-f005-4477-92e1-45cc2eb8c5b4
ms.openlocfilehash: b196d42477e1778c45df64b1390502645fdd649d
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84286469"
---
# <a name="detecting-changes-with-sqldependency"></a>SqlDependency を使用した変更の検出

クエリ結果が最初に取得されたクエリ結果と異なることを検出するために、<xref:System.Data.SqlClient.SqlDependency> オブジェクトを <xref:System.Data.SqlClient.SqlCommand> に関連付けることができます。 `OnChange` イベントにデリゲートを割り当てることもできます。これは、関連付けられたコマンドの結果が変更されたときに実行されます。 コマンドを実行する前に、<xref:System.Data.SqlClient.SqlDependency> をコマンドに関連付ける必要があります。 また、`HasChanges` の <xref:System.Data.SqlClient.SqlDependency> プロパティを使用しても、データが最初に取得されて以降にクエリ結果が変化したかどうかを判別できます。

## <a name="security-considerations"></a>セキュリティの考慮事項

指定されたコマンドについて基になるデータが変更されたという通知を受け取るために、依存関係を持つインフラストラクチャでは <xref:System.Data.SqlClient.SqlConnection> が呼び出されると、<xref:System.Data.SqlClient.SqlDependency.Start%2A> が開かれることを利用します。 クライアントが `SqlDependency.Start` の呼び出しを開始できるかどうかは、<xref:System.Data.SqlClient.SqlClientPermission> を使用し、コード アクセス セキュリティ属性を利用することで制御します。 詳しくは、「[クエリ通知の有効化](enabling-query-notifications.md)」および「[コード アクセス セキュリティと ADO.NET](../code-access-security.md)」をご覧ください。

### <a name="example"></a>例

次の手順では、依存関係を宣言し、コマンドを実行し、結果セットが変更されたときに通知を受け取る方法について説明します。

1. サーバーへの `SqlDependency` 接続を開始します。

2. サーバーに接続して Transact-SQL ステートメントを定義するための <xref:System.Data.SqlClient.SqlConnection> および <xref:System.Data.SqlClient.SqlCommand> オブジェクトを作成します。

3. 新しい `SqlDependency` オブジェクトを作成するか、既存のオブジェクトを使用して、それを `SqlCommand` オブジェクトにバインドします。 内部では、これによって <xref:System.Data.Sql.SqlNotificationRequest> オブジェクトが作成され、必要に応じてコマンド オブジェクトにバインドされます。 この通知要求には、この `SqlDependency` オブジェクトを一意に識別する内部識別子が含まれます。 また、これにより、クライアント リスナーがまだアクティブになっていない場合に起動されます。

4. イベント ハンドラーを `SqlDependency` オブジェクトの `OnChange` イベントにサブスクライブします。

5. `SqlCommand` オブジェクトの任意の `Execute` メソッドを使用して、コマンドを実行します。 コマンドは通知オブジェクトにバインドされているため、サーバーで通知を生成する必要があることが認識され、キュー情報が依存関係キューを指します。

6. サーバーへの `SqlDependency` 接続を停止します。

その後ユーザーが基になるデータを変更した場合、Microsoft SQL Server でその変更に対して保留中の通知があることが検出され、`SqlDependency.Start` を呼び出して作成された、基になる `SqlConnection` を介して処理され、クライアントに転送される通知が送信されます。 クライアント リスナーで、無効化メッセージが受信されます。 次にクライアント リスナーで、関連付けられている `SqlDependency` オブジェクトが検索され、`OnChange` イベントが起動されます。

次のコード フラグメントに、サンプル アプリケーションの作成に利用されるデザイン パターンを示します。

```vb
Sub Initialization()
    ' Create a dependency connection.
    SqlDependency.Start(connectionString, queueName)
End Sub

Sub SomeMethod()
    ' Assume connection is an open SqlConnection.
    ' Create a new SqlCommand object.
    Using command As New SqlCommand( _
      "SELECT ShipperID, CompanyName, Phone FROM dbo.Shippers", _
      connection)

        ' Create a dependency and associate it with the SqlCommand.
        Dim dependency As New SqlDependency(command)
        ' Maintain the refernce in a class member.
        ' Subscribe to the SqlDependency event.
        AddHandler dependency.OnChange, AddressOf OnDependencyChange

        ' Execute the command.
        Using reader = command.ExecuteReader()
            ' Process the DataReader.
        End Using
    End Using
End Sub

' Handler method
Sub OnDependencyChange(ByVal sender As Object, _
    ByVal e As SqlNotificationEventArgs)
    ' Handle the event (for example, invalidate this cache entry).
End Sub

Sub Termination()
    ' Release the dependency
    SqlDependency.Stop(connectionString, queueName)
End Sub
```

```csharp
void Initialization()
{
    // Create a dependency connection.
    SqlDependency.Start(connectionString, queueName);
}

void SomeMethod()
{
    // Assume connection is an open SqlConnection.

    // Create a new SqlCommand object.
    using (SqlCommand command=new SqlCommand(
        "SELECT ShipperID, CompanyName, Phone FROM dbo.Shippers",
        connection))
    {

        // Create a dependency and associate it with the SqlCommand.
        SqlDependency dependency=new SqlDependency(command);
        // Maintain the reference in a class member.

        // Subscribe to the SqlDependency event.
        dependency.OnChange+=new
           OnChangeEventHandler(OnDependencyChange);

        // Execute the command.
        using (SqlDataReader reader = command.ExecuteReader())
        {
            // Process the DataReader.
        }
    }
}

// Handler method
void OnDependencyChange(object sender,
   SqlNotificationEventArgs e )
{
  // Handle the event (for example, invalidate this cache entry).
}

void Termination()
{
    // Release the dependency.
    SqlDependency.Stop(connectionString, queueName);
}
```

## <a name="see-also"></a>関連項目

- [SQL Server のクエリ通知](query-notifications-in-sql-server.md)
- [ADO.NET の概要](../ado-net-overview.md)
