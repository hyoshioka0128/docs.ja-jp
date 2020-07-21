---
title: XML スキーマ制約およびリレーションシップ
ms.date: 03/30/2017
ms.assetid: 165bc2bc-60a1-40e0-9b89-7c68ef979079
ms.openlocfilehash: 2388d7c277ba1f01bea8d419e5aedf487b843ed7
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79150715"
---
# <a name="xml-schema-constraints-and-relationships"></a>XML スキーマ制約およびリレーションシップ
XML スキーマ定義言語 (XSD) スキーマでは、制約 (UNIQUE、キー、キー参照) およびリレーションシップ (**msdata:Relationship** 注釈を使用した) を指定できます。 このトピックでは、XML スキーマで指定した制約およびリレーションシップを解釈して <xref:System.Data.DataSet> を生成する方法について説明します。  
  
 一般的に、XML スキーマでは **DataSet** にリレーションシップだけを生成する場合に、**msdata:Relationship** 注釈を指定します。 詳細については、「[XML スキーマ (XSD) からの DataSet リレーションの生成](generating-dataset-relations-from-xml-schema-xsd.md)」を参照してください。 **DataSet** に制約を生成する場合は、制約 (UNIQUE、キー、およびキー参照) を指定します。 このトピックの後に説明されているように、リレーションシップを生成するにはキー制約とキー参照制約も使用するので注意してください。  
  
## <a name="generating-a-relationship-from-key-and-keyref-constraints"></a>キー制約およびキー参照制約によるリレーションシップの生成  
 **msdata:Relationship** 注釈を指定する代わりに、XML スキーマの割り当て処理時に使用するキー制約とキー参照制約を指定し、制約だけでなく、**DataSet** のリレーションシップも生成することができます。 ただし、**keyref** 要素で `msdata:ConstraintOnly="true"` を指定した場合、**DataSet** には制約だけが作成され、リレーションシップは生成されません。  
  
 入れ子になっていない **Order** 要素と **OrderDetail** 要素を含む XML スキーマの例を次に示します。 スキーマでは、キー制約とキー参照制約も指定します。  
  
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
  
 XML スキーマの割り当て処理時に生成される **DataSet** には、**Order** テーブルと **OrderDetail** テーブルが含まれます。 さらに、**DataSet** にはリレーションシップと制約も含まれます。 そのリレーションシップと制約の例を次に示します。 スキーマでは、**msdata:Relationship** 注釈が指定されないことに注意してください。代わりに、キー制約とキー参照制約を使用してリレーションが生成されます。  
  
```text
....ConstraintName: OrderNumberKey  
....Type: UniqueConstraint  
....Table: Order  
....Columns: OrderNumber  
....IsPrimaryKey: False  
  
....ConstraintName: OrderNoRef  
....Type: ForeignKeyConstraint  
....Table: OrderDetail  
....Columns: OrderNo  
....RelatedTable: Order  
....RelatedColumns: OrderNumber  
  
..RelationName: OrderNoRef  
..ParentTable: Order  
..ParentColumns: OrderNumber  
..ChildTable: OrderDetail  
..ChildColumns: OrderNo  
..ParentKeyConstraint: OrderNumberKey  
..ChildKeyConstraint: OrderNoRef  
..Nested: False  
```  
  
 上記のスキーマの例では、**Order** 要素と **OrderDetail** 要素は入れ子になっていません。 入れ子になっている Order 要素と OrderDetail 要素を含むスキーマの例を次に示します。 ただし、**msdata:Relationship** 注釈が指定されていないため、暗黙のリレーションが適用されます。 詳細については、「[入れ子になっているスキーマ要素間の暗黙的なリレーションの割り当て](map-implicit-relations-between-nested-schema-elements.md)」を参照してください。 スキーマでは、キー制約とキー参照制約も指定します。  
  
```xml  
<xs:schema id="MyDataSet" xmlns=""
            xmlns:xs="http://www.w3.org/2001/XMLSchema"
            xmlns:msdata="urn:schemas-microsoft-com:xml-msdata">  
  
 <xs:element name="MyDataSet" msdata:IsDataSet="true">  
  <xs:complexType>  
    <xs:choice maxOccurs="unbounded">  
  
      <xs:element name="Order">  
        <xs:complexType>  
          <xs:sequence>  
            <xs:element name="OrderNumber" type="xs:integer" />  
            <xs:element name="EmpNumber" type="xs:integer" />  
  
            <xs:element name="OrderDetail">  
              <xs:complexType>  
                <xs:sequence>  
                  <xs:element name="OrderNo" type="xs:integer" />  
                  <xs:element name="ItemNo" type="xs:string" />  
                </xs:sequence>  
              </xs:complexType>  
            </xs:element>  
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
  
 XML スキーマの割り当て処理によって生成された **DataSet** には、次の 2 つのテーブルが含まれます。  
  
```text  
Order(OrderNumber, EmpNumber, Order_Id)  
OrderDetail(OrderNumber, ItemNumber, Order_Id)  
```  
  
 さらに、**DataSet** には 2 つのリレーションシップ (1 つは **msdata:relationship** 注釈に基づいた、もう 1 つはキー制約とキー参照制約に基づいた) およびさまざまな制約も含まれます。 リレーションおよび制約の例を次に示します。  
  
```text
..RelationName: Order_OrderDetail  
..ParentTable: Order  
..ParentColumns: Order_Id  
..ChildTable: OrderDetail  
..ChildColumns: Order_Id  
..ParentKeyConstraint: Constraint1  
..ChildKeyConstraint: Order_OrderDetail  
..Nested: True  
  
..RelationName: OrderNoRef  
..ParentTable: Order  
..ParentColumns: OrderNumber  
..ChildTable: OrderDetail  
..ChildColumns: OrderNo  
..ParentKeyConstraint: OrderNumberKey  
..ChildKeyConstraint: OrderNoRef  
..Nested: False  
  
..ConstraintName: OrderNumberKey  
..Type: UniqueConstraint  
..Table: Order  
..Columns: OrderNumber  
..IsPrimaryKey: False  
  
..ConstraintName: Constraint1  
..Type: UniqueConstraint  
..Table: Order  
..Columns: Order_Id  
..IsPrimaryKey: True  
  
..ConstraintName: Order_OrderDetail  
..Type: ForeignKeyConstraint  
..Table: OrderDetail  
..Columns: Order_Id  
..RelatedTable: Order  
..RelatedColumns: Order_Id  
  
..ConstraintName: OrderNoRef  
..Type: ForeignKeyConstraint  
..Table: OrderDetail  
..Columns: OrderNo  
..RelatedTable: Order  
..RelatedColumns: OrderNumber  
```  
  
 入れ子になっているテーブルを参照するキー参照制約に **msdata:IsNested="true"** 注釈が含まれている場合は、**DataSet** により、そのキー参照制約と関連する UNIQUE/ キー制約に基づいて、1 つの入れ子になったリレーションシップが作成されます。  
  
## <a name="see-also"></a>関連項目

- [XML スキーマ (XSD) からの DataSet リレーショナル構造の派生](deriving-dataset-relational-structure-from-xml-schema-xsd.md)
- [ADO.NET の概要](../ado-net-overview.md)
