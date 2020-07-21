---
title: XML スキーマ (XSD) のキー参照制約の DataSet 制約への割り当て
ms.date: 03/30/2017
ms.assetid: 5b634fea-cc1e-4f6b-9454-10858105b1c8
ms.openlocfilehash: 902b79b73f494ced0f54b29babff1b2e767bd47a
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79150884"
---
# <a name="map-keyref-xml-schema-xsd-constraints-to-dataset-constraints"></a>XML スキーマ (XSD) のキー参照制約の DataSet 制約への割り当て
**keyref** 要素を使用すると、ドキュメント内の要素間にリンクを確立できます。 これは、リレーショナル データベースの外部キーのリレーションシップと同様です。 スキーマに **keyref** 要素を指定すると、スキーマの割り当て処理時に keyref 要素がそれに対応する <xref:System.Data.DataSet> の列の外部キー制約に変換されます。 既定では、**keyref** 要素によってリレーションも生成され、リレーションに **ParentTable**、**ChildTable**、**ParentColumn**、**ChildColumn** プロパティが指定されます。  
  
 **keyref** 要素で指定できる **msdata** 属性を次の表に示します。  
  
|属性名|説明|  
|--------------------|-----------------|  
|**msdata:ConstraintOnly**|スキーマの **keyref** 要素で **ConstraintOnly="true"** を指定した場合、制約が作成されますが、リレーションは作成されません。 この属性を指定しない (または **False** に設定する) 場合、制約およびリレーションが **DataSet** に作成されます。|  
|**msdata:ConstraintName**|**ConstraintName** 属性を指定した場合、その値が制約名として使用されます。 それ以外の場合、スキーマの **keyref** 要素の **name** 属性によって **DataSet** の制約名が設定されます。|  
|**msdata:UpdateRule**|スキーマの **keyref** 要素で **UpdateRule** 属性を指定した場合、その値が **DataSet** の **UpdateRule** 制約プロパティに割り当てられます。 それ以外の場合、**UpdateRule** プロパティは **Cascade** に設定されます。|  
|**msdata:DeleteRule**|スキーマの **keyref** 要素で **DeleteRule** 属性を指定した場合、その値が **DataSet** の **DeleteRule** 制約プロパティに割り当てられます。 それ以外の場合、**DeleteRule** プロパティは **Cascade** に設定されます。|  
|**msdata:AcceptRejectRule**|スキーマの **keyref** 要素で **AcceptRejectRule** 属性を指定した場合、その値が **DataSet** の **AcceptRejectRule** 制約プロパティに割り当てられます。 それ以外の場合、**AcceptRejectRule** プロパティは **None** に設定されます。|  
  
 **Order** 要素の **OrderNumber** 子要素と **OrderDetail** 要素の **OrderNo** 子要素の間の **key** リレーションシップと **keyref** リレーションシップを指定するスキーマの例を次に示します。  
  
 例では、**OrderDetail** 要素の **OrderNumber** 子要素が、**Order** 要素の **OrderNo** キーの子要素を参照します。  
  
```xml  
<xs:schema id="MyDataSet" xmlns=""
            xmlns:xs="http://www.w3.org/2001/XMLSchema"
            xmlns:msdata="urn:schemas-microsoft-com:xml-msdata">  
  
 <xs:element name="MyDataSet" msdata:IsDataSet="true">  
  <xs:complexType>  
    <xs:choice maxOccurs="unbounded">  
      <xs:element name="OrderDetail">  
       <xs:complexType>  
         <xs:sequence>  
           <xs:element name="OrderNo" type="xs:integer" />  
           <xs:element name="ItemNo" type="xs:string" />  
         </xs:sequence>  
       </xs:complexType>  
      </xs:element>  
      <xs:element name="Order">  
        <xs:complexType>  
          <xs:sequence>  
            <xs:element name="OrderNumber" type="xs:integer" />  
            <xs:element name="EmpNumber" type="xs:integer" />  
          </xs:sequence>  
        </xs:complexType>  
      </xs:element>  
    </xs:choice>  
  </xs:complexType>  
  
  <xs:key name="OrderNumberKey"  >  
    <xs:selector xpath=".//Order" />  
    <xs:field xpath="OrderNumber" />  
  </xs:key>  
  
  <xs:keyref name="OrderNoRef" refer="OrderNumberKey">  
    <xs:selector xpath=".//OrderDetail" />  
    <xs:field xpath="OrderNo" />  
  </xs:keyref>  
 </xs:element>  
</xs:schema>  
```  
  
 XML スキーマ定義言語 (XSD) スキーマの割り当て処理によって、2 つのテーブルを持つ次の **DataSet** が生成されます。  
  
```text  
OrderDetail(OrderNo, ItemNo) and  
Order(OrderNumber, EmpNumber)  
```  
  
 さらに、**DataSet** によって次の制約が定義されます。  
  
- **Order** テーブルの一意制約。  
  
    ```text
              Table: Order  
    Columns: OrderNumber
    ConstraintName: OrderNumberKey  
    Type: UniqueConstraint  
    IsPrimaryKey: False  
    ```  
  
- **Order** テーブルと **OrderDetail** テーブルの間のリレーションシップ。 スキーマの 2 つの要素が入れ子になっていないため、**Nested** プロパティは **False** に設定されます。  
  
    ```text
              ParentTable: Order  
    ParentColumns: OrderNumber
    ChildTable: OrderDetail  
    ChildColumns: OrderNo
    ParentKeyConstraint: OrderNumberKey  
    ChildKeyConstraint: OrderNoRef  
    RelationName: OrderNoRef  
    Nested: False  
    ```  
  
- **OrderDetail** テーブルの外部キー制約。  
  
    ```text  
              ConstraintName: OrderNoRef  
    Type: ForeignKeyConstraint  
    Table: OrderDetail  
    Columns: OrderNo
    RelatedTable: Order  
    RelatedColumns: OrderNumber
    ```  
  
## <a name="see-also"></a>関連項目

- [XML スキーマ (XSD) 制約の DataSet 制約への割り当て](mapping-xml-schema-xsd-constraints-to-dataset-constraints.md)
- [XML スキーマ (XSD) からの DataSet リレーションの生成](generating-dataset-relations-from-xml-schema-xsd.md)
- [ADO.NET の概要](../ado-net-overview.md)
