---
title: 推論の制限事項
ms.date: 03/30/2017
ms.assetid: 78517994-5d57-44f8-9d20-38812977de09
ms.openlocfilehash: 10347abc5b01edb4ec6fbf97221d44f4bfb88f54
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2019
ms.locfileid: "70784581"
---
# <a name="inference-limitations"></a>推論の制限事項
各ドキュメントに含まれている XML 要素によっては、XML から <xref:System.Data.DataSet> のスキーマを推論するプロセスにより、異なるスキーマが生成される可能性があります。 たとえば、次のような XML ドキュメントがあるとします。  
  
 Document1:  
  
```xml  
<DocumentElement>  
  <Element1>Text1</Element1>  
  <Element1>Text2</Element1>  
</DocumentElement>  
```  
  
 Document2:  
  
```xml  
<DocumentElement>  
  <Element1>Text1</Element1>  
</DocumentElement>  
```  
  
 推論プロセスでは、"Document1" については、"DocumentElement" という名前の **DataSet** と "Element1" という名前のテーブルが作成されます。これは、"Element1" が繰り返し出現する要素であるためです。  
  
 **DataSet:** DocumentElement  
  
 **テーブル:** Element1  
  
|Element1_Text|  
|--------------------|  
|Text1|  
|Text2|  
  
 これに対して、"Document2" については、"NewDataSet" という名前の **DataSet** と "DocumentElement" という名前のテーブルが推論プロセスで生成されます。 この場合、属性も子要素も持たない "Element1" は列として推論されます。  
  
 **DataSet:** NewDataSet  
  
 **テーブル:** DocumentElement  
  
|Element1|  
|--------------|  
|Text1|  
  
 これらの 2 つの XML ドキュメントは、同じスキーマを生成することを意図して記述されていますが、推論プロセスでは、各ドキュメントに含まれる要素を基にまったく異なるスキーマが生成されてしまいます。  
  
 XML ドキュメントからスキーマを生成するときに生じる可能性のあるこのような矛盾を避けるため、XML から **DataSet** を読み込むときは、XSD (XML スキーマ定義言語) または XDR (XML-Data Reduced) を使用して、スキーマを明示的に指定することをお勧めします。 XML スキーマを使用して **DataSet** スキーマを明示的に指定する方法については、「[XML スキーマ (XSD) からの DataSet リレーショナル構造の派生](deriving-dataset-relational-structure-from-xml-schema-xsd.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- [XML からの DataSet リレーショナル構造の推論](inferring-dataset-relational-structure-from-xml.md)
- [XML からの DataSet の読み込み](loading-a-dataset-from-xml.md)
- [XML の DataSet スキーマ情報の読み込み](loading-dataset-schema-information-from-xml.md)
- [DataSet での XML の使用](using-xml-in-a-dataset.md)
- [DataSet、DataTable、および DataView](index.md)
- [ADO.NET の概要](../ado-net-overview.md)
