---
title: 入れ子になっている要素に指定したリレーションシップの割り当て
ms.date: 03/30/2017
ms.assetid: 24a2d3e5-4af7-4f9a-ab7a-fe6684c9e4fe
ms.openlocfilehash: cd652f51f01dcfa16a8b707f35c658043c20670d
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79150897"
---
# <a name="map-relations-specified-for-nested-elements"></a>入れ子になっている要素に指定したリレーションシップの割り当て
スキーマには、その中の 2 つの要素間の割り当てを明示的に指定するために、**msdata:Relationship** 注釈をインクルードすることができます。 **msdata:Relationship** で指定されたスキーマの 2 つの要素は、必要に応じて、入れ子にすることができます。 割り当て処理では、スキーマの **msdata:Relationship** を使用して 2 つの列間に主キー/外部キーのリレーションシップを生成します。  
  
 **OrderDetail** 要素が **Order** の子要素であることを示す XML スキーマの例を次に示します。 **msdata:Relationship** はこの親子のリレーションシップを識別し、生成された **Order** テーブルの **OrderNumber** 列と生成された **OrderDetail** テーブルの **OrderNo** 列が関連付けられていることを示します。  
  
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
       <xs:element name="OrderNumber" type="xs:string" />  
       <xs:element name="EmpNumber" type="xs:string" />  
       <xs:element name="OrderDetail">  
          <xs:annotation>  
           <xs:appinfo>  
            <msdata:Relationship name="OrdODRelation"
                                msdata:parent="Order"
                                msdata:child="OrderDetail"
                                msdata:parentkey="OrderNumber"
                                msdata:childkey="OrderNo"/>  
           </xs:appinfo>  
          </xs:annotation>  
          <xs:complexType>  
            <xs:sequence>  
             <xs:element name="OrderNo" type="xs:string" />  
             <xs:element name="ItemNo" type="xs:string" />  
            </xs:sequence>  
         </xs:complexType>  
       </xs:element>  
     </xs:sequence>  
    </xs:complexType>  
   </xs:element>  
  </xs:choice>  
 </xs:complexType>  
</xs:element>  
</xs:schema>  
```  
  
 XML スキーマの割り当て処理によって <xref:System.Data.DataSet> に作成される内容は、次のとおりです。  
  
- **Order** および **OrderDetail** テーブル。  
  
    ```text  
    Order(OrderNumber, EmpNumber)  
    OrderDetail(OrderNo, ItemNo)  
    ```  
  
- **Order** テーブルと **OrderDetail** テーブルの間のリレーションシップ。 スキーマの **Order** 要素と **OrderDetail** 要素が入れ子になっているため、このリレーションシップの **Nested** プロパティは **True** に設定されます。  
  
    ```text  
    ParentTable: Order  
    ParentColumns: OrderNumber
    ChildTable: OrderDetail  
    ChildColumns: OrderNo
    RelationName: OrdODRelation  
    Nested: True  
    ```  
  
 割り当て処理によって制約は作成されません。  
  
## <a name="see-also"></a>関連項目

- [XML スキーマ (XSD) からの DataSet リレーションの生成](generating-dataset-relations-from-xml-schema-xsd.md)
- [XML スキーマ (XSD) 制約の DataSet 制約への割り当て](mapping-xml-schema-xsd-constraints-to-dataset-constraints.md)
- [ADO.NET の概要](../ado-net-overview.md)
