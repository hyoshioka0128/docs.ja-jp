---
title: DataSet への既存の制約の追加
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 307d2809-208b-4cf8-b6a9-5d16f15fc16c
ms.openlocfilehash: 267d6489d39f86fc06b35de8cf30dad74f501b0b
ms.sourcegitcommit: 4f4a32a5c16a75724920fa9627c59985c41e173c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/17/2019
ms.locfileid: "72523240"
---
# <a name="adding-existing-constraints-to-a-dataset"></a>DataSet への既存の制約の追加

**DataAdapter** の **Fill** メソッドを使うと、<xref:System.Data.DataSet> にデータ ソースからのテーブルの列および行だけが格納されます。制約は一般にデータ ソースで設定されますが、既定では **Fill** メソッドによって **DataSet** にこのスキーマ情報は追加されません。 データ ソースからの既存の主キー制約情報を **DataSet** に設定するには、**DataAdapter** の **FillSchema** メソッドを呼び出すか、または **Fill** を呼び出す前に **DataAdapter** の **MissingSchemaAction** プロパティを **AddWithKey** に設定します。 これにより、データ ソースの主キー制約が **DataSet** の主キー制約に反映されます。 外部キー制約情報はインクルードされないため、「[DataTable の制約](./dataset-datatable-dataview/datatable-constraints.md)」で示されているように明示的に作成する必要があります。  
  
データを格納する前に **DataSet** にスキーマ情報を追加すると、**DataSet** 内の <xref:System.Data.DataTable> オブジェクトに主キー制約が含まれるようになります。 その結果、**DataSet** に対して格納を行う追加の呼び出しを行うと、主キー列の情報を使用して、データ ソースからの新しい行と、各 **DataTable** の現在の行が照合されて、テーブルの現在のデータがデータ ソースのデータで上書きされます。 スキーマ情報がないと、**DataSet** にデータ ソースからの新しい行が付け加えられ、重複行が発生します。  
  
> [!NOTE]
> データ ソースの列が自動インクリメントとして指定されている場合、**FillSchema** メソッドまたは **MissingSchemaAction** が **AddWithKey** に設定された **Fill** メソッドでは、**AutoIncrement** プロパティが `true` に設定された **DataColumn** が作成されます。 ただし、**AutoIncrementStep** 値と **AutoIncrementSeed** 値は開発者自身が明示的に設定する必要があります。 自動インクリメント列について詳しくは、「[AutoIncrement 列の作成](./dataset-datatable-dataview/creating-autoincrement-columns.md)」をご覧ください。  
  
**FillSchema** を使用したり、**MissingSchemaAction** を **AddWithKey** に設定したりすると、データ ソースで主キー列情報を確認するための追加の処理が必要になります。 この追加の処理によりパフォーマンスが低下する場合があります。 デザイン時に主キー情報がわかっている場合は、最適のパフォーマンスを得るために主キー列 (複数の場合もある) を明示的に指定することをお勧めします。 テーブルに関する主キー情報を明示的に設定する方法については、「[主キーの定義](./dataset-datatable-dataview/defining-primary-keys.md)」をご覧ください。
  
次のコード例では、**FillSchema** を使用して **DataSet** にスキーマ情報を追加する方法を示します。
  
```vb  
Dim custDataSet As New DataSet()  
  
custAdapter.FillSchema(custDataSet, SchemaType.Source, "Customers")  
custAdapter.Fill(custDataSet, "Customers")  
```  
  
```csharp  
var custDataSet = new DataSet();  
  
custAdapter.FillSchema(custDataSet, SchemaType.Source, "Customers");  
custAdapter.Fill(custDataSet, "Customers");  
```  
  
次のコード例では、**Fill** メソッドの **MissingSchemaAction.AddWithKey** プロパティを使用して **DataSet** にスキーマ情報を追加する方法を示します。
  
```vb  
Dim custDataSet As New DataSet()  
  
custAdapter.MissingSchemaAction = MissingSchemaAction.AddWithKey  
custAdapter.Fill(custDataSet, "Customers")  
```  
  
```csharp  
var custDataSet = new DataSet();  
  
custAdapter.MissingSchemaAction = MissingSchemaAction.AddWithKey;  
custAdapter.Fill(custDataSet, "Customers");  
```  
  
## <a name="handling-multiple-result-sets"></a>複数の結果セットの処理  

**DataAdapter** では、**SelectCommand** から複数の結果セットが返された場合、**DataSet** に複数のテーブルが作成されます。 テーブルには、**Table** *N* という既定の名前が設定されます。N は 0 から始まりインクリメントされますが、"Table0" ではなく **Table** から始まります。 テーブル名が **FillSchema** メソッドに引数として渡された場合は、テーブルには、**TableName** *N* という名前が設定されます。N は 0 から始まりインクリメントされますが、"TableName0" ではなく **TableName** から始まります。  
  
> [!NOTE]
> **OleDbDataAdapter** オブジェクトの **FillSchema** メソッドが、複数の結果セットを返すコマンドに対して呼び出された場合は、最初の結果セットのスキーマ情報のみが返されます。 **OleDbDataAdapter** を使用して複数の結果セットに対するスキーマ情報を返すときは、**Fill** メソッドを呼び出すときに **AddWithKey** に設定した **MissingSchemaAction** を指定して、スキーマ情報を取得することをお勧めします。  
  
## <a name="see-also"></a>関連項目

- [DataAdapter と DataReader](dataadapters-and-datareaders.md)
- [DataSet、DataTable、および DataView](./dataset-datatable-dataview/index.md)
- [ADO.NET でのデータの取得および変更](retrieving-and-modifying-data.md)
- [ADO.NET の概要](ado-net-overview.md)
