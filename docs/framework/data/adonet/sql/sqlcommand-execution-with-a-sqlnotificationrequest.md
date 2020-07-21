---
title: SqlCommand の実行と SqlNotificationRequest
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 1776f48f-9bea-41f6-83a4-c990c7a2c991
ms.openlocfilehash: 3115bfb80d4e5e61ed49da11e36eaa37bc24334f
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2019
ms.locfileid: "70791536"
---
# <a name="sqlcommand-execution-with-a-sqlnotificationrequest"></a>SqlCommand の実行と SqlNotificationRequest

サーバーからフェッチした後で、データが変更される場合があります。当然、もう一度クエリを実行すると、前回とは異なる結果セットが得られます。<xref:System.Data.SqlClient.SqlCommand> を適切に構成することで、このような場合に通知を生成することができます。 この機能は、サーバー上でカスタムの通知キューを使用する場合や、実際のオブジェクトを保持しない場合に役に立ちます。

## <a name="creating-the-notification-request"></a>通知要求の作成

<xref:System.Data.Sql.SqlNotificationRequest> オブジェクトを使用して通知要求を作成し、それを `SqlCommand` オブジェクトにバインドできます。 要求を作成したら、`SqlNotificationRequest` オブジェクトは不要になります。 キューに対して任意の通知を照会し、適切に応答することができます。 通知は、アプリケーションがシャットダウンされ、その後再起動された場合でも発生する可能性があります。

コマンドに通知を関連付けて実行した場合、元の結果セットになんらかの変更が生じると、通知要求で構成した SQL Server キューにメッセージが送信されます。

SQL Server のキューをポーリングしメッセージを解釈する方法は、アプリケーションごとに固有なものになります。 アプリケーションは、メッセージの内容に基づいてキューのポーリングと応答を行います。

> [!NOTE]
> <xref:System.Data.SqlClient.SqlDependency> と共に SQL Server 通知要求を使用する場合は、既定のサービス名を使用するのではなく、独自のキュー名を作成してください。

<xref:System.Data.Sql.SqlNotificationRequest> に対応する新しいクライアント側セキュリティ要素はありません。 これはそもそもサーバー機能であり、ユーザーが通知を要求するために保持する必要がある特権はサーバーによって作成されています。

### <a name="example"></a>例

次のコード フラグメントは、<xref:System.Data.Sql.SqlNotificationRequest> を作成し、それを <xref:System.Data.SqlClient.SqlCommand> に関連付ける方法を示しています。

```vb
' Assume connection is an open SqlConnection.
' Create a new SqlCommand object.
Dim command As New SqlCommand( _
  "SELECT ShipperID, CompanyName, Phone FROM dbo.Shippers", connection)

' Create a SqlNotificationRequest object.
Dim notifcationRequest As New SqlNotificationRequest()
notificationRequest.id = "NotificationID"
notificationRequest.Service = "mySSBQueue"

' Associate the notification request with the command.
command.Notification = notificationRequest
' Execute the command.
command.ExecuteReader()
' Process the DataReader.
' You can use Transact-SQL syntax to periodically poll the
' SQL Server queue to see if you have a new message.
```

```csharp
// Assume connection is an open SqlConnection.
// Create a new SqlCommand object.
SqlCommand command=new SqlCommand(
 "SELECT ShipperID, CompanyName, Phone FROM dbo.Shippers", connection);

// Create a SqlNotificationRequest object.
SqlNotificationRequest notificationRequest=new SqlNotificationRequest();
notificationRequest.id="NotificationID";
notificationRequest.Service="mySSBQueue";

// Associate the notification request with the command.
command.Notification=notificationRequest;
// Execute the command.
command.ExecuteReader();
// Process the DataReader.
// You can use Transact-SQL syntax to periodically poll the
// SQL Server queue to see if you have a new message.
```

## <a name="see-also"></a>関連項目

- [SQL Server のクエリ通知](query-notifications-in-sql-server.md)
- [ADO.NET の概要](../ado-net-overview.md)
