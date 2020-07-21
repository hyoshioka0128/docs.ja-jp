---
title: '方法: LINQ to XML を使用してディクショナリを操作する'
ms.date: 07/20/2015
ms.assetid: 6cb3f969-1986-414a-b850-87418712edea
ms.openlocfilehash: 14c9c35693f323292849f01af79ae81f92921611
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84397675"
---
# <a name="how-to-work-with-dictionaries-using-linq-to-xml-visual-basic"></a>方法: LINQ to XML を使用してディクショナリを操作する (Visual Basic)
さまざまなデータ構造と XML を相互に変換すると便利な場合がよくあります。 このトピックでは、<xref:System.Collections.Generic.Dictionary%602> と XML を相互に変換することによる、一般的な相互変換の実装について説明します。  
  
## <a name="example"></a>例  
 この例では、XML リテラルと埋め込み式内のクエリを使用します。 このクエリは、新しい <xref:System.Xml.Linq.XElement> オブジェクトを射影します。射影されたオブジェクトは、`Root` <xref:System.Xml.Linq.XElement> オブジェクトの新しいコンテンツになります。  
  
```vb  
Dim dict As Dictionary(Of String, String) = New Dictionary(Of String, String)()  
dict.Add("Child1", "Value1")  
dict.Add("Child2", "Value2")  
dict.Add("Child3", "Value3")  
dict.Add("Child4", "Value4")  
Dim root As XElement = _  
    <Root>  
        <%= From keyValue In dict _  
            Select New XElement(keyValue.Key, keyValue.Value) %>  
    </Root>  
Console.WriteLine(root)  
```  
  
 このコードを実行すると、次の出力が生成されます。  
  
```xml  
          <Root>  
  <Child1>Value1</Child1>  
  <Child2>Value2</Child2>  
  <Child3>Value3</Child3>  
  <Child4>Value4</Child4>  
</Root>  
```  
  
## <a name="example"></a>例  
 次のコードは、XML からディクショナリを作成します。  
  
```vb  
Dim root As XElement = _  
        <Root>  
            <Child1>Value1</Child1>  
            <Child2>Value2</Child2>  
            <Child3>Value3</Child3>  
            <Child4>Value4</Child4>  
        </Root>  
  
Dim dict As Dictionary(Of String, String) = New Dictionary(Of String, String)  
For Each el As XElement In root.Elements  
    dict.Add(el.Name.LocalName, el.Value)  
Next  
For Each str As String In dict.Keys  
    Console.WriteLine("{0}:{1}", str, dict(str))  
Next  
```  
  
 このコードを実行すると、次の出力が生成されます。  
  
```console  
Child1:Value1  
Child2:Value2  
Child3:Value3  
Child4:Value4  
```  
  
## <a name="see-also"></a>関連項目

- [プロジェクションと変換 (LINQ to XML) (Visual Basic)](projections-and-transformations-linq-to-xml.md)
