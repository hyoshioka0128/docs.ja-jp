---
title: クエリ結果のページング
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: fa360c46-e5f8-411e-a711-46997771133d
ms.openlocfilehash: 2e7fb97e5c0cb42deff43c411f47e8d30e2257ef
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79149389"
---
# <a name="paging-through-a-query-result"></a>クエリ結果のページング
クエリ結果のページングとは、クエリ結果をデータの小さなサブセット、つまりページに分けて返すプロセスです。 クエリ結果のページングは、結果を管理しやすい小さな単位でユーザーに表示するために行われる一般的な処理です。  
  
 **DataAdapter** には、**Fill** メソッドのオーバーロードを通じて、1 ページ分のデータだけを返す機能が用意されています。 しかしこれは大きなクエリ結果のページングには適していません。**DataAdapter** が目的の <xref:System.Data.DataTable> または <xref:System.Data.DataSet> に、要求されたレコードだけを格納する一方で、クエリ全体を返すためのリソースが使用されるためです。 クエリ全体を返す必要があるリソースを使用せずにデータ ソースから 1 ページ分のデータを返すには、必要な行だけ返すように限定する抽出条件をクエリに追加します。  
  
 **Fill** メソッドを使用して 1 ページ分のデータを返すには、データ ページの先頭レコードを指定する **startRecord** パラメーターおよびデータ ページのレコード数を指定する **maxRecords** パラメーターを指定します。  
  
 **Fill** メソッドを使用してクエリ結果の最初のページ (ページ サイズは 5 レコード) を返す方法のコード例を次に示します。  
  
```vb  
Dim currentIndex As Integer = 0  
Dim pageSize As Integer = 5  
  
Dim orderSQL As String = "SELECT * FROM dbo.Orders ORDER BY OrderID"  
' Assumes that connection is a valid SqlConnection object.  
Dim adapter As SqlDataAdapter = _  
  New SqlDataAdapter(orderSQL, connection)  
  
Dim dataSet As DataSet = New DataSet()  
adapter.Fill(dataSet, currentIndex, pageSize, "Orders")  
```  
  
```csharp  
int currentIndex = 0;  
int pageSize = 5;  
  
string orderSQL = "SELECT * FROM Orders ORDER BY OrderID";  
// Assumes that connection is a valid SqlConnection object.  
SqlDataAdapter adapter = new SqlDataAdapter(orderSQL, connection);  
  
DataSet dataSet = new DataSet();  
adapter.Fill(dataSet, currentIndex, pageSize, "Orders");  
```  
  
 上の例では、**DataSet** に 5 つのレコードだけが格納されますが、**Orders** テーブル全体が返されます。 **DataSet** にこれと同じ 5 つのレコードを格納し、5 つのレコードだけを返すには、次のコード サンプルに示すように SQL ステートメントで TOP 句と WHERE 句を使用します。  
  
```vb  
Dim pageSize As Integer = 5  
  
Dim orderSQL As String = "SELECT TOP " & pageSize & _  
  " * FROM Orders ORDER BY OrderID"  
Dim adapter As SqlDataAdapter = _  
  New SqlDataAdapter(orderSQL, connection)  
  
Dim dataSet As DataSet = New DataSet()  
adapter.Fill(dataSet, "Orders")
```  
  
```csharp  
int pageSize = 5;  
  
string orderSQL = "SELECT TOP " + pageSize +
  " * FROM Orders ORDER BY OrderID";  
SqlDataAdapter adapter = new SqlDataAdapter(orderSQL, connection);  
  
DataSet dataSet = new DataSet();  
adapter.Fill(dataSet, "Orders");  
```  
  
 この方法でクエリ結果をページングするときは、次のレコード ページを返すコマンドに一意の ID を渡すために、行を順序付けする固有の識別子を保存する必要があります。次のコード サンプルで示します。  
  
```vb  
Dim lastRecord As String = _  
  dataSet.Tables("Orders").Rows(pageSize - 1)("OrderID").ToString()  
```  
  
```csharp  
string lastRecord =
  dataSet.Tables["Orders"].Rows[pageSize - 1]["OrderID"].ToString();  
```  
  
 **startRecord** パラメーターと **maxRecords** パラメーターを受け取る **Fill** メソッドのオーバーロードを使用して次のレコード ページを返すには、現在のレコード インデックスをページ サイズの分だけインクリメントし、テーブルにレコード ページを格納します。 **DataSet** に 1 ページ分のレコードだけを追加する場合でも、データベース サーバーはクエリ結果全体を返すことに注意してください。 次のデータ ページを格納する前にテーブル行をクリアするコード サンプルを次に示します。 データベース サーバーとのやり取りを減らすために、ローカルのキャッシュに、返された一定数の行を保存することもできます。  
  
```vb  
currentIndex = currentIndex + pageSize  
  
dataSet.Tables("Orders").Rows.Clear()  
  
adapter.Fill(dataSet, currentIndex, pageSize, "Orders")  
```  
  
```csharp  
currentIndex += pageSize;  
  
dataSet.Tables["Orders"].Rows.Clear();  
  
adapter.Fill(dataSet, currentIndex, pageSize, "Orders");  
```  
  
 データベース サーバーによってクエリ全体を返さずに次のレコード ページを返すには、SELECT ステートメントに限定的な抽出条件を指定します。 上の例では最後に返されたレコードが保存されますが、次のコード サンプルに示すようにそのレコードを WHERE 句で使用するとクエリの開始点を指定できます。  
  
```vb  
orderSQL = "SELECT TOP " & pageSize & _  
  " * FROM Orders WHERE OrderID > " & lastRecord & " ORDER BY OrderID"  
adapter.SelectCommand.CommandText = orderSQL  
  
dataSet.Tables("Orders").Rows.Clear()  
  
adapter.Fill(dataSet, "Orders")  
```  
  
```csharp  
orderSQL = "SELECT TOP " + pageSize +
  " * FROM Orders WHERE OrderID > " + lastRecord + " ORDER BY OrderID";  
adapter.SelectCommand.CommandText = orderSQL;  
  
dataSet.Tables["Orders"].Rows.Clear();  
  
adapter.Fill(dataSet, "Orders");  
```  
  
## <a name="see-also"></a>関連項目

- [DataAdapter と DataReader](dataadapters-and-datareaders.md)
- [ADO.NET の概要](ado-net-overview.md)
