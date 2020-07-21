---
title: リレーションシップの推論
ms.date: 03/30/2017
ms.assetid: 8fa86a9d-6545-4a9d-b1f5-58d9742179c7
ms.openlocfilehash: 4c9c13453e4a830fcda337e8163649ba6491a995
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2019
ms.locfileid: "70785365"
---
# <a name="inferring-relationships"></a>リレーションシップの推論
テーブルとして推論される要素に、同じくテーブルとして推論される子の要素が含まれている場合には、2 つのテーブル間に <xref:System.Data.DataRelation> が作成されます。 この場合、**ParentTableName_Id** という名前の新しい列が、親の要素に対して作成されたテーブルと、子の要素に対して作成されたテーブルの両方に追加されます。 この ID 列の **ColumnMapping** プロパティは、**MappingType.Hidden** に設定されます。 この列が、親テーブルの自動的にインクリメントされる主キーとなり、2 つのテーブル間の **DataRelation** で使用されます。 推論される他のすべての列のデータ型は **System.String** になりますが、追加される ID 列のデータ型は **System.Int32** になります。 親テーブルと子テーブル両方の新しい列を使用して、**DeleteRule** = **Cascade** である <xref:System.Data.ForeignKeyConstraint> も作成されます。  
  
 たとえば、次のような XML があるとします。  
  
```xml  
<DocumentElement>  
  <Element1>  
    <ChildElement1 attr1="value1" attr2="value2"/>  
    <ChildElement2>Text2</ChildElement2>  
  </Element1>  
</DocumentElement>  
```  
  
 推論プロセスにより 2 つのテーブルが生成されます: **Element1** と **ChildElement1**。  
  
 **Element1** テーブルには、次の 2 つの列があります: **Element1_Id** と **ChildElement2**。 **Element1_Id** 列の **ColumnMapping** プロパティは、**MappingType.Hidden** に設定されます。 **ChildElement2** 列の **ColumnMapping** プロパティは、**MappingType.Element** に設定されます。 **Element1_Id** 列は、**Element1** テーブルの主キーとして設定されます。  
  
 **ChildElement1** テーブルには、**attr1**、**attr2**、**Element1_Id** という名前の 3 つの列があります。 **attr1** 列と **attr2** 列の **ColumnMapping** プロパティは、**MappingType.Attribute** に設定されます。 **Element1_Id** 列の **ColumnMapping** プロパティは、**MappingType.Hidden** に設定されます。  
  
 両方のテーブルの **Element1_Id** 列を使用して、**DataRelation** と **ForeignKeyConstraint** が作成されます。  
  
 **DataSet:** DocumentElement  
  
 **テーブル:** Element1  
  
|Element1_Id|ChildElement2|  
|------------------|-------------------|  
|0|Text2|  
  
 **テーブル:** ChildElement1  
  
|attr1|attr2|Element1_Id|  
|-----------|-----------|------------------|  
|value1|value2|0|  
  
 **DataRelation:** Element1_ChildElement1  
  
 **ParentTable:** Element1  
  
 **ParentColumn:** Element1_Id  
  
 **ChildTable:** ChildElement1  
  
 **ChildColumn:** Element1_Id  
  
 **Nested:** True  
  
 **ForeignKeyConstraint:** Element1_ChildElement1  
  
 **Column:** Element1_Id  
  
 **ParentTable:** Element1  
  
 **ChildTable:** ChildElement1  
  
 **DeleteRule:** Cascade  
  
 **AcceptRejectRule:** None  
  
## <a name="see-also"></a>関連項目

- [XML からの DataSet リレーショナル構造の推論](inferring-dataset-relational-structure-from-xml.md)
- [XML からの DataSet の読み込み](loading-a-dataset-from-xml.md)
- [XML の DataSet スキーマ情報の読み込み](loading-dataset-schema-information-from-xml.md)
- [DataRelation の入れ子化](nesting-datarelations.md)
- [DataSet での XML の使用](using-xml-in-a-dataset.md)
- [DataSet、DataTable、および DataView](index.md)
- [ADO.NET の概要](../ado-net-overview.md)
