---
title: XML 宣言付きのシリアル化
ms.date: 07/20/2015
ms.assetid: 8726f79e-2bb0-4ba0-969d-197cca591647
ms.openlocfilehash: cd303a800efe42d3fa99d601f25d54320570bed3
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84411800"
---
# <a name="serializing-with-an-xml-declaration-visual-basic"></a>XML 宣言付きのシリアル化 (Visual Basic)
このトピックでは、シリアル化を実行する際に XML 宣言を生成するかどうかを制御する方法について説明します。  
  
## <a name="xml-declaration-generation"></a>XML 宣言の生成  
 <xref:System.IO.File> メソッドまたは <xref:System.IO.TextWriter> メソッドを使用して <xref:System.Xml.Linq.XElement.Save%2A?displayProperty=nameWithType> または <xref:System.Xml.Linq.XDocument.Save%2A?displayProperty=nameWithType> にシリアル化すると、XML 宣言が生成されます。 <xref:System.Xml.XmlWriter> にシリアル化する場合は、<xref:System.Xml.XmlWriterSettings> オブジェクトで指定したライター設定により、XML 宣言が生成されるかどうかが決定されます。  
  
 `ToString` メソッドを使用して文字列にシリアル化する場合、生成される XML には XML 宣言は含まれません。  
  
### <a name="serializing-with-an-xml-declaration"></a>XML 宣言付きのシリアル化  
 次の例では、<xref:System.Xml.Linq.XElement> を作成し、ドキュメントをファイルに保存して、そのファイルをコンソールに出力します。  
  
```vb  
Dim root As XElement = <Root>  
                           <Child>child content</Child>  
                       </Root>  
root.Save("Root.xml")  
Dim str As String = File.ReadAllText("Root.xml")  
Console.WriteLine(str)  
```  
  
 この例を実行すると、次の出力が生成されます。  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<Root>  
  <Child>child content</Child>  
</Root>  
```  
  
### <a name="serializing-without-an-xml-declaration"></a>XML 宣言なしでのシリアル化  
 <xref:System.Xml.Linq.XElement> を <xref:System.Xml.XmlWriter> に保存する方法を次の例に示します。  
  
```vb  
Dim sb As StringBuilder = New StringBuilder()  
Dim xws As XmlWriterSettings = New XmlWriterSettings()  
xws.OmitXmlDeclaration = True  
  
Using xw As XmlWriter = XmlWriter.Create(sb, xws)  
    Dim root = <Root>  
                   <Child>child content</Child>  
               </Root>  
    root.Save(xw)  
End Using  
Console.WriteLine(sb.ToString())  
```  
  
 この例を実行すると、次の出力が生成されます。  
  
```xml  
<Root><Child>child content</Child></Root>  
```  
  
## <a name="see-also"></a>関連項目

- [XML ツリーのシリアル化 (Visual Basic)](serializing-xml-trees.md)
