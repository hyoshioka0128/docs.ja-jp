---
title: DataAdapter DataTable と DataColumn のマップ
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: d023260a-a66a-4c39-b8f4-090cd130e730
ms.openlocfilehash: 6380dd0512bd7834f50b87f90f445cb01b7a8b95
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79151560"
---
# <a name="dataadapter-datatable-and-datacolumn-mappings"></a>DataAdapter DataTable と DataColumn のマップ
**DataAdapter** の **TableMappings** プロパティには、0 個以上の <xref:System.Data.Common.DataTableMapping> オブジェクトのコレクションが含まれます。 **DataTableMapping** では、データ ソースに対するクエリで返されたデータと <xref:System.Data.DataTable> の間のマスター マッピングが提供されます。 **DataTableMapping** 名は、**DataAdapter** の **Fill** メソッドに **DataTable** 名の代わりとして渡すことができます。 **Authors** テーブルに対して **AuthorsMapping** という名前の **DataTableMapping** を作成する例を次に示します。  
  
```vb  
workAdapter.TableMappings.Add("AuthorsMapping", "Authors")  
```  
  
```csharp  
workAdapter.TableMappings.Add("AuthorsMapping", "Authors");  
```  
  
 **DataTableMapping** を使用すると、**DataTable** 内でデータベースの列名とは異なる列名を使用できます。 **DataAdapter** では、テーブルの更新時にこのマップを使用して列が照合されます。  
  
 **DataAdapter** の **Fill** メソッドまたは **Update** メソッドを呼び出すときに **TableName** または **DataTableMapping** 名を指定しなかった場合、**DataAdapter** では "Table" という名前の **DataTableMapping** が検索されます。 その **DataTableMapping** が存在しない場合は、**DataTable** の **TableName** が "Table" になります。 "Table" という名前の **DataTableMapping** を作成することで既定の **DataTableMapping** を指定できます。  
  
 次に示すのは、<xref:System.Data.Common> 名前空間から **DataTableMapping** を作成し、それに "Table" という名前を付けて、指定した **DataAdapter** の既定のマップとして設定するコード サンプルです。 この例では、その後、クエリ結果の最初のテーブル (**Northwind** データベースの **Customers** テーブル) の列を <xref:System.Data.DataSet> の **Northwind Customers** テーブルにある、よりわかりやすい名前のセットに割り当てます。 割り当てられない列には、データ ソースの列名が使用されます。  
  
```vb  
Dim mapping As DataTableMapping = _  
  adapter.TableMappings.Add("Table", "NorthwindCustomers")  
mapping.ColumnMappings.Add("CompanyName", "Company")  
mapping.ColumnMappings.Add("ContactName", "Contact")  
mapping.ColumnMappings.Add("PostalCode", "ZIPCode")  
  
adapter.Fill(custDS)  
```  
  
```csharp  
DataTableMapping mapping =
  adapter.TableMappings.Add("Table", "NorthwindCustomers");  
mapping.ColumnMappings.Add("CompanyName", "Company");  
mapping.ColumnMappings.Add("ContactName", "Contact");  
mapping.ColumnMappings.Add("PostalCode", "ZIPCode");  
  
adapter.Fill(custDS);  
```  
  
 より高度な条件下では、同じ **DataAdapter** を使用して複数の割り当てが設定された複数テーブルの読み込みのサポートが必要な場合があります。 この場合、**DataTableMapping** オブジェクトを追加します。  
  
 **Fill** メソッドに **DataSet** のインスタンスと **DataTableMapping** 名が渡されたとき、その名前の割り当てが存在する場合はその名前が使用され、存在しない場合はその名前の **DataTable** が使用されます。  
  
 次に示すのは、**Customers** という名前と **BizTalkSchema** という **DataTable** 名を持つ **DataTableMapping** を作成する例です。 この例では、その後で、SELECT ステートメントで返された行を **BizTalkSchema** **DataTable** に割り当てています。  
  
```vb  
Dim mapping As ITableMapping = _  
  adapter.TableMappings.Add("Customers", "BizTalkSchema")  
mapping.ColumnMappings.Add("CustomerID", "ClientID")  
mapping.ColumnMappings.Add("CompanyName", "ClientName")  
mapping.ColumnMappings.Add("ContactName", "Contact")  
mapping.ColumnMappings.Add("PostalCode", "ZIP")  
  
adapter.Fill(custDS, "Customers")  
```  
  
```csharp  
ITableMapping mapping =
  adapter.TableMappings.Add("Customers", "BizTalkSchema");  
mapping.ColumnMappings.Add("CustomerID", "ClientID");  
mapping.ColumnMappings.Add("CompanyName", "ClientName");  
mapping.ColumnMappings.Add("ContactName", "Contact");  
mapping.ColumnMappings.Add("PostalCode", "ZIP");  
  
adapter.Fill(custDS, "Customers");  
```  
  
> [!NOTE]
> 列マップにソースの列名を指定しなかった場合、またはテーブル マップにソース テーブル名を指定しなかった場合は、自動的に既定の名前が生成されます。 列マップにソース列を指定しなかった場合は、列マップに **SourceColumn1** から始まるインクリメンタル既定名 **SourceColumn***N* が割り当てられます。 テーブル マップにソース テーブル名を指定しなかった場合は、テーブル マップに **SourceTable1** から始まるインクリメンタル既定名 **SourceTable***N* が割り当てられます。  
  
> [!NOTE]
> 列マップには、**SourceColumn***N* の命名規則を使用しないこと、また、テーブルの割り当てには **SourceTable***N* を使用しないことをお勧めします。これは、指定した名前が **ColumnMappingCollection** 内の既存する既定の列マップ名または **DataTableMappingCollection** 内のテーブル マップ名と競合しないようにするためです。 指定した名前が既に存在する場合は、例外がスローされます。  
  
## <a name="handling-multiple-result-sets"></a>複数の結果セットの処理  
 **SelectCommand** で複数のテーブルが返される場合、**Fill** では **DataSet** 内のテーブルに対する、インクリメント値を含むテーブル名が自動的に生成されます。これは、指定したテーブル名で開始し、**TableName***N* の形式で **TableName1** から数値を加算していく名前になります。 自動的に生成されたテーブル名は、テーブルの割り当てを使用して **DataSet** 内でテーブルに指定する名前に変換できます。 たとえば、**Customers** および **Orders** という 2 つのテーブルを返す **SelectCommand** に対して、次の **Fill** 呼び出しを実行します。  
  
```vb  
adapter.Fill(customersDataSet, "Customers")  
```  

```csharp  
adapter.Fill(customersDataSet, "Customers");  
```  

 **DataSet** には、次の 2 つのテーブルが作成されます: **Customers** と **Customers1**。 テーブル マップを使用して、2 つ目のテーブルに **Customers1** という名前の代わりに **Orders** という名前を付けることができます。 それには、次の例に示すように、ソース テーブル **Customers1** を **DataSet** テーブルの **Orders** に割り当てます。  
  
```vb  
adapter.TableMappings.Add("Customers1", "Orders")  
adapter.Fill(customersDataSet, "Customers")  
```  

```csharp  
adapter.TableMappings.Add("Customers1", "Orders");  
adapter.Fill(customersDataSet, "Customers");  
```
  
## <a name="see-also"></a>関連項目

- [DataAdapter と DataReader](dataadapters-and-datareaders.md)
- [ADO.NET でのデータの取得および変更](retrieving-and-modifying-data.md)
- [ADO.NET の概要](ado-net-overview.md)
