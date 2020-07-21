---
title: クエリによる DataTable の作成 (LINQ to DataSet)
description: CopyToDataTable メソッドを使用してクエリの結果を取得し、そのデータを DataTable にコピーして、データ バインディングに使用する方法について説明します。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 1b97afeb-03f8-41e2-8eb3-58aff65f7d18
ms.openlocfilehash: 0a7c8f005b90484ef2f9c7e48218bda40533696a
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84287013"
---
# <a name="creating-a-datatable-from-a-query-linq-to-dataset"></a>クエリによる DataTable の作成 (LINQ to DataSet)
<xref:System.Data.DataTable> オブジェクトの一般的な利用法の 1 つが、データ バインディングです。 <xref:System.Data.DataTableExtensions.CopyToDataTable%2A> メソッドは、クエリの結果を受け取り、そのデータを <xref:System.Data.DataTable> にコピーします。これをデータ バインディングに利用できます。 このデータ操作が実行されると、新しい <xref:System.Data.DataTable> が、基となった <xref:System.Data.DataTable> にマージ バックされます。  
  
 <xref:System.Data.DataTableExtensions.CopyToDataTable%2A> メソッドでは、次の処理を実行することでクエリの結果から <xref:System.Data.DataTable> を作成します。  
  
1. <xref:System.Data.DataTableExtensions.CopyToDataTable%2A> メソッドにより、ソース テーブル (<xref:System.Data.DataTable> インターフェイスを実装する <xref:System.Data.DataTable> オブジェクト) から <xref:System.Linq.IQueryable%601> を複製します。 通常、<xref:System.Collections.IEnumerable> ソースは LINQ to DataSet 式またはメソッド クエリから生成されます。  
  
2. 複製の <xref:System.Data.DataTable> のスキーマは、ソース テーブルで最初に列挙されている <xref:System.Data.DataRow> オブジェクトの列から作成されます。複製したテーブルの名前は、ソース テーブルの名前に "query" という単語を付加した名前になります。  
  
3. ソース テーブルの各行について、行の内容が新しい <xref:System.Data.DataRow> オブジェクトにコピーされた後、それが複製のテーブルに挿入されます。 このコピー操作の間、<xref:System.Data.DataRow.RowState%2A> プロパティと <xref:System.Data.DataRow.RowError%2A> プロパティは保持されます。 基になる <xref:System.ArgumentException> オブジェクトが別々のテーブルに由来している場合、<xref:System.Data.DataRow> がスローされます。  
  
4. クエリ実行可能な入力テーブルの <xref:System.Data.DataTable> オブジェクトがすべてコピーされた後、複製の <xref:System.Data.DataRow> が返されます。 基となるシーケンスに <xref:System.Data.DataRow> オブジェクトが含まれていない場合、このメソッドは空の <xref:System.Data.DataTable> を返します。  
  
<xref:System.Data.DataTableExtensions.CopyToDataTable%2A> メソッドを呼び出すと、ソース テーブルにバインドされているクエリが実行されます。  
  
 <xref:System.Data.DataTableExtensions.CopyToDataTable%2A> メソッドにより、ソース テーブルの行に Null 参照または Null 許容の値型が検出された場合、その値は <xref:System.DBNull.Value> に置き換えられます。 このようにして、返される <xref:System.Data.DataTable> の Null 値が適切に処理されます。  
  
 メモ:<xref:System.Data.DataTableExtensions.CopyToDataTable%2A> メソッドは、複数の <xref:System.Data.DataTable> オブジェクトまたは <xref:System.Data.DataSet> オブジェクトから行を返せるクエリを入力として受け入れます。 <xref:System.Data.DataTableExtensions.CopyToDataTable%2A> メソッドは、ソースの <xref:System.Data.DataTable> または <xref:System.Data.DataSet> オブジェクトから、返された <xref:System.Data.DataTable> にデータをコピーしますが、プロパティはコピーしません。 <xref:System.Data.DataTable> や <xref:System.Data.DataTable.Locale%2A> などの返された <xref:System.Data.DataTable.TableName%2A> に、明示的にプロパティを設定する必要があります。  
  
 次の例では、SalesOrderHeader テーブルに対して 2001 年 8 月 8 日以降の注文をクエリし、<xref:System.Data.DataTableExtensions.CopyToDataTable%2A> メソッドを使用して、このクエリから <xref:System.Data.DataTable> を作成します。 次に、<xref:System.Data.DataTable> が <xref:System.Windows.Forms.BindingSource> にバインドされます。これは <xref:System.Windows.Forms.DataGridView> のプロキシとして機能します。  
  
 [!code-csharp[DP LINQ to DataSet Examples#CopyToDataTable1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#copytodatatable1)]
 [!code-vb[DP LINQ to DataSet Examples#CopyToDataTable1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#copytodatatable1)]  
  
## <a name="creating-a-custom-copytodatatablet-method"></a>カスタム CopyToDataTable\<T> メソッドの作成  
 既存の <xref:System.Data.DataTableExtensions.CopyToDataTable%2A> メソッドは、ジェネリック パラメーター <xref:System.Collections.Generic.IEnumerable%601> が `T` 型である <xref:System.Data.DataRow> ソースに対してのみ作用します。 有用ではありますが、一連のスカラー型、匿名型を返すクエリ、またはテーブルの結合を実行するクエリからは、テーブルを作成できません。 一連のスカラー型または匿名型からテーブルを読み込む 2 つのカスタム `CopyToDataTable` メソッドの実装例については、「[方法: ジェネリック型 T が DataRow](implement-copytodatatable-where-type-not-a-datarow.md) ではない CopyToDataTable\<T> を実装する」を参照してください。  
  
 このセクションの例には、次のカスタム型が使用されています。  
  
 [!code-csharp[DP Custom CopyToDataTable Examples#ItemClass](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP Custom CopyToDataTable Examples/CS/Program.cs#itemclass)]
 [!code-vb[DP Custom CopyToDataTable Examples#ItemClass](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP Custom CopyToDataTable Examples/VB/Module1.vb#itemclass)]  
  
### <a name="example"></a>例  
 この例では、`SalesOrderHeader` テーブルと `SalesOrderDetail` テーブルを結合し、8 月以降のオンラインでの注文を取得して、クエリからテーブルを作成します。  
  
 [!code-csharp[DP Custom CopyToDataTable Examples#Join](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP Custom CopyToDataTable Examples/CS/Program.cs#join)]
 [!code-vb[DP Custom CopyToDataTable Examples#Join](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP Custom CopyToDataTable Examples/VB/Module1.vb#join)]  
  
### <a name="example"></a>例  
 次の例では、価格が $9.99 を超える一連の商品を照会し、そのクエリの結果からテーブルを作成します。  
  
 [!code-csharp[DP Custom CopyToDataTable Examples#LoadItemsIntoTable](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP Custom CopyToDataTable Examples/CS/Program.cs#loaditemsintotable)]
 [!code-vb[DP Custom CopyToDataTable Examples#LoadItemsIntoTable](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP Custom CopyToDataTable Examples/VB/Module1.vb#loaditemsintotable)]  
  
### <a name="example"></a>例  
 次の例では、価格が $9.99 を超える一連の商品を照会し、その結果を射影します。 返された一連の匿名型は、既存のテーブルに読み込まれます。  
  
 [!code-csharp[DP Custom CopyToDataTable Examples#LoadItemsIntoExistingTable](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP Custom CopyToDataTable Examples/CS/Program.cs#loaditemsintoexistingtable)]
 [!code-vb[DP Custom CopyToDataTable Examples#LoadItemsIntoExistingTable](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP Custom CopyToDataTable Examples/VB/Module1.vb#loaditemsintoexistingtable)]  
  
### <a name="example"></a>例  
 次の例では、価格が $9.99 を超える一連の商品を照会し、その結果を射影します。 返された一連の匿名型は、既存のテーブルに読み込まれます。 `Book` 型と `Movies` 型は `Item` 型から派生するため、テーブル スキーマは自動的に展開されます。  
  
 [!code-csharp[DP Custom CopyToDataTable Examples#LoadItemsExpandSchema](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP Custom CopyToDataTable Examples/CS/Program.cs#loaditemsexpandschema)]
 [!code-vb[DP Custom CopyToDataTable Examples#LoadItemsExpandSchema](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP Custom CopyToDataTable Examples/VB/Module1.vb#loaditemsexpandschema)]  
  
### <a name="example"></a>例  
 次の例では、価格が $9.99 を超える一連の商品を照会し、新しいテーブルに読み込まれる一連の <xref:System.Double> を返します。  
  
 [!code-csharp[DP Custom CopyToDataTable Examples#LoadScalarSequence](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP Custom CopyToDataTable Examples/CS/Program.cs#loadscalarsequence)]
 [!code-vb[DP Custom CopyToDataTable Examples#LoadScalarSequence](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP Custom CopyToDataTable Examples/VB/Module1.vb#loadscalarsequence)]  
  
## <a name="see-also"></a>関連項目

- [プログラミング ガイド](programming-guide-linq-to-dataset.md)
- [ジェネリック メソッド Field および SetField](generic-field-and-setfield-methods-linq-to-dataset.md)
- [LINQ to DataSet の例](linq-to-dataset-examples.md)
