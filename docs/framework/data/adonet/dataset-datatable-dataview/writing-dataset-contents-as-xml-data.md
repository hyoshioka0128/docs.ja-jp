---
title: DataSet 内容の XML データとしての書き込み
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: fd15f8a5-3b4c-46d0-a561-4559ab2a4705
ms.openlocfilehash: 9a63e79b2fce137ba9d21db861850a471cb42b9f
ms.sourcegitcommit: 8a0fe8a2227af612f8b8941bdb8b19d6268748e7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/03/2019
ms.locfileid: "71833963"
---
# <a name="writing-dataset-contents-as-xml-data"></a>DataSet 内容の XML データとしての書き込み
ADO.NET では、<xref:System.Data.DataSet> の XML 表現を記述することができます。このとき、 にスキーマが含まれていても、含まれていなくてもかまいません。 XML にインラインで含まれているスキーマ情報は、XML スキーマ定義言語 (XSD) を使用して記述されています。 スキーマには、リレーション定義および制約定義と、<xref:System.Data.DataSet> のテーブル定義が含まれています。  
  
 <xref:System.Data.DataSet> が XML データとして書き込まれると、<xref:System.Data.DataSet> の行は現在のバージョンで書き込まれます。 ただし、行の現在の値と元の値の両方を含めるには、<xref:System.Data.DataSet> を DiffGram として書き込みます。  
  
 <xref:System.Data.DataSet> の XML 表現は、ファイル、ストリーム、**XmlWriter**、または文字列に書き込むことができます。 複数の書き込み先があることから、<xref:System.Data.DataSet> の XML 表現の転送方法を柔軟に変更できます。 <xref:System.Data.DataSet> の XML 表現を文字列として取得するには、次の例に示すように **GetXml** メソッドを使用します。  
  
```vb  
Dim xmlDS As String = custDS.GetXml()  
```  
  
```csharp  
string xmlDS = custDS.GetXml();  
```  
  
 **GetXml** では、スキーマ情報を含まない <xref:System.Data.DataSet> の XML 表現が返されます。 <xref:System.Data.DataSet> (XML スキーマ) のスキーマ情報を文字列に書き込むには、**GetXmlSchema** を使用します。  
  
 <xref:System.Data.DataSet> をファイル、ストリーム、または **XmlWriter** に書き込むには、**WriteXml** メソッドを使用します。 **WriteXml** に渡す 1 番目のパラメーターは、XML の出力先です。 たとえば、ファイル名や **System.IO.TextWriter** オブジェクトなどが含まれている文字列を渡します。 2 番目のパラメーター **XmlWriteMode** (省略可能) では、XML 出力の書き込み方法を指定できます。  
  
 **XmlWriteMode** のオプションを次の表に示します。  
  
|XmlWriteMode のオプション|説明|  
|-------------------------|-----------------|  
|**IgnoreSchema**|<xref:System.Data.DataSet> の現在の内容を XML スキーマを含まない XML データとして書き込みます。 既定値です。|  
|**WriteSchema**|<xref:System.Data.DataSet> の現在の内容を XML データとして書き込みます。このとき、リレーショナル構造がインライン XML スキーマとして書き込まれます。|  
|**DiffGram**|元の値と現在の値を含め、<xref:System.Data.DataSet> 全体を DiffGram として書き込みます。 詳しくは、「[DiffGrams](diffgrams.md)」をご覧ください。|  
  
 **DataRelation** オブジェクトが含まれる <xref:System.Data.DataSet> の XML 表現を書き込むときは、多くの場合、この XML 表現で、それぞれの親子のリレーションを持つ子行が関連する親要素内に入れ子になるようにします。 これ行うには、**DataRelation** を <xref:System.Data.DataSet> に追加するときに、**DataRelation** の **Nested** プロパティを **true** に設定します。 詳しくは、「[DataRelation の入れ子化](nesting-datarelations.md)」をご覧ください。  
  
 <xref:System.Data.DataSet> の XML 表現をファイルに書き込む 2 つの例を次に示します。 1 番目の例では、書き込まれる XML のファイル名を文字列として **WriteXml** に渡します。 2 番目の例では、**System.IO.StreamWriter** オブジェクトを渡します。
  
```vb  
custDS.WriteXml("Customers.xml", XmlWriteMode.WriteSchema)  
```  
  
```csharp  
custDS.WriteXml("Customers.xml", XmlWriteMode.WriteSchema);  
```  
  
```vb  
Dim xmlSW As System.IO.StreamWriter = New System.IO.StreamWriter("Customers.xml")  
custDS.WriteXml(xmlSW, XmlWriteMode.WriteSchema)  
xmlSW.Close()  
```  
  
```csharp  
System.IO.StreamWriter xmlSW = new System.IO.StreamWriter("Customers.xml");  
custDS.WriteXml(xmlSW, XmlWriteMode.WriteSchema);  
xmlSW.Close();  
```  
  
## <a name="mapping-columns-to-xml-elements-attributes-and-text"></a>XML 要素、属性、およびテキストへの列の割り当て  
 テーブルの列を XML 形式で表す方法を指定するには、**DataColumn** オブジェクトの **ColumnMapping** プロパティを使用します。 テーブル列の **ColumnMapping** プロパティに対するさまざまな **MappingType** の値と、結果の XML を、次の表に示します。  
  
|MappingType の値|説明|  
|-----------------------|-----------------|  
|**要素**|既定値です。 列が XML 要素として書き込まれます。このとき、ColumnName は要素名になり、列の内容は要素のテキストとして書き込まれます。 次に例を示します。<br /><br /> `<ColumnName>Column Contents</ColumnName>`|  
|**属性**|列が、現在の行の XML 要素の XML 属性として書き込まれます。このとき、ColumnName は属性名になり、列の内容は属性の値として書き込まれます。 次に例を示します。<br /><br /> `<RowElement ColumnName="Column Contents" />`|  
|**SimpleContent**|列の内容が、現在の行の XML 要素のテキストとして書き込まれます。 次に例を示します。<br /><br /> `<RowElement>Column Contents</RowElement>`<br /><br /> **Element** 列または入れ子になったリレーションのあるテーブルの列に対しては、**SimpleContent** を設定できないことに注意してください。|  
|**[非表示]**|列は XML 出力に書き込まれません。|  
  
## <a name="see-also"></a>関連項目

- [DataSet での XML の使用](using-xml-in-a-dataset.md)
- [DiffGrams](diffgrams.md)
- [DataRelation の入れ子化](nesting-datarelations.md)
- [XSD としての DataSet スキーマ情報の書き込み](writing-dataset-schema-information-as-xsd.md)
- [DataSet、DataTable、および DataView](index.md)
- [ADO.NET の概要](../ado-net-overview.md)
