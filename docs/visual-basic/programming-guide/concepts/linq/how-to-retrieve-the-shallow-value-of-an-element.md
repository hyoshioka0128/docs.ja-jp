---
title: '方法: 要素の浅い値を取得する'
ms.date: 07/20/2015
ms.assetid: 730a6670-fb8c-41fc-8a1b-eb97a837e432
ms.openlocfilehash: 24e6b128481f56941f0a61da9766f02813a46e97
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84397818"
---
# <a name="how-to-retrieve-the-shallow-value-of-an-element-visual-basic"></a>方法: 要素の浅い値を取得する (Visual Basic)

このトピックでは、要素の浅い値を取得する方法について説明します。 浅い値は、特定の要素のみの値のことです。これに対し、深い値とは、すべての子孫要素の値が単一の文字列として連結された値をいいます。

キャストまたは <xref:System.Xml.Linq.XElement.Value%2A?displayProperty=nameWithType> プロパティによって要素値を取得する場合は、深い値を取得することになります。 浅い値を取得するには、次の例のように `ShallowValue` 拡張メソッドを使用します。 浅い値を取得することは、要素をその内容に基づいて選択する必要がある場合に役立ちます。

次の例では、要素の浅い値を取得する拡張メソッドを宣言しています。 次に、この拡張メソッドをクエリの中で使用して、計算値を含んだすべての要素をリストします。

## <a name="example"></a>例

次のテキスト ファイル (Report.xml) は、この例のソースです。

```xml
<?xml version="1.0" encoding="utf-8" ?>
<Report>
  <Section>
    <Heading>
      <Column Name="CustomerId">=Customer.CustomerId.Heading</Column>
      <Column Name="Name">=Customer.Name.Heading</Column>
    </Heading>
    <Detail>
      <Column Name="CustomerId">=Customer.CustomerId</Column>
      <Column Name="Name">=Customer.Name</Column>
    </Detail>
  </Section>
</Report>
```

```vb
Module Module1
    <System.Runtime.CompilerServices.Extension()> _
    Public Function ShallowValue(ByVal xe As XElement)
        Return xe _
               .Nodes() _
               .OfType(Of XText)() _
               .Aggregate(New StringBuilder(), _
                              Function(s, c) s.Append(c), _
                              Function(s) s.ToString())
    End Function

    Sub Main()
        Dim root As XElement = XElement.Load("Report.xml")

        Dim query As IEnumerable(Of XElement) = _
            From el In root.Descendants() _
            Where (el.ShallowValue().StartsWith("=")) _
            Select el

        For Each q As XElement In query
            Console.WriteLine("{0}{1}{2}", _
                q.Name.ToString().PadRight(8), _
                q.Attribute("Name").ToString().PadRight(20), _
                q.ShallowValue())
        Next
    End Sub
End Module
```

この例を実行すると、次の出力が生成されます。

```console
Column  Name="CustomerId"   =Customer.CustomerId.Heading
Column  Name="Name"         =Customer.Name.Heading
Column  Name="CustomerId"   =Customer.CustomerId
Column  Name="Name"         =Customer.Name
```

## <a name="see-also"></a>関連項目

- [LINQ to XML 軸 (Visual Basic)](linq-to-xml-axes.md)
