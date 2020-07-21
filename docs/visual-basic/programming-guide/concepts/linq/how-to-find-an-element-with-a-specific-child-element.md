---
title: '方法: 特定の子要素を持つ要素を検索する'
ms.date: 07/20/2015
ms.assetid: b0d0a463-6a85-46c3-8453-ad25b0ecf93c
ms.openlocfilehash: a05504070fe3d2ea5eb6135fd3bf697b131686c6
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84405288"
---
# <a name="how-to-find-an-element-with-a-specific-child-element-visual-basic"></a>方法: 特定の子要素を持つ要素を検索する (Visual Basic)
このトピックでは、特定の値を含む子要素を持つ特定の要素を検索する方法について説明します。  
  
## <a name="example"></a>例  
 この例では、"Examp2.EXE" の値を含む `Test` 子要素を持つ `CommandLine` 要素を検索します。  
  
 この例では、次の XML ドキュメントを使用します: 「[サンプル XML ファイル:テスト構成 (LINQ to XML)](sample-xml-file-test-configuration-linq-to-xml.md)」。  
  
```vb  
Dim root As XElement = XElement.Load("TestConfig.xml")  
Dim tests As IEnumerable(Of XElement) = _  
    From el In root.<Test> _  
    Where el.<CommandLine>.Value = "Examp2.EXE" _  
    Select el  
For Each el as XElement In tests  
    Console.WriteLine(el.@TestId)  
Next  
```  
  
 このコードを実行すると、次の出力が生成されます。  
  
```console  
0002  
0006  
```  
  
 この例では、[XML 子軸プロパティ](../../../language-reference/xml-axis/xml-child-axis-property.md)、[XML 属性軸プロパティ](../../../language-reference/xml-axis/xml-attribute-axis-property.md)、および [XML 値プロパティ](../../../language-reference/xml-axis/xml-value-property.md)が使用されることに注意してください。  
  
## <a name="example"></a>例  
 次の例は名前空間に含まれている XML 用のクエリです。これらのクエリは上の例と同じ機能を表しています。 詳細については、「[名前空間の概要 (LINQ to XML) (Visual Basic)](namespaces-overview-linq-to-xml.md)」を参照してください。  
  
 この例では、次の XML ドキュメントを使用します: 「[サンプル XML ファイル: 名前空間内のテスト構成](sample-xml-file-test-configuration-in-a-namespace.md)」。  
  
```vb  
Imports <xmlns='http://www.adatum.com'>  
  
Module Module1  
    Sub Main()  
        Dim root As XElement = XElement.Load("TestConfigInNamespace.xml")  
        Dim tests As IEnumerable(Of XElement) = _  
            From el In root.<Test> _  
            Where el.<CommandLine>.Value = "Examp2.EXE" _  
            Select el  
        For Each el As XElement In tests  
            Console.WriteLine(el.@TestId)  
        Next  
    End Sub  
End Module  
```  
  
 このコードを実行すると、次の出力が生成されます。  
  
```console  
0002  
0006  
```  
  
## <a name="see-also"></a>関連項目

- <xref:System.Xml.Linq.XElement.Attribute%2A>
- <xref:System.Xml.Linq.XContainer.Elements%2A>
- [基本的なクエリ (LINQ to XML) (Visual Basic)](basic-queries-linq-to-xml.md)
- [標準クエリ演算子の概要 (Visual Basic)](standard-query-operators-overview.md)
- [射影操作 (Visual Basic)](projection-operations.md)
