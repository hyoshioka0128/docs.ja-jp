---
title: ビジネス ロジックの実装 (LINQ to SQL)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: c4577590-7b12-42e1-84a6-95aa2562727e
ms.openlocfilehash: 51b92549a40d0e5121cc390f5dbdf726cc06404b
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79174551"
---
# <a name="implementing-business-logic-linq-to-sql"></a>ビジネス ロジックの実装 (LINQ to SQL)
このトピックの「ビジネス ロジック」とは、データベースでデータを挿入、更新、または削除される前にデータに適用されるカスタム規則または検証テストのことです。 ビジネス ロジックは、「ビジネス ルール」または「ドメイン ロジック」とも呼ばれます。 n 層アプリケーションでは、通常、論理層として設計されるため、プレゼンテーション層やデータ アクセス層から独立して変更できます。 データベースのデータを更新、挿入、または削除する前または後に、データ アクセス層によってビジネス ロジックを呼び出すことができます。  
  
 ビジネス ロジックは、フィールドの型がテーブル列の型と互換性を持つかどうか確認するスキーマ検証のような簡単なものにすることもできます。 または、任意の複雑な方法で相互に影響するオブジェクトのセットから成るビジネス ロジックも可能です。 規則は、データベース上のストアド プロシージャとして、またはメモリ内のオブジェクトとして実装可能です。 ビジネス ロジックの実装方法とは無関係に、[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] では、部分クラスと部分メソッドを使ってビジネス ロジックをデータ アクセス コードから分離することができます。  
  
## <a name="how-linq-to-sql-invokes-your-business-logic"></a>LINQ to SQL でビジネス ロジックを呼び出す方法  
 手動で、またはオブジェクト リレーショナル デザイナーか SQLMetal を使用して、デザイン時にエンティティ クラスを生成すると、部分クラスとして定義されます。 つまり、別個のコード ファイル内で、カスタム ビジネス ロジックを格納するエンティティ クラスの別の部分を定義できます。 コンパイル時に 2 つの部分が 1 つのクラスにマージされます。 ただし、オブジェクト リレーショナル デザイナーまたは SQLMetal を使ってエンティティ クラスを再生成する必要がある場合は、そうしてもかまいません。その場合、開発者が作成したクラスの部分は変更されません。  
  
 エンティティと <xref:System.Data.Linq.DataContext> を定義する部分クラスには、部分メソッドが含まれます。 これらは機能拡張ポイントであり、これらを使用して、エンティティまたはエンティティ プロパティを更新、挿入、削除する前および後にビジネス ロジックを適用できます。 部分メソッドはコンパイル時のイベントのようなものです。 コード ジェネレーターはメソッド シグネチャを定義して、get および set プロパティ アクセサー内、`DataContext` コンストラクター内、および、場合によっては <xref:System.Data.Linq.DataContext.SubmitChanges%2A> 呼び出し時に背後でメソッドを呼び出します。 ただし、特定の部分メソッドを実装しない場合には、そのメソッドのすべての参照と定義はコンパイル時に削除されます。  
  
 別個のコード ファイル内に作成する実装定義では、必要な任意のカスタム ロジックを実行できます。 部分クラス自体をドメイン層として使用できます。または、部分メソッドの実装定義から別個の 1 つ以上のオブジェクトに呼び出すこともできます。 どちらの場合も、ビジネス ロジックはデータ アクセス コードとプレゼンテーション層コードから明確に分離されています。  
  
## <a name="a-closer-look-at-the-extensibility-points"></a>機能拡張ポイントの詳細  
 次の例は、`Customers` と `Orders` の 2 つのテーブルを持つ `DataContext` クラス用にオブジェクト リレーショナル デザイナーによって生成されるコードの一部分です。 このクラスで Insert、Update、および Delete メソッドがテーブルごとに定義されていることに注意してください。  
  
```vb  
Partial Public Class Northwnd  
    Inherits System.Data.Linq.DataContext  
  
    Private Shared mappingSource As _  
        System.Data.Linq.Mapping.MappingSource = New _  
        AttributeMappingSource  
  
    #Region "Extensibility Method Definitions"  
    Partial Private Sub OnCreated()  
    End Sub  
    Partial Private Sub InsertCustomer(instance As Customer)  
    End Sub  
    Partial Private Sub UpdateCustomer(instance As Customer)  
    End Sub  
    Partial Private Sub DeleteCustomer(instance As Customer)  
    End Sub  
    Partial Private Sub InsertOrder(instance As [Order])  
    End Sub  
    Partial Private Sub UpdateOrder(instance As [Order])  
    End Sub  
    Partial Private Sub DeleteOrder(instance As [Order])  
    End Sub  
    #End Region  
```  
  
```csharp  
public partial class MyNorthWindDataContext : System.Data.Linq.DataContext  
    {  
        private static System.Data.Linq.Mapping.MappingSource mappingSource = new AttributeMappingSource();  
  
        #region Extensibility Method Definitions  
        partial void OnCreated();  
        partial void InsertCustomer(Customer instance);  
        partial void UpdateCustomer(Customer instance);  
        partial void DeleteCustomer(Customer instance);  
        partial void InsertOrder(Order instance);  
        partial void UpdateOrder(Order instance);  
        partial void DeleteOrder(Order instance);  
        #endregion  
```  
  
 部分クラス内で Insert、Update、および Delete メソッドを実装すると、[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] ランタイムは <xref:System.Data.Linq.DataContext.SubmitChanges%2A> の呼び出し時に、既定のメソッドの代わりにこれらのメソッドを呼び出します。 こうすることで、作成、読み取り、更新、削除操作の既定の動作をオーバーライドできます。 詳細については、「[チュートリアル:エンティティ クラスの挿入、更新、および削除の動作のカスタマイズ](/visualstudio/data-tools/walkthrough-customizing-the-insert-update-and-delete-behavior-of-entity-classes)」を参照してください。  
  
 `OnCreated` メソッドはクラス コンストラクター内で呼び出されます。  
  
```vb  
Public Sub New(ByVal connection As String)  
    MyBase.New(connection, mappingSource)  
    OnCreated()  
End Sub  
```  
  
```csharp  
public MyNorthWindDataContext(string connection) :  
            base(connection, mappingSource)  
        {  
            OnCreated();  
        }  
```  
  
 エンティティの作成時、読み込み時、および検証時 ([!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] の呼び出し時) に `SubmitChanges` ランタイムによって呼び出される 3 つのメソッドが、エンティティ クラスに含まれています。 さらに、エンティティ クラスには、各プロパティごとの 2 つの部分メソッドも含まれています。このうち 1 つはプロパティの設定前に、もう 1 つは設定後に呼び出されます。 次のコード例は、`Customer` クラス用に生成されるいくつかのメソッドを示しています。  
  
```vb  
#Region "Extensibility Method Definitions"  
    Partial Private Sub OnLoaded()  
    End Sub  
    Partial Private Sub OnValidate(action As _  
        System.Data.Linq.ChangeAction)  
    End Sub  
    Partial Private Sub OnCreated()  
    End Sub  
    Partial Private Sub OnCustomerIDChanging(value As String)  
    End Sub  
    Partial Private Sub OnCustomerIDChanged()  
    End Sub  
    Partial Private Sub OnCompanyNameChanging(value As String)  
    End Sub  
    Partial Private Sub OnCompanyNameChanged()  
    End Sub  
' ...Additional Changing/Changed methods for each property.  
```  
  
```csharp  
#region Extensibility Method Definitions  
    partial void OnLoaded();  
    partial void OnValidate();  
    partial void OnCreated();  
    partial void OnCustomerIDChanging(string value);  
    partial void OnCustomerIDChanged();  
    partial void OnCompanyNameChanging(string value);  
    partial void OnCompanyNameChanged();  
// ...additional Changing/Changed methods for each property  
```  
  
 以下の `CustomerID` プロパティの例に示されるように、メソッドはプロパティの set アクセサー内で呼び出されます。  
  
```vb  
Public Property CustomerID() As String  
    Set  
        If (String.Equals(Me._CustomerID, value) = False) Then  
            Me.OnCustomerIDChanging(value)  
            Me.SendPropertyChanging()  
            Me._CustomerID = value  
            Me.SendPropertyChanged("CustomerID")  
            Me.OnCustomerIDChanged()  
        End If  
    End Set  
End Property  
```  
  
```csharp  
public string CustomerID  
{  
    set  
    {  
        if ((this._CustomerID != value))  
        {  
            this.OnCustomerIDChanging(value);  
            this.SendPropertyChanging();  
            this._CustomerID = value;  
            this.SendPropertyChanged("CustomerID");  
            this.OnCustomerIDChanged();  
        }  
     }  
}  
```  
  
 クラスの開発者が作成する部分で、メソッドの実装定義を記述します。 Visual Studio では、「`partial`」と入力した後、クラスの別の部分にメソッド定義用の IntelliSense が表示されます。  
  
```vb  
Partial Public Class Customer  
    Private Sub OnCustomerIDChanging(value As String)  
        ' Perform custom validation logic here.  
    End Sub  
End Class  
```  
  
```csharp  
partial class Customer
    {  
        partial void OnCustomerIDChanging(string value)  
        {  
            //Perform custom validation logic here.  
        }  
    }  
```  
  
 部分メソッドを使ってビジネス ロジックをアプリケーションに追加する方法の詳細については、以下のトピックを参照してください。  
  
 [方法: エンティティ クラスに検証を追加する](/visualstudio/data-tools/how-to-add-validation-to-entity-classes)  
  
 [チュートリアル: エンティティ クラスの挿入、更新、および削除の動作のカスタマイズ](/visualstudio/data-tools/walkthrough-customizing-the-insert-update-and-delete-behavior-of-entity-classes)  
  
 [チュートリアル: エンティティ クラスに検証を追加する](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/bb629301(v=vs.120))  
  
## <a name="see-also"></a>関連項目

- [部分クラスと部分メソッド](../../../../../csharp/programming-guide/classes-and-structs/partial-classes-and-methods.md)
- [部分メソッド](../../../../../visual-basic/programming-guide/language-features/procedures/partial-methods.md)
- [Visual Studio の LINQ to SQL ツール](/visualstudio/data-tools/linq-to-sql-tools-in-visual-studio2)
- [SqlMetal.exe (コード生成ツール)](../../../../tools/sqlmetal-exe-code-generation-tool.md)
