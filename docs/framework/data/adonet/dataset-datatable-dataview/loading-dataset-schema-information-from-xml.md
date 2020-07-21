---
title: XML の DataSet スキーマ情報の読み込み
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 43dfb23b-5cef-46f2-8d87-78f0fba1eb8c
ms.openlocfilehash: 69994c546fea842ffef1c8c43d6d6f5bc35e0629
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79151053"
---
# <a name="loading-dataset-schema-information-from-xml"></a>XML の DataSet スキーマ情報の読み込み
<xref:System.Data.DataSet> のスキーマ (テーブル、列、リレーション、および制約) は、プログラムを使用して定義され、<xref:System.Data.Common.DataAdapter> の **Fill** メソッドまたは **FillSchema** メソッドによって作成されるか、あるいは XML ドキュメントから読み込まれます。 XML ドキュメントから **DataSet** スキーマ情報を読み込むには、**DataSet** の **ReadXmlSchema** メソッドまたは **InferXmlSchema** メソッドを使用します。 **ReadXmlSchema** を使用すると、XML スキーマ定義言語 (XSD) スキーマが含まれているドキュメントまたはインライン XML スキーマが含まれている XML ドキュメントから、**DataSet** スキーマ情報を読み込むかまたは推論できます。 **InferXmlSchema** を使用すると、XML ドキュメントからスキーマを推論できます。このとき、指定した特定の XML 名前空間は無視されます。  
  
> [!NOTE]
> XSD の構造 (入れ子になったリレーションなど) を使用してメモリ内で作成された **DataSet** を、Web サービスまたは XML シリアル化を使って転送した場合、**DataSet** 内のテーブルの順序が維持されない場合があります。 この場合、**DataSet** の受け取り側はテーブルの順序に依存していないことが必要です。 ただし、メモリ内で作成するのではなく、転送する **DataSet** のスキーマを XSD ファイルから読み取った場合は、テーブルの順序が常に維持されます。  
  
## <a name="readxmlschema"></a>ReadXmlSchema  
 XML ドキュメントから **DataSet** のスキーマだけを読み込み、データを読み込まないようにするには、**DataSet** の **ReadXmlSchema** メソッドを使用します。 **ReadXmlSchema** では、XML スキーマ定義言語 (XSD) スキーマを使用して定義されている **DataSet** が作成されます。  
  
 **ReadXmlSchema** メソッドは、ファイル名、ストリーム、または読み込む XML ドキュメントが格納されている **XmlReader** のいずれか 1 つを引数として受け取ります。 この XML ドキュメントには、スキーマだけが含まれているか、またはデータのある XML 要素と共にスキーマがインラインで含まれています。 インライン スキーマを XML スキーマとして記述する方法の詳細については、「[XML スキーマ (XSD) からの DataSet リレーショナル構造の派生](deriving-dataset-relational-structure-from-xml-schema-xsd.md)」を参照してください。  
  
 **ReadXmlSchema** に渡された XML ドキュメントに、インライン スキーマ情報が含まれていない場合、**ReadXmlSchema** は XML ドキュメントの要素からスキーマを推論します。 **DataSet** に既にスキーマが含まれている場合、テーブルが存在しなければ新しいテーブルを追加することによって現在のスキーマが拡張されます。 既存のテーブルには新しい列は追加されません。 **DataSet** に既に追加される列が存在していますが、XML で検出された列の型と矛盾する場合には、例外がスローされます。 **ReadXmlSchema** によって XML ドキュメントからスキーマが推論される方法の詳細については、「[XML からの DataSet リレーショナル構造の推論](inferring-dataset-relational-structure-from-xml.md)」を参照してください。  
  
 **ReadXmlSchema** では **DataSet** スキーマの読み込みまたは推論のいずれかが実行されますが、**DataSet** の **ReadXml** メソッドでは、スキーマと XML ドキュメントのデータの両方の読み込みまたは推論が実行されます。 詳しくは、「[XML からの DataSet の読み込み](loading-a-dataset-from-xml.md)」をご覧ください。  
  
 XML ドキュメントまたは XML ストリームから **DataSet** スキーマを読み込む方法のコード例を次に示します。 1 番目の例では、XML スキーマ ファイル名が **ReadXmlSchema** メソッドに渡されます。 2 番目の例では、**System.IO.StreamReader** が示されています。  
  
```vb  
Dim dataSet As DataSet = New DataSet  
dataSet.ReadXmlSchema("schema.xsd")  
```  
  
```csharp  
DataSet dataSet = new DataSet();  
dataSet.ReadXmlSchema("schema.xsd");  
```  
  
```vb  
Dim xmlStream As New System.IO.StreamReader("schema.xsd")
Dim dataSet As DataSet = New DataSet  
dataSet.ReadXmlSchema(xmlStream)  
xmlStream.Close()  
```  
  
```csharp  
System.IO.StreamReader xmlStream = new System.IO.StreamReader("schema.xsd");  
DataSet dataSet = new DataSet();  
dataSet.ReadXmlSchema(xmlStream);  
xmlStream.Close();  
```  
  
## <a name="inferxmlschema"></a>InferXmlSchema  
 **DataSet** に対し、**DataSet** の **InferXmlSchema** メソッドを使用して XML ドキュメントのスキーマを推論するように指示できます。 **InferXmlSchema** は、**XmlReadMode** を **InferSchema** に設定した **ReadXml** (データの読み込みとスキーマの推論) と、読み取られるドキュメントにインライン スキーマが含まれていない場合の **ReadXmlSchema** の両方と同様の機能を備えています。 ただし **InferXmlSchema** には、スキーマを推論するときに無視する特定の XML 名前空間を指定できる追加機能が用意されています。 **InferXmlSchema** に必要な 2 つの引数は、XML ドキュメントの位置と、この操作によって無視される XML 名前空間の文字列配列です。XML ドキュメントの位置は、ファイル名、ストリーム、または **XmlReader** によって指定されます。  
  
 たとえば、次のような XML があるとします。  
  
```xml  
<NewDataSet xmlns:od="urn:schemas-microsoft-com:officedata">  
<Categories>  
  <CategoryID od:adotype="3">1</CategoryID>
  <CategoryName od:maxLength="15" od:adotype="130">Beverages</CategoryName>
  <Description od:adotype="203">Soft drinks and teas</Description>
</Categories>  
<Products>  
  <ProductID od:adotype="20">1</ProductID>
  <ReorderLevel od:adotype="3">10</ReorderLevel>
  <Discontinued od:adotype="11">0</Discontinued>
</Products>  
</NewDataSet>  
```  
  
 前述の XML ドキュメントの要素に対して指定されている属性により、**XmlReadMode** が **InferSchema** の**ReadXmlSchema** メソッドと **ReadXml** メソッドでは、すべての要素 に対するテーブルが作成されます: **Categories**、**CategoryID**、**CategoryName**、**Description**、**Products**、**ProductID**、**ReorderLevel**、**Discontinued**。 (詳細については、「[XML からの DataSet リレーショナル構造の推論](inferring-dataset-relational-structure-from-xml.md)」を参照してください)。ただし、これより適切な方法としては、最初に **Categories** テーブルと **Products** テーブルだけを作成し、次に **Categories** テーブルの **CategoryID**、**CategoryName**、**Description** 列を作成し、**Products** テーブルの **ProductID**、**ReorderLevel**、**Discontinued** 列を作成します。 推論されたスキーマが、XML 要素に指定されている属性を無視するようにするには、**InferXmlSchema** メソッドを使用して **officedata** の XML 名前空間を無視するように指定します。この例を次に示します。  
  
```vb  
Dim dataSet As DataSet = New DataSet  
dataSet.InferXmlSchema("input_od.xml", New String() {"urn:schemas-microsoft-com:officedata"})  
```  
  
```csharp  
DataSet dataSet = new DataSet();  
dataSet.InferXmlSchema("input_od.xml", new string[] "urn:schemas-microsoft-com:officedata");  
```  
  
## <a name="see-also"></a>関連項目

- [DataSet での XML の使用](using-xml-in-a-dataset.md)
- [XML スキーマ (XSD) からの DataSet リレーショナル構造の派生](deriving-dataset-relational-structure-from-xml-schema-xsd.md)
- [XML からの DataSet リレーショナル構造の推論](inferring-dataset-relational-structure-from-xml.md)
- [XML からの DataSet の読み込み](loading-a-dataset-from-xml.md)
- [DataSet、DataTable、および DataView](index.md)
- [ADO.NET の概要](../ado-net-overview.md)
