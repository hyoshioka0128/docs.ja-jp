---
title: N 層アプリケーションでのデータ取得および CUD 操作 (LINQ to SQL)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: c3133d53-83ed-4a4d-af8b-82edcf3831db
ms.openlocfilehash: 5ab829993b8f8faa6dcb91d3f23e8442b8aa95bd
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79148414"
---
# <a name="data-retrieval-and-cud-operations-in-n-tier-applications-linq-to-sql"></a>N 層アプリケーションでのデータ取得および CUD 操作 (LINQ to SQL)
Customers または Orders のようなエンティティ オブジェクトをネットワークを介してクライアントにシリアル化すると、これらのエンティティはデータ コンテキストからデタッチされます。 変更内容、および他のオブジェクトとの関連付けはデータ コンテキストによって追跡されなくなります。 クライアントがデータを読み取るだけの場合は、これは問題にはなりません。 また、クライアントが新しい行をデータベースに追加できるようにすることも、ある程度簡単です。 しかし、アプリケーションでクライアントによるデータの更新または削除を可能にする必要がある場合には、<xref:System.Data.Linq.DataContext.SubmitChanges%2A?displayProperty=nameWithType> を呼び出す前に、新しいデータ コンテキストにエンティティをアタッチする必要があります。 さらに、元の値によるオプティミスティック コンカレンシーチェックを使用する場合には、何らかの方法で、元のエンティティと変更後のエンティティをデータベースに渡す必要もあります。 エンティティがデタッチされた後に新しいデータ コンテキストにエンティティを入れるために、`Attach` メソッドが用意されています。  
  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] エンティティの代わりにプロキシ オブジェクトをシリアル化する場合でも、データベースにデータを送るには、データ アクセス層 (DAL) 上にエンティティを構築して、新しい <xref:System.Data.Linq.DataContext?displayProperty=nameWithType> にそれをアタッチする必要があります。  
  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] は、エンティティがどのようにシリアル化されるかについてはまったく関与しません。 Windows Communication Foundation (WCF) を使ってシリアル化できるクラスを、オブジェクト リレーショナル デザイナーと SQLMetal ツールを使用して生成する方法について詳しくは、「[方法: エンティティをシリアル化可能にする](how-to-make-entities-serializable.md)」をご覧ください。  
  
> [!NOTE]
> `Attach` メソッドは、新しいエンティティまたは逆シリアル化されたエンティティに対してのみ呼び出してください。 エンティティを元のデータ コンテキストからデタッチする唯一の方法は、シリアル化です。 デタッチされていないエンティティを新しいデータ コンテキストにアタッチしようとした場合、元のデータ コンテキストの遅延ローダーがそのエンティティにまだ存在するならば、[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] は例外をスローします。 2 つの異なるデータ コンテキストの遅延ローダーを持つエンティティに対して、挿入、更新、および削除操作を実行すると、予想外の結果が生じる可能性があります。 遅延ローダーについて詳しくは、「[遅延読み込みと即時読み込み](deferred-versus-immediate-loading.md)」をご覧ください。  
  
## <a name="retrieving-data"></a>データの取得  
  
### <a name="client-method-call"></a>クライアントのメソッド呼び出し  
 Windows フォーム クライアントから DAL に対するメソッド呼び出しの例を以下に示します。 この例では、DAL は Windows サービス ライブラリとして実装されています。  
  
```vb  
Private Function GetProdsByCat_Click(ByVal sender As Object, ByVal e _  
    As EventArgs)  
  
    ' Create the WCF client proxy.  
    Dim proxy As New NorthwindServiceReference.Service1Client  
  
    ' Call the method on the service.  
    Dim products As NorthwindServiceReference.Product() = _  
        proxy.GetProductsByCategory(1)  
  
    ' If the database uses original values for concurrency checks,  
    ' the client needs to store them and pass them back to the  
    ' middle tier along with the new values when updating data.  
  
    For Each v As NorthwindClient1.NorthwindServiceReference.Product _  
        In products  
        ' Persist to a List(Of Product) declared at class scope.  
        ' Additional change-tracking logic is the responsibility  
        ' of the presentation tier and/or middle tier.  
        originalProducts.Add(v)  
    Next  
  
    ' (Not shown) Bind the products list to a control  
    ' and/or perform whatever processing is necessary.  
End Function  
```  
  
```csharp  
private void GetProdsByCat_Click(object sender, EventArgs e)  
{  
    // Create the WCF client proxy.  
    NorthwindServiceReference.Service1Client proxy =
    new NorthwindClient.NorthwindServiceReference.Service1Client();  
  
    // Call the method on the service.  
    NorthwindServiceReference.Product[] products =
    proxy.GetProductsByCategory(1);  
  
    // If the database uses original values for concurrency checks,
    // the client needs to store them and pass them back to the
    // middle tier along with the new values when updating data.  
    foreach (var v in products)  
    {  
        // Persist to a list<Product> declared at class scope.  
        // Additional change-tracking logic is the responsibility  
        // of the presentation tier and/or middle tier.  
        originalProducts.Add(v);  
    }  
  
    // (Not shown) Bind the products list to a control  
    // and/or perform whatever processing is necessary.  
    }  
```  
  
### <a name="middle-tier-implementation"></a>中間層での実装  
 次の例は、中間層でのインターフェイス メソッドの実装を示しています。 ここでは、次の 2 つの点が重要です。  
  
- <xref:System.Data.Linq.DataContext> はメソッドのスコープで宣言されます。  
  
- メソッドは、実際の結果から成る <xref:System.Collections.IEnumerable> コレクションを返します。 シリアライザーは、結果をクライアント/プレゼンテーション層に戻すためのクエリを実行します。 中間層でクエリ結果にローカルにアクセスするには、クエリ変数に対して `ToList` または `ToArray` を呼び出すことで、実行を強制できます。 その後、そのリストまたは配列を `IEnumerable` として返すことができます。  
  
```vb  
Public Function GetProductsByCategory(ByVal categoryID As Integer) _  
    As IEnumerable(Of Product)  
  
    Dim db As New NorthwindClasses1DataContext(connectionString)  
    Dim productQuery = _  
    From prod In db.Products _  
    Where prod.CategoryID = categoryID _  
    Select prod  
  
    Return productQuery.AsEnumerable()  
  
End Function  
```  
  
```csharp  
public IEnumerable<Product> GetProductsByCategory(int categoryID)  
{  
    NorthwindClasses1DataContext db =
    new NorthwindClasses1DataContext(connectionString);  
  
    IEnumerable<Product> productQuery =  
    from prod in db.Products  
    where prod.CategoryID == categoryID  
    select prod;  
  
    return productQuery.AsEnumerable();
}  
```  
  
 データ コンテキストの 1 つのインスタンスの有効期間は、1 つの「作業単位」である必要があります。 疎結合環境では、通常、作業単位は小さく、たとえば `SubmitChanges` の 1 つの呼び出しを含む単一のオプティミスティック トランザクションです。 このため、データ コンテキストはメソッドのスコープ内で作成されて破棄されます。 作業単位にビジネス ルール ロジックの呼び出しが含まれる場合、通常は、その操作全体のために `DataContext` インスタンスを保持する必要が生じます。 いずれにしても、`DataContext` インスタンスの有効期間は、多数のトランザクションにわたって長い時間になることが意図されていません。  
  
 このメソッドは Product オブジェクトを返しますが、各 Product に関連付けられた Order_Detail オブジェクトのコレクションを返しません。 この既定の動作を変更するには、<xref:System.Data.Linq.DataLoadOptions> オブジェクトを使用します。 詳細については、[取得する関連データの量を制御する](how-to-control-how-much-related-data-is-retrieved.md)」をご覧ください。  
  
## <a name="inserting-data"></a>データの挿入  
 新しいオブジェクトを挿入するために、プレゼンテーション層は単に中間層インターフェイス上の関連するメソッドを呼び出して、挿入対象の新しいオブジェクトを渡します。 ただし、クライアントがいくつかの値だけを渡して、オブジェクト全体の構築を中間層に任せた方が効率的である場合もあります。  
  
### <a name="middle-tier-implementation"></a>中間層での実装  
 中間層で、新しい <xref:System.Data.Linq.DataContext> が作成され、<xref:System.Data.Linq.DataContext> メソッドを使ってオブジェクトが <xref:System.Data.Linq.Table%601.InsertOnSubmit%2A> にアタッチされて、<xref:System.Data.Linq.DataContext.SubmitChanges%2A> の呼び出し時にオブジェクトが挿入されます。 他の Web サービスのシナリオとまったく同じ方法で、例外、コールバック、エラー状態を処理できます。  
  
```vb  
' No call to Attach is necessary for inserts.  
Public Sub InsertOrder(ByVal o As Order)  
  
    Dim db As New NorthwindClasses1DataContext(connectionString)  
    db.Orders.InsertOnSubmit(o)  
  
    ' Exception handling not shown.  
    db.SubmitChanges()  
  
End Sub  
```  
  
```csharp  
// No call to Attach is necessary for inserts.  
    public void InsertOrder(Order o)  
    {  
        NorthwindClasses1DataContext db = new NorthwindClasses1DataContext(connectionString);  
        db.Orders.InsertOnSubmit(o);  
  
        // Exception handling not shown.  
        db.SubmitChanges();  
    }  
```  
  
## <a name="deleting-data"></a>データの削除  
 既存のオブジェクトをデータベースから削除するために、プレゼンテーション層は中間層インターフェイス上の関連するメソッドを呼び出して、削除対象のオブジェクトの元の値を含むコピーを渡します。  
  
 削除操作ではオプティミスティック コンカレンシー チェックが行われて、削除対象のオブジェクトを新しいデータ コンテキストに最初にアタッチする必要があります。 この例では、オブジェクトにタイムスタンプ (RowVersion) が含まれないことを示すために `Boolean` パラメーターが `false` に設定されます。 各レコードのタイムスタンプがデータベース テーブルで生成される場合には、コンカレンシー チェックは特にクライアントにとって非常に簡単です。 元のオブジェクトまたは変更後のオブジェクトを渡して、`Boolean` パラメーターを `true` に設定するだけです。 いずれの場合も、中間層では、通常、<xref:System.Data.Linq.ChangeConflictException> をキャッチする必要があります。 オプティミスティック コンカレンシーの競合を処理する方法について詳しくは、「[オプティミスティック コンカレンシー: 概要)](optimistic-concurrency-overview.md) の下のステートメントを右クリックします。  
  
 関連するテーブルに対する外部キー制約を含むエンティティを削除する際には、<xref:System.Data.Linq.EntitySet%601> コレクション内のすべてのオブジェクトを最初に削除する必要があります。  
  
```vb  
' Attach is necessary for deletes.  
Public Sub DeleteOrder(ByVal order As Order)  
    Dim db As New NorthwindClasses1DataContext(connectionString)  
  
    db.Orders.Attach(order, False)  
    ' This will throw an exception if the order has order details.  
    db.Orders.DeleteOnSubmit(order)  
  
    Try  
        ' ConflictMode is an optional parameter.  
        db.SubmitChanges(ConflictMode.ContinueOnConflict)  
  
    Catch ex As ChangeConflictException  
        ' Get conflict information, and take actions  
        ' that are appropriate for your application.  
        ' See MSDN Article "How to: Manage Change  
        ' Conflicts (LINQ to SQL).  
  
    End Try  
End Sub  
```  
  
```csharp  
// Attach is necessary for deletes.  
public void DeleteOrder(Order order)  
{  
    NorthwindClasses1DataContext db = new NorthwindClasses1DataContext(connectionString);  
  
    db.Orders.Attach(order, false);  
    // This will throw an exception if the order has order details.  
    db.Orders.DeleteOnSubmit(order);  
    try  
    {  
        // ConflictMode is an optional parameter.  
        db.SubmitChanges(ConflictMode.ContinueOnConflict);  
    }  
    catch (ChangeConflictException e)  
    {  
       // Get conflict information, and take actions  
       // that are appropriate for your application.  
       // See MSDN Article How to: Manage Change Conflicts (LINQ to SQL).  
    }  
}  
```  
  
## <a name="updating-data"></a>データの更新  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] は、オプティミスティック コンカレンシーを行う次のようなシナリオでの更新をサポートします。  
  
- タイムスタンプつまり RowVersion 番号に基づくオプティミスティック コンカレンシー。  
  
- エンティティ プロパティのサブセットの元の値に基づくオプティミスティック コンカレンシー。  
  
- 元のエンティティ全体および変更後のエンティティ全体に基づくオプティミスティック コンカレンシー。  
  
 また、エンティティとそのリレーションシップの両方に対して更新または削除を実行することもできます (たとえば Customer と、それに関連した Order オブジェクトのコレクション)。 エンティティ オブジェクトとその子 (`EntitySet`) コレクションから成るグラフをクライアント上で変更して、オプティミスティック コンカレンシー チェックで元の値が必要とされる場合には、クライアントはそれぞれのエンティティと <xref:System.Data.Linq.EntitySet%601> オブジェクトの元の値を提供する必要があります。 1 つのメソッド呼び出しで互いに関連する更新、削除、挿入のセットをクライアントが実行できるようにするには、各エンティティにどんな操作を実行するかを示す方法をクライアントに提供する必要があります。 その後、中間層で適切な <xref:System.Data.Linq.ITable.Attach%2A> メソッドを呼び出した後、<xref:System.Data.Linq.ITable.InsertOnSubmit%2A> を呼び出す前に、各エンティティに対して <xref:System.Data.Linq.ITable.DeleteAllOnSubmit%2A>, <xref:System.Data.Linq.Table%601.InsertOnSubmit%2A> または `Attach` (挿入の場合は <xref:System.Data.Linq.DataContext.SubmitChanges%2A> 無し) を呼び出す必要があります。 更新を試行する前に元の値を入手するためにデータベースからデータを取得しないでください。  
  
 オプティミスティック コンカレンシーについて詳しくは、「[オプティミスティック コンカレンシー: 概要)](optimistic-concurrency-overview.md) の下のステートメントを右クリックします。 オプティミスティック コンカレンシーの変更の競合を解決する方法について、詳しくは「[方法: 変更の競合を管理する](how-to-manage-change-conflicts.md)」をご覧ください。  
  
 それぞれのシナリオの例を以下に示します。  
  
### <a name="optimistic-concurrency-with-timestamps"></a>タイムスタンプを使用したオプティミスティック コンカレンシー  
  
```vb  
' Assume that "customer" has been sent by client.  
' Attach with "true" to say this is a modified entity  
' and it can be checked for optimistic concurrency  
' because it has a column that is marked with the  
' "RowVersion" attribute.  
  
db.Customers.Attach(customer, True)  
  
Try  
    ' Optional: Specify a ConflictMode value  
    ' in call to SubmitChanges.  
    db.SubmitChanges()  
Catch ex As ChangeConflictException  
    ' Handle conflict based on options provided.  
    ' See MSDN article "How to: Manage Change  
    ' Conflicts (LINQ to SQL)".  
End Try  
```  
  
```csharp  
// Assume that "customer" has been sent by client.  
// Attach with "true" to say this is a modified entity  
// and it can be checked for optimistic concurrency because  
//  it has a column that is marked with "RowVersion" attribute  
db.Customers.Attach(customer, true)  
try  
{  
    // Optional: Specify a ConflictMode value  
    // in call to SubmitChanges.  
    db.SubmitChanges();  
}  
catch(ChangeConflictException e)  
{  
    // Handle conflict based on options provided  
    // See MSDN article How to: Manage Change Conflicts (LINQ to SQL).  
}  
```  
  
### <a name="with-subset-of-original-values"></a>元の値のサブセットを使用した場合  
 この手法では、クライアントは変更対象の値と共に、シリアル化されたオブジェクト全体を返します。  
  
```vb  
Public Sub UpdateProductInventory(ByVal p As Product, ByVal _  
    unitsInStock As Short?, ByVal unitsOnOrder As Short?)  
  
    Using db As New NorthwindClasses1DataContext(connectionString)  
        ' p is the original unmodified product  
        ' that was obtained from the database.  
        ' The client kept a copy and returns it now.  
        db.Products.Attach(p, False)  
  
        ' Now that the original values are in the data context,  
        ' apply the changes.  
        p.UnitsInStock = unitsInStock  
        p.UnitsOnOrder = unitsOnOrder  
  
        Try  
            ' Optional: Specify a ConflictMode value  
            ' in call to SubmitChanges.  
            db.SubmitChanges()  
  
        Catch ex As Exception  
            ' Handle conflict based on options provided.  
            ' See MSDN article "How to: Manage Change Conflicts  
            ' (LINQ to SQL)".  
        End Try  
    End Using  
End Sub  
```  
  
```csharp  
public void UpdateProductInventory(Product p, short? unitsInStock, short? unitsOnOrder)  
{  
    using (NorthwindClasses1DataContext db = new NorthwindClasses1DataContext(connectionString))  
    {  
        // p is the original unmodified product  
        // that was obtained from the database.  
        // The client kept a copy and returns it now.  
        db.Products.Attach(p, false);  
  
        // Now that the original values are in the data context, apply the changes.  
        p.UnitsInStock = unitsInStock;  
        p.UnitsOnOrder = unitsOnOrder;  
        try  
        {  
             // Optional: Specify a ConflictMode value  
             // in call to SubmitChanges.  
             db.SubmitChanges();  
        }  
        catch (ChangeConflictException e)  
        {  
            // Handle conflict based on provided options.  
            // See MSDN article How to: Manage Change Conflicts  
            // (LINQ to SQL).  
        }  
    }  
}  
```  
  
### <a name="with-complete-entities"></a>エンティティ全体を使用する場合  
  
```vb  
Public Sub UpdateProductInfo(ByVal newProd As Product, ByVal _  
    originalProd As Product)  
  
    Using db As New NorthwindClasses1DataContext(connectionString)  
        db.Products.Attach(newProd, originalProd)  
  
        Try  
            ' Optional: Specify a ConflictMode value  
            ' in call to SubmitChanges.  
            db.SubmitChanges()  
  
        Catch ex As Exception  
            ' Handle potential change conflicgt in whatever way  
            ' is appropriate for your application.  
            ' For more information, see the MSDN article  
            ' "How to: Manage Change Conflicts (LINQ to  
            ' SQL)".  
        End Try  
  
    End Using  
End Sub  
```  
  
```csharp  
public void UpdateProductInfo(Product newProd, Product originalProd)  
{  
     using (NorthwindClasses1DataContext db = new  
        NorthwindClasses1DataContext(connectionString))  
     {  
         db.Products.Attach(newProd, originalProd);  
         try  
         {  
               // Optional: Specify a ConflictMode value  
               // in call to SubmitChanges.  
               db.SubmitChanges();  
         }  
        catch (ChangeConflictException e)  
        {  
            // Handle potential change conflict in whatever way  
            // is appropriate for your application.  
            // For more information, see the MSDN article  
            // How to: Manage Change Conflicts (LINQ to SQL)/  
        }
    }  
}  
```  
  
 コレクションを更新するには、<xref:System.Data.Linq.ITable.AttachAll%2A> ではなく `Attach` を呼び出します。  
  
### <a name="expected-entity-members"></a>必要なエンティティ メンバー  
 既に説明したように、`Attach` メソッドを呼び出す前に設定する必要があるのは、エンティティ オブジェクトのいくつかのメンバーだけです。 設定する必要のあるエンティティ メンバーは、次の条件を満たす必要があります。  
  
- エンティティの ID の一部分である。  
  
- 変更される予定である。  
  
- タイムスタンプであるか、<xref:System.Data.Linq.Mapping.ColumnAttribute.UpdateCheck%2A> 属性が `Never` 以外の値に設定されている。  
  
 テーブルでオプティミスティック コンカレンシー チェック用にタイムスタンプまたはバージョン番号を使用している場合は、<xref:System.Data.Linq.ITable.Attach%2A> を呼び出す前にこれらのメンバーを設定する必要があります。 Column 属性の <xref:System.Data.Linq.Mapping.ColumnAttribute.IsVersion%2A> プロパティが true に設定されている場合、メンバーはオプティミスティック コンカレンシー チェック専用です。 要求された更新は、データベース上のバージョン番号またはタイムスタンプ値が同じ場合にのみ、送信されます。  
  
 また、<xref:System.Data.Linq.Mapping.ColumnAttribute.UpdateCheck%2A> が `Never` に設定されていないメンバーもまた、オプティミスティック コンカレンシー チェックに使用されます。 他の値が指定されない場合、既定値は `Always` です。  
  
 これらの必要なメンバーのいずれかが欠落している場合、<xref:System.Data.Linq.ChangeConflictException> 中に <xref:System.Data.Linq.DataContext.SubmitChanges%2A> ("行が見つからないか変更されています") がスローされます。  
  
### <a name="state"></a>状態  
 エンティティ オブジェクトが <xref:System.Data.Linq.DataContext> インスタンスにアタッチされた後、そのオブジェクトは `PossiblyModified` 状態にあると見なされます。 アタッチされたオブジェクトを強制的に `Modified` 状態にする方法は、3 つあります。  
  
1. 未変更としてアタッチした後、フィールドを直接変更する。  
  
2. 現在のオブジェクト インスタンスと元のオブジェクト インスタンスを受け入れる <xref:System.Data.Linq.Table%601.Attach%2A> オーバーロードを使ってアタッチする。 こうすると、古い値と新しい値が変更トラッカーに提供されるため、変更されたフィールドが自動的に判別されます。  
  
3. (true に設定された) 2 番目のブール値パラメーターを受け入れる <xref:System.Data.Linq.Table%601.Attach%2A> オーバーロードを使ってアタッチする。 こうすると、元の値を提供しなくても、変更トラッカーはオブジェクトが変更済みと見なします。 この手法では、オブジェクトにバージョン/タイムスタンプ フィールドが含まれる必要があります。  
  
 詳しくは、「[オブジェクトの状態と変更の追跡](object-states-and-change-tracking.md)」をご覧ください。  
  
 アタッチ対象のオブジェクトと同じ ID を持つエンティティ オブジェクトが ID キャッシュ内に既に存在する場合、<xref:System.Data.Linq.DuplicateKeyException> がスローされます。  
  
 オブジェクトの `IEnumerable` セットを使ってアタッチするとき、既存のキーが含まれる場合には、<xref:System.Data.Linq.DuplicateKeyException> がスローされます。 残りのオブジェクトはアタッチされません。  
  
## <a name="see-also"></a>関連項目

- [LINQ to SQL を使用する n 層アプリケーションとリモート アプリケーション](n-tier-and-remote-applications-with-linq-to-sql.md)
- [背景情報](background-information.md)
