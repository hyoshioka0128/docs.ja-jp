---
title: XML スキーマ (XSD) の UNIQUE 制約の DataSet 制約への割り当て
ms.date: 03/30/2017
ms.assetid: 56da90bf-21d3-4d1a-8bb8-de908866b78d
ms.openlocfilehash: 8bcf705ce4415929e685be79f813846bbb40bb36
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79150845"
---
# <a name="map-unique-xml-schema-xsd-constraints-to-dataset-constraints"></a>XML スキーマ (XSD) の UNIQUE 制約の DataSet 制約への割り当て
XML スキーマ定義言語 (XSD) スキーマでは、**unique** 要素を使用して要素または属性の一意性制約を指定します。 XML スキーマをリレーショナル スキーマに変換する処理では、XML スキーマの要素または属性で指定した UNIQUE 制約が、生成される <xref:System.Data.DataTable> に対応する <xref:System.Data.DataSet> の UNIQUE 制約に割り当てられます。  
  
 **unique** 要素で指定できる **msdata** 属性を次の表に示します。  
  
|属性名|説明|  
|--------------------|-----------------|  
|**msdata:ConstraintName**|この属性を指定した場合、その値が制約名として使用されます。 それ以外の場合は、**name** 属性によって制約名の値が設定されます。|  
|**msdata:PrimaryKey**|**unique** 要素が `PrimaryKey="true"` である場合、一意制約は、**IsPrimaryKey** プロパティが **true** に設定された状態で作成されます。|  
  
 **unique** 要素を使用して一意性制約を指定する XML スキーマの例を次に示します。  
  
```xml  
<xs:schema id="SampleDataSet"
            xmlns:xs="http://www.w3.org/2001/XMLSchema"
            xmlns:msdata="urn:schemas-microsoft-com:xml-msdata">  
  <xs:element name="Customers">  
    <xs:complexType>  
      <xs:sequence>  
        <xs:element name="CustomerID" type="xs:integer"
           minOccurs="0"/>  
        <xs:element name="CompanyName" type="xs:string"
           minOccurs="0"/>  
       <xs:element name="Phone" type="xs:string" />  
     </xs:sequence>  
   </xs:complexType>  
 </xs:element>  
  
 <xs:element name="SampleDataSet" msdata:IsDataSet="true">  
  <xs:complexType>  
    <xs:choice maxOccurs="unbounded">  
      <xs:element ref="Customers" />  
    </xs:choice>  
  </xs:complexType>  
   <xs:unique     msdata:ConstraintName="UCustID"     name="UniqueCustIDConstr" >       <xs:selector xpath=".//Customers" />       <xs:field xpath="CustomerID" />     </xs:unique>  
</xs:element>  
</xs:schema>  
```  
  
 スキーマの **unique** 要素では、ドキュメント インスタンスのすべての **Customers** 要素に対し、**CustomerID** 子要素の値が一意である必要があることが指定されます。 **DataSet** を作成する場合は、割り当て処理によってスキーマが読み込まれ、次のテーブルが生成されます。  
  
```text  
Customers (CustomerID, CompanyName, Phone)  
```  
  
 次の **DataSet** に示すように、マッピング プロセスによって **CustomerID** 列に対する一意制約も作成されます。 (わかりやすいように、関連するプロパティだけを示します)。  
  
```text  
      DataSetName: MyDataSet  
TableName: Customers  
  ColumnName: CustomerID  
      AllowDBNull: True  
      Unique: True  
  ConstraintName: UcustID       Type: UniqueConstraint  
      Table: Customers  
      Columns: CustomerID
      IsPrimaryKey: False  
```  
  
 生成される **DataSet** では、一意制約のために **IsPrimaryKey** プロパティが **False** に設定されます。 列の **unique** プロパティでは、**CustomerID** 列の値が一意であることが示されます (ただし、列の **AllowDBNull** プロパティで指定されているように、null 参照でもかまいません)。  
  
 スキーマを変更し、オプションの **msdata:PrimaryKey** 属性を **True** に設定すると、一意制約がテーブルに作成されます。 **AllowDBNull** 列プロパティが **False** に設定され、制約の **IsPrimaryKey** プロパティが **True** に設定されるため、**CustomerID** 列が主キー列になります。  
  
 XML スキーマの要素や属性を組み合わせて UNIQUE 制約を指定できます。 次の例では、スキーマに別の **xs:field** 要素を追加することにより、**CustomerID** の値と **CompanyName** の値の組み合わせを任意のインスタンスのすべての **Customers** に対して必ず一意になるように指定する方法を示します。  
  
```xml  
      <xs:unique
         msdata:ConstraintName="SomeName"
         name="UniqueCustIDConstr" >
  <xs:selector xpath=".//Customers" />
  <xs:field xpath="CustomerID" />
  <xs:field xpath="CompanyName" />
</xs:unique>  
```  
  
 その結果、**DataSet** に作成される制約を次に示します。  
  
```text  
ConstraintName: SomeName  
  Table: Customers  
  Columns: CustomerID CompanyName
  IsPrimaryKey: False  
```  
  
## <a name="see-also"></a>関連項目

- [XML スキーマ (XSD) 制約の DataSet 制約への割り当て](mapping-xml-schema-xsd-constraints-to-dataset-constraints.md)
- [XML スキーマ (XSD) からの DataSet リレーションの生成](generating-dataset-relations-from-xml-schema-xsd.md)
- [ADO.NET の概要](../ado-net-overview.md)
