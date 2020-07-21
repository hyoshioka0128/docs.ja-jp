---
title: 属性の値を取得する方法 (LINQ to XML) (C#)
ms.date: 07/20/2015
ms.assetid: 817bbe89-5979-4234-bf0c-46f63692ac8c
ms.openlocfilehash: 212ad3bb3097e7e2c76da8f165011b181f329d4c
ms.sourcegitcommit: 99b153b93bf94d0fecf7c7bcecb58ac424dfa47c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2020
ms.locfileid: "80249195"
---
# <a name="how-to-retrieve-the-value-of-an-attribute-linq-to-xml-c"></a>属性の値を取得する方法 (LINQ to XML) (C#)
このトピックでは、属性の値を取得する方法について説明します。 主に 2 つの方法があります。1 つは、<xref:System.Xml.Linq.XAttribute> を目的の型にキャストする方法です。その後、明示的な変換演算子によって、要素または属性のコンテンツが指定した型に変換されます。 もう 1 つは、<xref:System.Xml.Linq.XAttribute.Value%2A> プロパティを使用する方法です。 ただし、通常はキャストがより適切な方法です。 属性を null 許容の値の型にキャストすると、存在しているかどうかが不明確な属性の値を取得する場合にコードをより簡単に記述できます。 この手法の例については、「[要素の値を取得する方法 (LINQ to XML) (C#)](./how-to-retrieve-the-value-of-an-element-linq-to-xml.md)」を参照してください。  
  
## <a name="example"></a>例  
 属性の値を取得するには、<xref:System.Xml.Linq.XAttribute> オブジェクトを目的の型にキャストします。  
  
```csharp  
XElement root = new XElement("Root",  
                    new XAttribute("Attr", "abcde")  
                );  
Console.WriteLine(root);  
string str = (string)root.Attribute("Attr");  
Console.WriteLine(str);  
```  
  
 この例を実行すると、次の出力が生成されます。  
  
```output  
<Root Attr="abcde" />  
abcde  
```  
  
## <a name="example"></a>例  
 属性が名前空間内にある場合にその属性の値を取得する方法を次の例に示します。 詳細については、「[名前空間の概要 (LINQ to XML)](namespaces-overview-linq-to-xml.md)」を参照してください。  
  
```csharp  
XNamespace aw = "http://www.adventure-works.com";  
XElement root = new XElement(aw + "Root",  
                    new XAttribute(aw + "Attr", "abcde")  
                );  
string str = (string)root.Attribute(aw + "Attr");  
Console.WriteLine(str);  
```  
  
 この例を実行すると、次の出力が生成されます。  
  
```output  
abcde  
```  
  
## <a name="see-also"></a>関連項目

- [LINQ to XML 軸 (C#)](./linq-to-xml-axes-overview.md)
