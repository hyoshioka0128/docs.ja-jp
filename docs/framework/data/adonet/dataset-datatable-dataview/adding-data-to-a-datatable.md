---
title: DataTable へのデータの追加
description: DataTable を作成し、列と制約を使用してその構造を定義した後、このコード例を参照して、ADO.NET のテーブルに新しいデータ行を追加します。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: d6aa8474-7bde-48f7-949d-20dc38a1625b
ms.openlocfilehash: 94ebc97d5f90b5bb92186ba6f33015633bd01127
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84286935"
---
# <a name="adding-data-to-a-datatable"></a>DataTable へのデータの追加
<xref:System.Data.DataTable> を作成し、列と制約を使用してそのテーブルの構造を定義した後で、テーブルに新しいデータ行を追加できます。 新しい行を追加するには、新しい変数を <xref:System.Data.DataRow> 型として宣言します。 <xref:System.Data.DataTable.NewRow%2A> メソッドを呼び出すと、新しい **DataRow** オブジェクトが返されます。 次に、**DataTable** は、<xref:System.Data.DataColumnCollection> での定義に従って、テーブルの構造に基づいて **DataRow** オブジェクトを作成します。  
  
 **NewRow** メソッドを呼び出して新しい行を作成する例を次に示します。  
  
```vb  
Dim workRow As DataRow = workTable.NewRow()  
```  
  
```csharp  
DataRow workRow = workTable.NewRow();  
```  
  
 その後でインデックスまたは列名を使用して、新しく追加した行を操作する例を次に示します。  
  
```vb  
workRow("CustLName") = "Smith"  
workRow(1) = "Smith"  
```  
  
```csharp  
workRow["CustLName"] = "Smith";  
workRow[1] = "Smith";  
```  
  
 新しい行にデータを挿入した後で **Add** メソッドを使用して <xref:System.Data.DataRowCollection> に行を追加するコードを次に示します。  
  
```vb  
workTable.Rows.Add(workRow)  
```  
  
```csharp  
workTable.Rows.Add(workRow);  
```  
  
 **Add** メソッドを呼び出して <xref:System.Object> 型の値の配列を渡すことにより、新しい行を追加する別の例を次に示します。  
  
```vb  
workTable.Rows.Add(new Object() {1, "Smith"})  
```  
  
```csharp  
workTable.Rows.Add(new Object[] {1, "Smith"});  
```  
  
 **Object** 型の値の配列を **Add** メソッドに渡すと、テーブル内に新しい行が作成され、その行の列値がオブジェクト配列の値に設定されます。 配列内の値は、テーブル内での列の順序に基づいて、列に順次的に割り当てられます。  
  
 新しく作成した **Customers** テーブルに 10 行を追加する例を次に示します。  
  
```vb  
Dim workRow As DataRow  
Dim i As Integer  
  
For i = 0 To 9  
  workRow = workTable.NewRow()  
  workRow(0) = i  
  workRow(1) = "CustName" & I.ToString()  
  workTable.Rows.Add(workRow)  
Next  
```  
  
```csharp  
DataRow workRow;  
  
for (int i = 0; i <= 9; i++)
{  
  workRow = workTable.NewRow();  
  workRow[0] = i;  
  workRow[1] = "CustName" + i.ToString();  
  workTable.Rows.Add(workRow);  
}  
```  
  
## <a name="see-also"></a>関連項目

- <xref:System.Data.DataColumnCollection>
- <xref:System.Data.DataRow>
- <xref:System.Data.DataRowCollection>
- <xref:System.Data.DataTable>
- [DataTable 内のデータの操作](manipulating-data-in-a-datatable.md)
- [ADO.NET の概要](../ado-net-overview.md)
