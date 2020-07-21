---
title: 列の推論
ms.date: 03/30/2017
ms.assetid: 0e022699-c922-454c-93e2-957dd7e7247a
ms.openlocfilehash: 2718cbcf29799f99c8648b129fdb6079a6f6d344
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2019
ms.locfileid: "70786179"
---
# <a name="inferring-columns"></a>列の推論
ADO.NET は、<xref:System.Data.DataSet> のテーブルとして推論する要素を、XML ドキュメントから決定した後、それらのテーブルの列を推論します。 ADO.NET 2.0 では、各 **simpleType** 要素の厳密に型指定されたデータ型を推論する新しいスキーマ推論エンジンが導入されました。 以前のバージョンでは、推論される **simpleType** 要素のデータ型は、常に **xsd:string** でした。  
  
## <a name="migration-and-backward-compatibility"></a>移行および下位互換性  
 **ReadXml** メソッドは、**InferSchema** 型の引数を受け取ります。 この引数を使用することにより、以前のバージョンと互換性のある推論方法を指定することができます。 **InferSchema** 列挙型で使用できる値を、次の表に示します。  
  
 <xref:System.Data.XmlReadMode.InferSchema>  
 単純型を <xref:System.String> として常に推論することで下位互換性を提供します。  
  
 <xref:System.Data.XmlReadMode.InferTypedSchema>  
 厳密に型指定されたデータ型を推論します。 <xref:System.Data.DataTable> で使用した場合、例外をスローします。  
  
 <xref:System.Data.XmlReadMode.IgnoreSchema>  
 インライン スキーマを無視し、データを既存の <xref:System.Data.DataSet> スキーマに読み取ります。  
  
## <a name="attributes"></a>属性  
 「[テーブルの推論](inferring-tables.md)」で説明されているように、属性を持つ要素は、テーブルとして推論されます。 その要素の属性は、そのテーブルの列として推論されます。 スキーマが XML に書き戻される場合に、列の名前が確実に属性として書き込まれるように、推論された列の **ColumnMapping** プロパティは **MappingType.Attribute** に設定されます。 属性の値は、テーブルの行に格納されます。 たとえば、次のような XML があるとします。  
  
```xml  
<DocumentElement>  
  <Element1 attr1="value1" attr2="value2"/>  
</DocumentElement>  
```  
  
 推論プロセスにより、**attr1** および **attr2** という 2 つの列を持つ **Element1** という名前のテーブルが生成されます。 2 つの列の **ColumnMapping** プロパティは、**MappingType.Attribute** に設定されます。  
  
 **DataSet:** DocumentElement  
  
 **テーブル:** Element1  
  
|attr1|attr2|  
|-----------|-----------|  
|value1|value2|  
  
## <a name="elements-without-attributes-or-child-elements"></a>属性または子の要素を持たない要素  
 要素に子の要素または属性がない場合、その要素は列として推論されます。 列の **ColumnMapping** プロパティは、**MappingType.Element** に設定されます。 子の要素のテキストは、テーブルの行に格納されます。 たとえば、次のような XML があるとします。  
  
```xml  
<DocumentElement>  
  <Element1>  
    <ChildElement1>Text1</ChildElement1>  
    <ChildElement2>Text2</ChildElement2>  
  </Element1>  
</DocumentElement>  
```  
  
 推論プロセスにより、**ChildElement1** および **ChildElement2** という 2 つの列を持つ **Element1** という名前のテーブルが生成されます。 2 つの列の **ColumnMapping** プロパティは、**MappingType.Element** に設定されます。  
  
 **DataSet:** DocumentElement  
  
 **テーブル:** Element1  
  
|ChildElement1|ChildElement2|  
|-------------------|-------------------|  
|Text1|Text2|  
  
## <a name="see-also"></a>関連項目

- [XML からの DataSet リレーショナル構造の推論](inferring-dataset-relational-structure-from-xml.md)
- [XML からの DataSet の読み込み](loading-a-dataset-from-xml.md)
- [XML の DataSet スキーマ情報の読み込み](loading-dataset-schema-information-from-xml.md)
- [DataSet での XML の使用](using-xml-in-a-dataset.md)
- [DataSet、DataTable、および DataView](index.md)
- [ADO.NET の概要](../ado-net-overview.md)
