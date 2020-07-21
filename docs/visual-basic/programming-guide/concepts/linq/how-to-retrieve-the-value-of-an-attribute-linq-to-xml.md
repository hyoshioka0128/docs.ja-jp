---
title: '方法: 属性の値を取得する (LINQ to XML)'
ms.date: 07/20/2015
ms.assetid: 5f4b3790-c83f-4eb3-a889-e3587edf3ca1
ms.openlocfilehash: 48ad3c0ab079012793fd9eea89d52fc3a7b1698f
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84397805"
---
# <a name="how-to-retrieve-the-value-of-an-attribute-linq-to-xml-visual-basic"></a>方法: 属性の値を取得する (LINQ to XML) (Visual Basic)
このトピックでは、属性の値を取得する方法について説明します。 主に 2 つの方法があります。1 つは、<xref:System.Xml.Linq.XAttribute> を目的の型にキャストする方法です。その後、明示的な変換演算子によって、要素または属性のコンテンツが指定した型に変換されます。 もう 1 つは、<xref:System.Xml.Linq.XAttribute.Value%2A> プロパティを使用する方法です。 ただし、通常はキャストがより適切な方法です。 属性を null 許容の値の型にキャストすると、存在しているかどうかが不明確な属性の値を取得する場合にコードをより簡単に記述できます。 この手法の例については、「[方法:要素の値を取得する (LINQ to XML) (Visual Basic)](how-to-retrieve-the-value-of-an-element-linq-to-xml.md)」を参照してください。  
  
## <a name="example"></a>例  
 Visual Basic では、統合属性プロパティを使用して属性の値を取得できます。  
  
```vb  
Dim root As XElement = <Root Attr="abcde"/>  
Console.WriteLine(root)  
Dim str As String = root.@Attr  
Console.WriteLine(str)  
```  
  
 この例を実行すると、次の出力が生成されます。  
  
```xml  
<Root Attr="abcde" />  
abcde  
```  
  
## <a name="example"></a>例  
 Visual Basic では、統合属性プロパティを使用して属性の値を設定できます。 また、統合属性プロパティを使用して存在しない属性の値を設定すると、その属性が作成されます。  
  
```vb  
Dim root As XElement = <Root Att1="content"/>  
root.@Att1 = "new content"  
root.@Att2 = "new attribute"  
Console.WriteLine(root)  
```  
  
 この例を実行すると、次の出力が生成されます。  
  
```xml  
<Root Att1="new content" Att2="new attribute" />  
```  
  
## <a name="example"></a>例  
 属性が名前空間内にある場合にその属性の値を取得する方法を次の例に示します。 詳細については、「[名前空間の概要 (LINQ to XML) (Visual Basic)](namespaces-overview-linq-to-xml.md)」を参照してください。  
  
```vb  
Imports <xmlns:aw="http://www.adventure-works.com">  
  
Module Module1  
    Sub Main()  
        Dim root As XElement = <aw:Root aw:Attr="abcde"/>  
        Dim str As String = root.@aw:Attr  
        Console.WriteLine(str)  
    End Sub  
End Module  
```  
  
 この例を実行すると、次の出力が生成されます。  
  
```console  
abcde  
```  
  
## <a name="see-also"></a>関連項目

- [LINQ to XML 軸 (Visual Basic)](linq-to-xml-axes.md)
