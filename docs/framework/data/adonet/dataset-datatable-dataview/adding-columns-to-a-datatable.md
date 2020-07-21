---
title: DataTable への列の追加
description: DataTable には、テーブルの Columns プロパティによって参照される DataColumn オブジェクトが格納されます。 次のコード例を使用して、ADO.NET のテーブルに列を追加します。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: e85c4a0e-4f3f-458c-b58b-0ddbc06bf974
ms.openlocfilehash: 9d6d21696acd7a6b63cfd6d2ea7e906ec2acd7c9
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84286948"
---
# <a name="adding-columns-to-a-datatable"></a>DataTable への列の追加
<xref:System.Data.DataTable> には、テーブルの **Columns** プロパティによって参照される <xref:System.Data.DataColumn> オブジェクトのコレクションが格納されます。 この列のコレクションと制約によって、テーブルのスキーマ (構造) が定義されます。  
  
 テーブル内に **DataColumn** オブジェクトを作成するには、**DataColumn** コンストラクターを使用するか、または <xref:System.Data.DataColumnCollection> であるテーブルの **Columns** プロパティの **Add** メソッドを呼び出します。 **Add** メソッドは、オプションの **ColumnName**、**DataType**、**Expression** の各引数を受け取り、新しい **DataColumn** をコレクションのメンバーとして作成します。 また、このメソッドは既存の **DataColumn** オブジェクトを受け取り、それをコレクションに追加して、要求された場合は、追加された **DataColumn** への参照を返します。 **DataTable** オブジェクトはデータ ソースに固有ではないため、**DataColumn** のデータ型を指定するときには、.NET Framework 型が使用されます。  
  
 **DataTable** に 4 つの列を追加する例を次に示します。  
  
```vb  
Dim workTable As DataTable = New DataTable("Customers")  
  
Dim workCol As DataColumn = workTable.Columns.Add( _  
    "CustID", Type.GetType("System.Int32"))  
workCol.AllowDBNull = false  
workCol.Unique = true  
  
workTable.Columns.Add("CustLName", Type.GetType("System.String"))  
workTable.Columns.Add("CustFName", Type.GetType("System.String"))  
workTable.Columns.Add("Purchases", Type.GetType("System.Double"))  
```  
  
```csharp  
DataTable workTable = new DataTable("Customers");  
  
DataColumn workCol = workTable.Columns.Add("CustID", typeof(Int32));  
workCol.AllowDBNull = false;  
workCol.Unique = true;  
  
workTable.Columns.Add("CustLName", typeof(String));  
workTable.Columns.Add("CustFName", typeof(String));  
workTable.Columns.Add("Purchases", typeof(Double));  
```  
  
 この例では、**DBNull** 値を許可せずに値を一意の値に制約するように、**CustID** 列のプロパティが設定されていることに注意してください。 ただし、**CustID** 列をテーブルの主キー列として定義した場合、**AllowDBNull** プロパティは自動的に **false** に設定され、**Unique** プロパティは自動的に **true** に設定されます。 詳しくは、「[主キーの定義](defining-primary-keys.md)」をご覧ください。  
  
> [!CAUTION]
> 列名が指定されていない列を **DataColumnCollection** に追加する場合、この列には "Column1" から始まって増分される既定名 Column*N* が割り当てられます。 列名を指定するときには、"Column*N*" の命名規則を使用しないことをお勧めします。これは、指定した名前が **DataColumnCollection** に既に存在する既定の列名と競合しないようにするためです。 指定した名前が既に存在する場合は、例外がスローされます。  
  
 <xref:System.Xml.Linq.XElement> を、<xref:System.Data.DataColumn.DataType%2A> 内の <xref:System.Data.DataColumn> の <xref:System.Data.DataTable> として使用すると、データを読み取るときに XML シリアル化が機能しません。 たとえば、<xref:System.Xml.XmlDocument> メソッドを使用して `DataTable.WriteXml` を書き込むと、XML へのシリアル化で <xref:System.Xml.Linq.XElement> に親ノードが追加されます。 この問題に対処するには、<xref:System.Data.SqlTypes.SqlXml> の代わりに <xref:System.Xml.Linq.XElement> 型を使用します。 `ReadXml` および `WriteXml` は、<xref:System.Data.SqlTypes.SqlXml> で適切に機能します。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Data.DataColumn>
- <xref:System.Data.DataColumnCollection>
- <xref:System.Data.DataTable>
- [DataTable スキーマの定義](datatable-schema-definition.md)
- [DataTables](datatables.md)
- [ADO.NET の概要](../ado-net-overview.md)
