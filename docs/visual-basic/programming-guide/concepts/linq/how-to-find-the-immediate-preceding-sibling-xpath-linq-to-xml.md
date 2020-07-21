---
title: '方法: 直前の兄弟を検索する (XPath-LINQ to XML)'
ms.date: 07/20/2015
ms.assetid: ec046283-9fe2-4440-b295-860bf700099d
ms.openlocfilehash: 8b0071b2f39b8debdd52083718fe928c1f9fb6f3
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84364527"
---
# <a name="how-to-find-the-immediate-preceding-sibling-xpath-linq-to-xml-visual-basic"></a>方法: 直前の兄弟を検索する (XPath-LINQ to XML) (Visual Basic)

ノードの直前の兄弟を検索することが必要になる場合があります。 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] とは対照的に、XPath では先行する兄弟軸の位置述語にはセマンティクス上の違いがあります。この  と XPath の相違点は、注目すべき特徴といえます。

## <a name="example"></a>例

この例では、[!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] クエリは、<xref:System.Linq.Enumerable.Last%2A> 演算子を使用して、<xref:System.Xml.Linq.XNode.ElementsBeforeSelf%2A> から返されるコレクション内の最後のノードを検索します。 一方、XPath 式は、値が 1 の述語を使用して直前の要素を検索します。

```vb
Dim root As XElement = _
    <Root>
        <Child1/>
        <Child2/>
        <Child3/>
        <Child4/>
    </Root>
Dim child4 As XElement = root.Element("Child4")

' LINQ to XML query
Dim el1 As XElement = child4.ElementsBeforeSelf().Last()

' XPath expression
Dim el2 As XElement = _
    DirectCast(child4.XPathEvaluate("preceding-sibling::*[1]"),  _
    IEnumerable).Cast(Of XElement)().First()

If el1 Is el2 Then
    Console.WriteLine("Results are identical")
Else
    Console.WriteLine("Results differ")
End If
Console.WriteLine(el1)
```

この例を実行すると、次の出力が生成されます。

```console
Results are identical
<Child3 />
```

## <a name="see-also"></a>関連項目

- [XPath ユーザー向けの LINQ to XML (Visual Basic)](linq-to-xml-for-xpath-users.md)
