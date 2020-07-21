---
title: 厳密に型指定された DataSet の生成
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 54333cbf-bb43-4314-a7d4-6dc1dd1c44b3
ms.openlocfilehash: 25419f8a810b52103e6b862cfe2fe6ab5a1fd981
ms.sourcegitcommit: ad800f019ac976cb669e635fb0ea49db740e6890
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/29/2019
ms.locfileid: "73040086"
---
# <a name="generating-strongly-typed-datasets"></a>厳密に型指定された DataSet の生成
XML スキーマ定義言語 (XSD) 標準に準拠する XML スキーマがあれば、Windows ソフトウェア開発キット (SDK) に付属する XSD.exe ツールを使用して、厳密に型指定された <xref:System.Data.DataSet> を生成できます。  
  
 (データベース テーブルから xsd を作成するには、<xref:System.Data.DataSet.WriteXmlSchema%2A> に関するトピック、または「[Visual Studio でのデータセットの操作](/visualstudio/data-tools/dataset-tools-in-visual-studio)」を参照してください)。  
  
 次のコードでは、このツールを使用して **DataSet** を生成する構文を示します。  
  
```console  
xsd.exe /d /l:CS XSDSchemaFileName.xsd /eld /n:XSDSchema.Namespace  
```  
  
 この構文の `/d` ディレクティブでは、**DataSet** を生成することをツールに指示し、`/l:` では使用する言語 (C#、Visual Basic .NET など) をツールに指示します。 オプションの `/eld` ディレクティブを指定すると、生成された **DataSet** に対し、LINQ to DataSet を使用してクエリを実行できます。 このオプションは、`/d` オプションと組み合わせて指定します。 詳しくは、「[型指定された DataSet のクエリ](../querying-typed-datasets.md)」をご覧ください。 オプションの `/n:` ディレクティブでは、**XSDSchema.Namespace** という名前の名前空間も **DataSet** に対して生成することをツールに指示します。 コマンドの出力は XSDSchemaFileName.cs で、ADO.NET アプリケーションでコンパイルおよび使用できます。 生成されたコードをライブラリまたはモジュールとしてコンパイルできます。  
  
 C# コンパイラ (csc.exe) を使用して、生成されたコードをライブラリとしてコンパイルする構文を次のコードで示します。  
  
```console  
csc.exe /t:library XSDSchemaFileName.cs /r:System.dll /r:System.Data.dll  
```  
  
 `/t:` ディレクティブはライブラリとしてコンパイルすることをツールに知らせ、`/r:` ディレクティブはコンパイルに必要な依存ライブラリを指定します。 コマンドの出力は XSDSchemaFileName.dll で、`/r:` ディレクティブによる ADO.NET アプリケーションのコンパイル時にコンパイラに渡すことができます。  
  
 ADO.NET アプリケーションの XSD.exe に渡された名前空間にアクセスする構文を次のコードで示します。  
  
```vb  
Imports XSDSchema.Namespace  
```  
  
```csharp  
using XSDSchema.Namespace;  
```  
  
 次のコード例では、**CustomerDataSet** という名前の型指定された **DataSet** を使用して、**Northwind** データベースから顧客リストを読み込みます。 **Fill** メソッドを使用してデータを読み込んだ後、例では、型指定された **CustomersRow** (**DataRow**) オブジェクトを使用して、**Customers** テーブルの各顧客をループします。 このようにすると、**DataColumnCollection** による場合とは異なり、**CustomerID** 列に直接アクセスできます。  
  
```vb  
Dim customers As CustomerDataSet= New CustomerDataSet()  
Dim adapter As SqlDataAdapter New SqlDataAdapter( _  
  "SELECT * FROM dbo.Customers;", _  
  "Data Source=(local);Integrated " & _  
  "Security=SSPI;Initial Catalog=Northwind")  
  
adapter.Fill(customers, "Customers")  
  
Dim customerRow As CustomerDataSet.CustomersRow  
For Each customerRow In customers.Customers  
  Console.WriteLine(customerRow.CustomerID)  
Next  
```  
  
```csharp  
CustomerDataSet customers = new CustomerDataSet();  
SqlDataAdapter adapter = new SqlDataAdapter(  
  "SELECT * FROM dbo.Customers;",  
  "Data Source=(local);Integrated " +  
  "Security=SSPI;Initial Catalog=Northwind");  
  
adapter.Fill(customers, "Customers");  
  
foreach(CustomerDataSet.CustomersRow customerRow in customers.Customers)  
  Console.WriteLine(customerRow.CustomerID);  
```  
  
 例に使用された XML スキーマを次に示します。
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<xs:schema id="CustomerDataSet" xmlns="" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:msdata="urn:schemas-microsoft-com:xml-msdata">  
  <xs:element name="CustomerDataSet" msdata:IsDataSet="true">  
    <xs:complexType>  
      <xs:choice maxOccurs="unbounded">  
        <xs:element name="Customers">  
          <xs:complexType>  
            <xs:sequence>  
              <xs:element name="CustomerID" type="xs:string" minOccurs="0" />  
            </xs:sequence>  
          </xs:complexType>  
        </xs:element>  
      </xs:choice>  
    </xs:complexType>  
  </xs:element>  
</xs:schema>  
```  
  
## <a name="see-also"></a>関連項目

- <xref:System.Data.DataColumnCollection>
- <xref:System.Data.DataSet>
- [型指定されたデータセット](typed-datasets.md)
- [DataSet、DataTable、および DataView](index.md)
- [ADO.NET の概要](../ado-net-overview.md)
