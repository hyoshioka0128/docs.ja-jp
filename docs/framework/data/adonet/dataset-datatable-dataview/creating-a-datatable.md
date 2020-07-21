---
title: DataTable の作成
description: ADO.NET で DataTable を作成する方法について説明します。これは、インメモリ リレーショナル データの 1 つのテーブルを表し、単独で使用することも、他の .NET Framework オブジェクトで使用することもできます。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: eecf9d78-60e3-4fdc-8de0-e56c13a89414
ms.openlocfilehash: 335137eeef02e590539c6d83e46cb39901a1e03f
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84286922"
---
# <a name="creating-a-datatable"></a>DataTable の作成
<xref:System.Data.DataTable> は 1 つのインメモリ リレーショナル データのテーブルを表します。DataTable は単独で作成および使用することも、他の .NET Framework オブジェクトから <xref:System.Data.DataSet> のメンバーとして使用することもできます。  
  
 **DataTable** オブジェクトは、適切な **DataTable** コンストラクターを使用することにより作成できます。 このオブジェクトを **DataSet** に追加するには、**Add** メソッドを使用して、**DataTable** オブジェクトの **Tables** コレクションにオブジェクトを追加します。  
  
 **DataSet** 内に **DataTable** オブジェクトを作成する場合は、**DataAdapter** オブジェクトの **Fill** メソッドまたは **FillSchema** メソッドを使用するか、**DataSet** の **ReadXml**、**ReadXmlSchema**、または **InferXmlSchema** メソッドを使用して定義済みまたは推論による XML スキーマから作成することができます。 ある **DataSet** の **Tables** コレクションのメンバーとして追加した **DataTable** を、その後で他の **DataSet** のテーブルのコレクションに追加することはできません。  
  
 最初に作成した時点では、**DataTable** にはスキーマ (構造) がありません。 テーブルのスキーマを定義するには、<xref:System.Data.DataColumn> オブジェクトを作成し、テーブルの **Columns** コレクションに追加する必要があります。 テーブルの主キー列を定義したり、**Constraint** オブジェクトを作成してテーブルの **Constraints** コレクションに追加したりすることもできます。 **DataTable** のスキーマを定義した後で、**DataRow** オブジェクトをテーブルの **Rows** コレクションに追加することにより、データ行をテーブルに追加できます。  
  
 **DataTable** を作成するときに <xref:System.Data.DataTable.TableName%2A> プロパティの値を指定する必要はありません。このプロパティは、後から指定することも、空のままにしておくこともできます。 ただし、**TableName** 値のないテーブルを **DataSet** に追加した場合、そのテーブルの名前は既定のテーブル名 Table*N* になります。この既定名は Table0 に相当する "Table" から始まり、連続する番号が割り当てられていきます。  
  
> [!NOTE]
> **TableName** の値を指定するときは、"Table*N*" の命名規則を使用しないことをお勧めします。これは、指定した名前が **DataSet** に既に存在する既定のテーブル名と競合しないようにするためです。 指定した名前が既に存在する場合は、例外がスローされます。  
  
 次の例では、**DataTable** オブジェクトのインスタンスを作成し、"Customers" という名前を割り当てます。  
  
```vb  
Dim workTable as DataTable = New DataTable("Customers")  
```  
  
```csharp  
DataTable workTable = new DataTable("Customers");  
```  
  
 次の例では、**DataTable** のインスタンスを作成し、**DataSet** の **Tables** コレクションに追加します。  
  
```vb  
Dim customers As DataSet = New DataSet  
Dim customersTable As DataTable = _  
   customers.Tables.Add("CustomersTable")  
```  
  
```csharp  
DataSet customers = new DataSet();  
DataTable customersTable = customers.Tables.Add("CustomersTable");  
```  
  
## <a name="see-also"></a>関連項目

- <xref:System.Data.DataTable>
- <xref:System.Data.DataTableCollection>
- [DataTables](datatables.md)
- [DataAdapter からの DataSet の読み込み](../populating-a-dataset-from-a-dataadapter.md)
- [XML からの DataSet の読み込み](loading-a-dataset-from-xml.md)
- [XML の DataSet スキーマ情報の読み込み](loading-dataset-schema-information-from-xml.md)
- [ADO.NET の概要](../ado-net-overview.md)
