---
title: 厳密に型指定された DataSet の生成
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 54333cbf-bb43-4314-a7d4-6dc1dd1c44b3
ms.openlocfilehash: ce7e5ad53f7aa5dad457ca1aa6ab76716086c0c3
ms.sourcegitcommit: 8a0fe8a2227af612f8b8941bdb8b19d6268748e7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/03/2019
ms.locfileid: "71833987"
---
# <a name="generating-strongly-typed-datasets"></a>厳密に型指定された DataSet の生成
Xml スキーマ定義言語 (XSD) 標準に準拠した XML スキーマを使用すると、Windows ソフトウェア開発キット (SDK) に用意されている XSD.EXE ツールを使用して、厳密に型指定された @no__t 0 を生成できます。  
  
 (データベーステーブルから xsd を作成するには、「<xref:System.Data.DataSet.WriteXmlSchema%2A>」または「 [Visual Studio でのデータセットの操作](/visualstudio/data-tools/dataset-tools-in-visual-studio)」を参照してください)。  
  
 次のコードは、このツールを使用して**データセット**を生成するための構文を示しています。  
  
```  
xsd.exe /d /l:CS XSDSchemaFileName.xsd /eld /n:XSDSchema.Namespace  
```  
  
 この構文では、`/d` ディレクティブは**データセット**を生成するようにツールに指示し、@no__t は、使用する言語 (たとえば、 C#または Visual Basic .net) をツールに指示します。 省略可能な `/eld` ディレクティブは、LINQ to DataSet を使用して、生成されたデータセットに対してクエリを実行できることを指定し**ます。** このオプションは、`/d` オプションと組み合わせて指定します。 詳細については、「[型指定](../querying-typed-datasets.md)された Dataset のクエリ」を参照してください。 オプションの `/n:` ディレクティブは、 **Xsdschema. namespace**という名前の**データセット**の名前空間も生成するようにツールに指示します。 コマンドの出力は XSDSchemaFileName.cs で、ADO.NET アプリケーションでコンパイルおよび使用できます。 生成されたコードをライブラリまたはモジュールとしてコンパイルできます。  
  
 C# コンパイラ (csc.exe) を使用して、生成されたコードをライブラリとしてコンパイルする構文を次のコードで示します。  
  
```  
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
  
 次のコード例では、顧客**データセット**という名前の型指定された**データセット**を使用して、 **Northwind**データベースから顧客のリストを読み込みます。 **Fill**メソッドを使用してデータが読み込まれると、この例では、型指定された Customer **srow** (**DataRow**) オブジェクトを使用して**Customers**テーブルの各顧客をループします。 これにより、 **DataColumnCollection**を介してではなく、 **CustomerID**列に直接アクセスできます。  
  
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
  
 次に、この例で使用する XML スキーマを示します。
  
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
