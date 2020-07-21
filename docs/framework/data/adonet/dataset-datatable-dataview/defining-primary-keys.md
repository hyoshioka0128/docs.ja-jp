---
title: 主キーの定義
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 2ea85959-e763-4669-8bd9-46a9dab894bd
ms.openlocfilehash: 159b23eb4ef5ca38ebce6e488080d315ec3be081
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79151183"
---
# <a name="defining-primary-keys"></a>主キーの定義
通常、データベース テーブルには、テーブル内の各行を一意に識別する単一の列または複数の列があります。 行を識別するこのような列を、主キーと呼びます。  
  
 1 つの <xref:System.Data.DataColumn> を <xref:System.Data.DataTable> の <xref:System.Data.DataTable.PrimaryKey%2A> として指定すると、テーブルによってその列の <xref:System.Data.DataColumn.AllowDBNull%2A> プロパティが **false** に、<xref:System.Data.DataColumn.Unique%2A> プロパティが **true** に自動的に設定されます。 複数列の主キーの場合は、**AllowDBNull** プロパティだけが自動的に **false** に設定されます。  
  
 <xref:System.Data.DataTable> の **PrimaryKey** プロパティがその値として、1 つ以上の **DataColumn** オブジェクトから成る配列を受け取る例を次に示します。 最初の例は、1 つの列を主キーとして定義しています。  
  
```vb  
workTable.PrimaryKey = New DataColumn() {workTable.Columns("CustID")}  
  
' Or  
  
Dim columns(1) As DataColumn  
columns(0) = workTable.Columns("CustID")  
workTable.PrimaryKey = columns  
```  
  
```csharp  
workTable.PrimaryKey = new DataColumn[] {workTable.Columns["CustID"]};  
  
// Or  
  
DataColumn[] columns = new DataColumn[1];  
columns[0] = workTable.Columns["CustID"];  
workTable.PrimaryKey = columns;  
```  
  
 2 つの列を主キーとして定義する例を次に示します。  
  
```vb  
workTable.PrimaryKey = New DataColumn() {workTable.Columns("CustLName"), _  
                                         workTable.Columns("CustFName")}  
  
' Or  
  
Dim keyColumn(2) As DataColumn  
keyColumn(0) = workTable.Columns("CustLName")  
keyColumn(1) = workTable.Columns("CustFName")  
workTable.PrimaryKey = keyColumn  
```  
  
```csharp  
workTable.PrimaryKey = new DataColumn[] {workTable.Columns["CustLName"],
                                         workTable.Columns["CustFName"]};  
  
// Or  
  
DataColumn[] keyColumn = new DataColumn[2];  
keyColumn[0] = workTable.Columns["CustLName"];  
keyColumn[1] = workTable.Columns["CustFName"];  
workTable.PrimaryKey = keyColumn;  
```  
  
## <a name="see-also"></a>関連項目

- <xref:System.Data.DataTable>
- [DataTable スキーマの定義](datatable-schema-definition.md)
- [DataTables](datatables.md)
- [ADO.NET の概要](../ado-net-overview.md)
