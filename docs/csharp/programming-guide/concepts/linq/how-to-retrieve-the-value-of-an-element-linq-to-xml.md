---
title: 要素の値を取得する方法 (LINQ to XML) (C#)
ms.date: 07/20/2015
ms.assetid: 4228c007-07c9-4cf2-a45b-e7074c109581
ms.openlocfilehash: c4bb78e937fe0de08242923cdd7cd638abf571c7
ms.sourcegitcommit: f87ad41b8e62622da126aa928f7640108c4eff98
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/07/2020
ms.locfileid: "80805835"
---
# <a name="how-to-retrieve-the-value-of-an-element-linq-to-xml-c"></a>要素の値を取得する方法 (LINQ to XML) (C#)

この記事では、要素の値を取得する方法について説明します。 値を取得するには、主に 2 つの方法があります。

- <xref:System.Xml.Linq.XElement> または <xref:System.Xml.Linq.XAttribute> を目的の型にキャストします。 その後、明示的な変換演算子によって、要素または属性のコンテンツが指定した型に変換され、変数に代入されます。

- <xref:System.Xml.Linq.XElement.Value%2A?displayProperty=nameWithType> または <xref:System.Xml.Linq.XAttribute.Value%2A?displayProperty=nameWithType> プロパティを使用します。 また、これらのプロパティを使用して値を設定することもできます。

C# の場合、通常はキャストがより適切な方法です。 要素または属性を null 許容の値の型にキャストすると、存在しているかどうかが不明確な要素 (または属性) の値を取得する場合にコードをより簡単に記述できます。 この記事の[最後の例](#element-might-not-exist-example)では、要素が存在しない可能性がある場合に、キャストがより単純であることを示しています。 ただし、<xref:System.Xml.Linq.XElement.Value%2A?displayProperty=nameWithType> プロパティの場合とは異なり、キャストを通じて要素のコンテンツを設定することはできません。  
  
## <a name="string-cast-example"></a>文字列キャストの例  
 要素の値を取得するには、<xref:System.Xml.Linq.XElement> オブジェクトを目的の型にキャストします。 次に示すように、要素は文字列にキャストできます。  
  
```csharp  
XElement e = new XElement("StringElement", "abcde");  
Console.WriteLine(e);  
Console.WriteLine("Value of e:" + (string)e);  
```  
  
 この例を実行すると、次の出力が生成されます。  
  
```output  
<StringElement>abcde</StringElement>  
Value of e:abcde  
```  
  
## <a name="integer-cast-example"></a>整数キャストの例  
 文字列以外の型に要素をキャストすることもできます。 たとえば、次のコードに示すように、整数を含んだ要素を `int` にキャストできます。  
  
```csharp  
XElement e = new XElement("Age", "44");  
Console.WriteLine(e);  
Console.WriteLine("Value of e:" + (int)e);  
```  
  
 この例を実行すると、次の出力が生成されます。  
  
```output  
<Age>44</Age>  
Value of e:44  
```  
  
 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] では、`string`、`bool`、`bool?`、`int`、`int?`、`uint`、`uint?`、`long`、`long?`、`ulong`、`ulong?`、`float`、`float?`、`double`、`double?`、`decimal`、`decimal?`、`DateTime`、`DateTime?`、`TimeSpan`、`TimeSpan?`、`GUID`、および `GUID?` というデータ型について明示的なキャスト演算子を用意しています。  
  
 また、[!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] は、<xref:System.Xml.Linq.XAttribute> オブジェクトについても同様のキャスト演算子を用意しています。  
  
## <a name="value-property-example"></a>Value プロパティの例  
 <xref:System.Xml.Linq.XElement.Value%2A> プロパティを使用すると、要素のコンテンツを取得できます。  
  
```csharp  
XElement e = new XElement("StringElement", "abcde");
Console.WriteLine(e);  
Console.WriteLine("Value of e:" + e.Value);  
```  
  
 この例を実行すると、次の出力が生成されます。  
  
```output  
<StringElement>abcde</StringElement>  
Value of e:abcde  
```  
  
## <a name="element-might-not-exist-example"></a>要素が存在しない可能性の例
 存在しているかどうかが明確でない要素の値の取得を試行する場合があります。 このケースでは、null 許容参照型または null 許容の値の型にキャストされた要素を代入するときに、その要素が存在しない場合、代入された変数は `null` に設定されます。 要素が存在するかどうかわからないときは、<xref:System.Xml.Linq.XElement.Value%2A> プロパティよりもキャストを使用した方が簡単であることを、次のコードは示しています。  
  
```csharp  
XElement root = new XElement("Root",  
    new XElement("Child1", "child 1 content"),  
    new XElement("Child2", "2")  
);  
  
// The following assignments show why it is easier to use  
// casting when the element might or might not exist.  
  
string c1 = (string)root.Element("Child1");  
Console.WriteLine("c1:{0}", c1 == null ? "element does not exist" : c1);  
  
int? c2 = (int?)root.Element("Child2");  
Console.WriteLine("c2:{0}", c2 == null ? "element does not exist" : c2.ToString());  
  
string c3 = (string)root.Element("Child3");  
Console.WriteLine("c3:{0}", c3 == null ? "element does not exist" : c3);  
  
int? c4 = (int?)root.Element("Child4");  
Console.WriteLine("c4:{0}", c4 == null ? "element does not exist" : c4.ToString());  
  
Console.WriteLine();  
  
// The following assignments show the required code when using  
// the Value property when the element might or might not exist.  
// Notice that this is more difficult than the casting approach.  
  
XElement e1 = root.Element("Child1");  
string v1;  
if (e1 == null)  
    v1 = null;  
else  
    v1 = e1.Value;  
Console.WriteLine("v1:{0}", v1 == null ? "element does not exist" : v1);  
  
XElement e2 = root.Element("Child2");  
int? v2;  
if (e2 == null)  
    v2 = null;  
else  
    v2 = Int32.Parse(e2.Value);  
Console.WriteLine("v2:{0}", v2 == null ? "element does not exist" : v2.ToString());  
  
XElement e3 = root.Element("Child3");  
string v3;  
if (e3 == null)  
    v3 = null;  
else  
    v3 = e3.Value;  
Console.WriteLine("v3:{0}", v3 == null ? "element does not exist" : v3);  
  
XElement e4 = root.Element("Child4");  
int? v4;  
if (e4 == null)  
    v4 = null;  
else  
    v4 = Int32.Parse(e4.Value);  
Console.WriteLine("v4:{0}", v4 == null ? "element does not exist" : v4.ToString());  
```  
  
 このコードを実行すると、次の出力が生成されます。  
  
```output  
c1:child 1 content  
c2:2  
c3:element does not exist  
c4:element does not exist  
  
v1:child 1 content  
v2:2  
v3:element does not exist  
v4:element does not exist  
```  
  
 通常、要素や属性のコンテンツを取得するには、キャストを使用する方が単純なコードになります。  
  
## <a name="see-also"></a>関連項目

- [LINQ to XML 軸 (C#)](./linq-to-xml-axes-overview.md)
