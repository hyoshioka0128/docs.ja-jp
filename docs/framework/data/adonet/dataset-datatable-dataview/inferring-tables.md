---
title: テーブルの推論
ms.date: 03/30/2017
ms.assetid: 74a288d4-b8e9-4f1a-b2cd-10df92c1ed1f
ms.openlocfilehash: 52ffd3fe90eb491dd01acf8538276cc828fdb309
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2019
ms.locfileid: "70784486"
---
# <a name="inferring-tables"></a>テーブルの推論
XML ドキュメントから <xref:System.Data.DataSet> のスキーマを推論するときには、ADO.NET では、テーブルを表す XML 要素を最初に決定します。 次に示す XML 構造では、**DataSet** スキーマのテーブルが推論されます。  
  
- 属性を持つ要素  
  
- 子要素を持つ要素  
  
- 繰り返し出現する要素  
  
## <a name="elements-with-attributes"></a>属性を持つ要素  
 要素に属性が指定されている場合は、それらの要素はテーブルとして推論されます。 たとえば、次のような XML があるとします。  
  
```xml  
<DocumentElement>  
  <Element1 attr1="value1"/>  
  <Element1 attr1="value2">Text1</Element1>  
</DocumentElement>  
```  
  
 推論プロセスにより、"Element1" という名前のテーブルが生成されます。  
  
 **DataSet:** DocumentElement  
  
 **テーブル:** Element1  
  
|attr1|Element1_Text|  
|-----------|--------------------|  
|value1||  
|value2|Text1|  
  
## <a name="elements-with-child-elements"></a>子要素を持つ要素  
 子要素を持つ要素は、テーブルとして推論されます。 たとえば、次のような XML があるとします。  
  
```xml  
<DocumentElement>  
  <Element1>  
    <ChildElement1>Text1</ChildElement1>  
  </Element1>  
</DocumentElement>  
```  
  
 推論プロセスにより、"Element1" という名前のテーブルが生成されます。  
  
 **DataSet:** DocumentElement  
  
 **テーブル:** Element1  
  
|ChildElement1|  
|-------------------|  
|Text1|  
  
 ドキュメント (ルート) 要素に属性または子要素があり、それらが列として推論される場合には、そのドキュメント要素はテーブルとして推論されます。 ドキュメント要素の属性や子要素が列として推論されない場合、そのドキュメント要素は **DataSet** として推論されます。 たとえば、次のような XML があるとします。  
  
```xml  
<DocumentElement>  
  <Element1>Text1</Element1>  
  <Element2>Text2</Element2>  
</DocumentElement>  
```  
  
 推論プロセスにより、"DocumentElement" という名前のテーブルが生成されます。  
  
 **DataSet:** NewDataSet  
  
 **テーブル:** DocumentElement  
  
|Element1|Element2|  
|--------------|--------------|  
|Text1|Text2|  
  
 または、次のような XML があるとします。  
  
```xml  
<DocumentElement>  
  <Element1 attr1="value1" attr2="value2"/>  
</DocumentElement>  
```  
  
 推論プロセスにより、"Element1" という名前のテーブルを含む "DocumentElement" という名前の **DataSet** が生成されます。  
  
 **DataSet:** DocumentElement  
  
 **テーブル:** Element1  
  
|attr1|attr2|  
|-----------|-----------|  
|value1|value2|  
  
## <a name="repeating-elements"></a>繰り返し出現する要素  
 繰り返し出現する要素は、単一のテーブルとして推論されます。 たとえば、次のような XML があるとします。  
  
```xml  
<DocumentElement>  
  <Element1>Text1</Element1>  
  <Element1>Text2</Element1>  
</DocumentElement>  
```  
  
 推論プロセスにより、"Element1" という名前のテーブルが生成されます。  
  
 **DataSet:** DocumentElement  
  
 **テーブル:** Element1  
  
|Element1_Text|  
|--------------------|  
|Text1|  
|Text2|  
  
## <a name="see-also"></a>関連項目

- [XML からの DataSet リレーショナル構造の推論](inferring-dataset-relational-structure-from-xml.md)
- [XML からの DataSet の読み込み](loading-a-dataset-from-xml.md)
- [XML の DataSet スキーマ情報の読み込み](loading-dataset-schema-information-from-xml.md)
- [DataSet での XML の使用](using-xml-in-a-dataset.md)
- [DataSet、DataTable、および DataView](index.md)
- [ADO.NET の概要](../ado-net-overview.md)
