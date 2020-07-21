---
title: DataSet の内容のコピー
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: cb846617-2b1a-44ff-bd7f-5835f5ea37fa
ms.openlocfilehash: de13e07eb5c19b8beffa724fec4a128c418a4fed
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79151365"
---
# <a name="copying-dataset-contents"></a>DataSet の内容のコピー
<xref:System.Data.DataSet> のコピーを作成すると、元のデータに影響せずにデータを使用したり、**DataSet** のデータのサブセットを使用したりできます。 **DataSet** をコピーすると、次の操作を行うことができます。  
  
- スキーマ、データ、行状態情報、行バージョンなどの **DataSet** の正確なコピーを作成できます。  
  
- 既存の **DataSet** のスキーマを含み、行だけを変更した **DataSet** を作成できます。 変更されたすべての行を返したり、特定の **DataRowState** を指定したりできます。 行の状態の詳細については、「[行の状態とバージョン](row-states-and-row-versions.md)」を参照してください。  
  
- 行をコピーせずに、**DataSet** のスキーマ (リレーショナル構造) だけをコピーできます。 行は、<xref:System.Data.DataTable> を使用して、既存の <xref:System.Data.DataTable.ImportRow%2A> にインポートできます。  
  
 スキーマとデータを含む **DataSet** の正確なコピーを作成するには、**DataSet** の <xref:System.Data.DataSet.Copy%2A> メソッドを使用します。 **DataSet** の正確なコピーを作成する方法を次のコード サンプルに示します。  
  
```vb  
Dim copyDataSet As DataSet = customerDataSet.Copy()  
```  
  
```csharp  
DataSet copyDataSet = customerDataSet.Copy();  
```  
  
 スキーマと、**Added**、**Modified**、または **Deleted** の行を表すデータだけが含まれる **DataSet** のコピーを作成するには、**DataSet** の <xref:System.Data.DataSet.GetChanges%2A> メソッドを使用します。 また、**GetChanges** の呼び出し時に **DataRowState** の値を渡すことによって、**GetChanges** を使用して特定の行状態の行だけを返すことができます。 **GetChanges** の呼び出し時に **DataRowState** を渡す方法のコード例を次に示します。  
  
```vb  
' Copy all changes.  
Dim changeDataSet As DataSet = customerDataSet.GetChanges()  
' Copy only new rows.  
Dim addedDataSetAs DataSet = _  
    customerDataSet.GetChanges(DataRowState.Added)  
```  
  
```csharp  
// Copy all changes.  
DataSet changeDataSet = customerDataSet.GetChanges();  
// Copy only new rows.  
DataSet addedDataSet= customerDataSet.GetChanges(DataRowState.Added);  
```  
  
 スキーマだけを含む **DataSet** のコピーを作成するには、**DataSet** の <xref:System.Data.DataSet.Clone%2A> メソッドを使用します。 また、**DataTable** の **ImportRow** メソッドを使用して、複製した **DataSet** に既存の行を追加することもできます。 **ImportRow** メソッドを使用すると、データ、行の状態、および行バージョンの情報が指定したテーブルに追加されます。 列名が一致し、データ型が互換性のある型の場合には、列の値だけが追加されます。  
  
 **DataSet** の複製を作成し、**CountryRegion** 列の値が "Germany" の顧客に対する **DataSet** の複製内の **Customers** テーブルに、元の **DataSet** の行を追加するコードの例を次に示します。  
  
```vb  
Dim customerDataSet As New DataSet  
        customerDataSet.Tables.Add(New DataTable("Customers"))  
        customerDataSet.Tables("Customers").Columns.Add("Name", GetType(String))  
        customerDataSet.Tables("Customers").Columns.Add("CountryRegion", GetType(String))  
        customerDataSet.Tables("Customers").Rows.Add("Juan", "Spain")  
        customerDataSet.Tables("Customers").Rows.Add("Johann", "Germany")  
        customerDataSet.Tables("Customers").Rows.Add("John", "UK")  
  
Dim germanyCustomers As DataSet = customerDataSet.Clone()  
  
Dim copyRows() As DataRow = _  
  customerDataSet.Tables("Customers").Select("CountryRegion = 'Germany'")  
  
Dim customerTable As DataTable = germanyCustomers.Tables("Customers")  
Dim copyRow As DataRow  
  
For Each copyRow In copyRows  
  customerTable.ImportRow(copyRow)  
Next  
```  
  
```csharp  
DataSet customerDataSet = new DataSet();  
customerDataSet.Tables.Add(new DataTable("Customers"));  
customerDataSet.Tables["Customers"].Columns.Add("Name", typeof(string));  
customerDataSet.Tables["Customers"].Columns.Add("CountryRegion", typeof(string));  
customerDataSet.Tables["Customers"].Rows.Add("Juan", "Spain");  
customerDataSet.Tables["Customers"].Rows.Add("Johann", "Germany");  
customerDataSet.Tables["Customers"].Rows.Add("John", "UK");  
  
DataSet germanyCustomers = customerDataSet.Clone();  
  
DataRow[] copyRows =
  customerDataSet.Tables["Customers"].Select("CountryRegion = 'Germany'");  
  
DataTable customerTable = germanyCustomers.Tables["Customers"];  
  
foreach (DataRow copyRow in copyRows)  
  customerTable.ImportRow(copyRow);  
```  
  
## <a name="see-also"></a>関連項目

- <xref:System.Data.DataSet>
- <xref:System.Data.DataTable>
- [DataSet、DataTable、および DataView](index.md)
- [ADO.NET の概要](../ado-net-overview.md)
