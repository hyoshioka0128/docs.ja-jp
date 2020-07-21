---
title: DataTable 内のデータの表示
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 1d26e0fb-f6e0-4afa-9a9c-b8d55b8f20dc
ms.openlocfilehash: c13f0b802b2714a17ea4014625a65ebd1b0011f4
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2019
ms.locfileid: "70785852"
---
# <a name="viewing-data-in-a-datatable"></a>DataTable 内のデータの表示

<xref:System.Data.DataTable> の内容には、**DataTable** の **Rows** コレクションと **Columns** コレクションを使用してアクセスできます。 また、<xref:System.Data.DataTable.Select%2A> メソッドを使用すると、検索条件、並べ替え順序、行の状態などの基準に基づいて **DataTable** 内のデータのサブセットを返すことができます。 さらに、主キー値を使用して特定の行を検索するときは、**DataRowCollection** の <xref:System.Data.DataRowCollection.Find%2A> メソッドを使用できます。

**DataTable** オブジェクトの **Select** メソッドからは、指定した条件と一致する <xref:System.Data.DataRow> オブジェクトのセットが返されます。 **Select** は、オプションの引数として、フィルター式、並べ替え式、**DataViewRowState** を受け取ります。 フィルター式では、**DataColumn** の値に基づいて返す行が特定されます (`LastName = 'Smith'` など)。 並べ替え式は、列の並べ替えについての標準 SQL 規則に基づく `LastName ASC, FirstName ASC` などの式です。 式の記述の規則については、**DataColumn** クラスの <xref:System.Data.DataColumn.Expression%2A> プロパティのトピックを参照してください。

> [!TIP]
> **DataTable** の **Select** メソッドへの呼び出しを多数実行する場合は、最初に **DataTable** の <xref:System.Data.DataView> を作成することにより、パフォーマンスを向上させることができます。 **DataView** を作成すると、テーブルの行にインデックスが付けられます。 **Select** メソッドでそのインデックスを使用すると、クエリ結果を生成するまでの時間が大幅に短縮されます。 **DataTable** の **DataView** を作成する方法については、「[DataView](dataviews.md)」を参照してください。

**Select** メソッドでは、<xref:System.Data.DataViewRowState> に基づいて、表示または操作する行のバージョンが決定されます。 有効な **DataViewRowState** 列挙値の説明を次の表に示します。

|DataViewRowState の値|説明|
|----------------------------|-----------------|
|**CurrentRows**|変更されていない行、追加された行、および変更された行を含む現在の行。|
|**削除済み**|削除された行。|
|**ModifiedCurrent**|元のデータを変更した後のバージョンである、現在のバージョン。 (**ModifiedOriginal** を参照)|
|**ModifiedOriginal**|変更されたすべての行の元のバージョン。 現在のバージョンは、**ModifiedCurrent** を使用して取得できます。|
|**追加**|新しい行。|
|**None**|なし。|
|**OriginalRows**|変更されていない行および削除された行を含む元の行。|
|**Unchanged**|変更されていない行。|

次の例では、**DataSet** オブジェクトをフィルター処理して、**DataViewRowState** が **CurrentRows** に設定されている行だけを操作できるようにします。

```vb
Dim column As DataColumn
Dim row As DataRow

Dim currentRows() As DataRow = _
    workTable.Select(Nothing, Nothing, DataViewRowState.CurrentRows)

If (currentRows.Length < 1 ) Then
  Console.WriteLine("No Current Rows Found")
Else
  For Each column in workTable.Columns
    Console.Write(vbTab & column.ColumnName)
  Next

  Console.WriteLine(vbTab & "RowState")

  For Each row In currentRows
    For Each column In workTable.Columns
      Console.Write(vbTab & row(column).ToString())
    Next

    Dim rowState As String = _
        System.Enum.GetName(row.RowState.GetType(), row.RowState)
    Console.WriteLine(vbTab & rowState)
  Next
End If
```

```csharp
DataRow[] currentRows = workTable.Select(
    null, null, DataViewRowState.CurrentRows);

if (currentRows.Length < 1 )
  Console.WriteLine("No Current Rows Found");
else
{
  foreach (DataColumn column in workTable.Columns)
    Console.Write("\t{0}", column.ColumnName);

  Console.WriteLine("\tRowState");

  foreach (DataRow row in currentRows)
  {
    foreach (DataColumn column in workTable.Columns)
      Console.Write("\t{0}", row[column]);

    Console.WriteLine("\t" + row.RowState);
  }
}
```

**Select** メソッドを使用して、異なる **RowState** 値またはフィールド値を持つ行を返すこともできます。 次の例では、削除されたすべての行を参照する **DataRow** 配列と、**CustID** 列が 5 より大きいすべての行 (**CustLName** の順に並べ替えられたもの) を参照する別の **DataRow** 配列が返されます。 **Deleted** 行の情報を表示する方法については、「[行の状態とバージョン](row-states-and-row-versions.md)」を参照してください。

```vb
' Retrieve all deleted rows.
Dim deletedRows() As DataRow = workTable.Select(Nothing, Nothing, DataViewRowState.Deleted)

' Retrieve rows where CustID > 5, and order by CustLName.
Dim custRows() As DataRow = workTable.Select( _
    "CustID > 5", "CustLName ASC")
```

```csharp
// Retrieve all deleted rows.
DataRow[] deletedRows = workTable.Select(
    null, null, DataViewRowState.Deleted);

// Retrieve rows where CustID > 5, and order by CustLName.
DataRow[] custRows = workTable.Select("CustID > 5", "CustLName ASC");
```

## <a name="see-also"></a>関連項目

- <xref:System.Data.DataRow>
- <xref:System.Data.DataSet>
- <xref:System.Data.DataTable>
- <xref:System.Data.DataViewRowState>
- [DataTable 内のデータの操作](manipulating-data-in-a-datatable.md)
- [行の状態とバージョン](row-states-and-row-versions.md)
- [ADO.NET の概要](../ado-net-overview.md)
