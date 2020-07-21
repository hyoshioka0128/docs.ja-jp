---
title: 入れ子になっていない要素間のリレーションの指定
ms.date: 03/30/2017
ms.assetid: e31325da-7691-4d33-acf4-99fccca67006
ms.openlocfilehash: bee427c6cdf76792773ea827c8772b276ff29c31
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79150819"
---
# <a name="specify-relations-between-elements-with-no-nesting"></a>入れ子になっていない要素間のリレーションの指定
要素が入れ子になっていない場合、暗黙的なリレーションは作成されません。 それに対し、**msdata:Relationship** 注釈を使用すると、入れ子になっていない要素間にリレーションを明示的に指定できます。  
  
 互いに入れ子になっていない **Order** 要素と **OrderDetail** 要素の間に **msdata:Relationship** 注釈を指定する XML スキーマの例を次に示します。 **msdata:Relationship** 注釈は、**Schema** 要素の子要素として指定します。  
  
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
           <xs:element name="OrderNo" type="xs:string" />  
           <xs:element name="ItemNo" type="xs:string" />  
         </xs:sequence>  
       </xs:complexType>  
      </xs:element>  
      <xs:element name="Order">  
       <xs:complexType>  
         <xs:sequence>  
           <xs:element name="OrderNumber" type="xs:string" />  
           <xs:element name="EmpNumber" type="xs:string" />  
         </xs:sequence>  
       </xs:complexType>  
      </xs:element>  
    </xs:choice>  
  </xs:complexType>  
  
  </xs:element>  
   <xs:annotation>  
     <xs:appinfo>  
       <msdata:Relationship name="OrdOrderDetailRelation"  
                            msdata:parent="Order"
                            msdata:child="OrderDetail"
                            msdata:parentkey="OrderNumber"
                            msdata:childkey="OrderNo"/>  
     </xs:appinfo>  
  </xs:annotation>  
</xs:schema>  
```  
  
 次に示すように、XML スキーマ定義言語 (XSD) スキーマ マッピング処理によって、**Order** テーブルと **OrderDetail** テーブルを含む <xref:System.Data.DataSet> が作成され、それらのテーブル間にリレーションシップが指定されます。  
  
```text  
RelationName: OrdOrderDetailRelation  
ParentTable: Order  
ParentColumns: OrderNumber
ChildTable: OrderDetail  
ChildColumns: OrderNo
Nested: False  
```  
  
## <a name="see-also"></a>関連項目

- [XML スキーマ (XSD) からの DataSet リレーションの生成](generating-dataset-relations-from-xml-schema-xsd.md)
- [XML スキーマ (XSD) 制約の DataSet 制約への割り当て](mapping-xml-schema-xsd-constraints-to-dataset-constraints.md)
- [ADO.NET の概要](../ado-net-overview.md)
