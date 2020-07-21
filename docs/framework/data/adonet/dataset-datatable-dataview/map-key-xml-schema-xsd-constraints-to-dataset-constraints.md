---
title: XML スキーマ (XSD) のキー制約の DataSet 制約への割り当て
ms.date: 03/30/2017
ms.assetid: 22664196-f270-4ebc-a169-70e16a83dfa1
ms.openlocfilehash: 5ebf333b065157fa9497cc1471a45698663638e5
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79150936"
---
# <a name="map-key-xml-schema-xsd-constraints-to-dataset-constraints"></a>XML スキーマ (XSD) のキー制約の DataSet 制約への割り当て
スキーマでは、**key** 要素を使用して要素または属性のキー制約を指定できます。 キー制約を指定する要素または属性の値は、スキーマ インスタンス内で一意になる必要があります。また、null 値にすることはできません。  
  
 キー制約を定義する列の値を null 値にできない点を除くと、キー制約は UNIQUE 制約と同じです。  
  
 **key** 要素に指定できる **msdata** 属性を次の表に示します。  
  
|属性名|説明|  
|--------------------|-----------------|  
|**msdata:ConstraintName**|この属性を指定した場合、その値が制約名として使用されます。 それ以外の場合は、**name** 属性によって制約名の値が設定されます。|  
|**msdata:PrimaryKey**|`PrimaryKey="true"` が指定されている場合、**IsPrimaryKey** 制約のプロパティを **true** に設定することによって、主キーになります。 主キーの値は null 値にできないため、**AllowDBNull** 列のプロパティが **false** に設定されます。|  
  
 キー制約を指定するスキーマの変換では、割り当て処理により、制約の列ごとに **AllowDBNull** 列のプロパティが **false** に設定された状態でテーブルに一意制約が作成されます。 **key** 要素で `msdata:PrimaryKey="true"` を指定しない限り、一意制約の **IsPrimaryKey** プロパティも **false** に設定されます。 これは、スキーマに `PrimaryKey="true"` が指定される UNIQUE 制約と同じです。  
  
 **key** 要素を使用して **CustomerID** 要素のキー制約を指定するスキーマの例を次に示します。  
  
```xml  
<xs:schema id="cod"  
            xmlns:xs="http://www.w3.org/2001/XMLSchema"
            xmlns:msdata="urn:schemas-microsoft-com:xml-msdata">  
  <xs:element name="Customers">  
    <xs:complexType>  
      <xs:sequence>  
        <xs:element name="CustomerID" type="xs:string" minOccurs="0" />  
        <xs:element name="CompanyName" type="xs:string" minOccurs="0" />  
       <xs:element name="Phone" type="xs:string" />  
     </xs:sequence>  
   </xs:complexType>  
 </xs:element>  
<xs:element name="MyDataSet" msdata:IsDataSet="true">  
  <xs:complexType>  
    <xs:choice maxOccurs="unbounded">  
      <xs:element ref="Customers" />  
    </xs:choice>  
  </xs:complexType>  
   <xs:key  msdata:PrimaryKey="true"  
       msdata:ConstraintName="KeyCustID"  
          name="KeyConstCustomerID" >  
     <xs:selector xpath=".//Customers" />  
     <xs:field xpath="CustomerID" />  
    </xs:key>  
 </xs:element>  
</xs:schema>
```  
  
 **key** 要素は、**Customers** 要素の **CustomerID** 子要素の値を一意の値にし、null 値を許可しないように指定します。 XML スキーマ定義言語 (XSD) スキーマの変換では、割り当て処理によって次のテーブルが作成されます。  
  
```text  
Customers(CustomerID, CompanyName, Phone)  
```  
  
 また、次の <xref:System.Data.DataSet> に示すように、XML スキーマの割り当てによって **CustomerID** 列の **UniqueConstraint** を作成することもできます (わかりやすいように、関連するプロパティだけを示します)。  
  
```text  
      DataSetName: MyDataSet  
TableName: customers  
  ColumnName: CustomerID  
      AllowDBNull: False  
      Unique: True  
  ConstraintName: KeyCustID  
      Table: customers  
      Columns: CustomerID
      IsPrimaryKey: True  
```  
  
 生成される **DataSet** では、スキーマの **Key** 要素で `msdata:PrimaryKey="true"` が指定されるため、**UniqueConstraint** の **IsPrimaryKey** プロパティが **true** に設定されます。  
  
 **DataSet** にある **UniqueConstraint** の **ConstraintName** プロパティの値は、スキーマの **key** 要素で指定した **msdata:ConstraintName** 属性の値です。  
  
## <a name="see-also"></a>関連項目

- [XML スキーマ (XSD) 制約の DataSet 制約への割り当て](mapping-xml-schema-xsd-constraints-to-dataset-constraints.md)
- [XML スキーマ (XSD) からの DataSet リレーションの生成](generating-dataset-relations-from-xml-schema-xsd.md)
- [ADO.NET の概要](../ado-net-overview.md)
