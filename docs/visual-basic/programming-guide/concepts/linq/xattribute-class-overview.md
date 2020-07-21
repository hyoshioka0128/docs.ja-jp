---
title: XAttribute クラスの概要
ms.date: 07/20/2015
ms.assetid: 7781580a-9583-4a1b-ae1e-91c5936eb0b1
ms.openlocfilehash: 5b165044b4bea83e1a0789e3dd00367ed27b43e8
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84413207"
---
# <a name="xattribute-class-overview-visual-basic"></a>XAttribute クラスの概要 (Visual Basic)
属性は、要素に関連付けられている名前と値のペアです。 <xref:System.Xml.Linq.XAttribute> クラスは、XML 属性を表します。  
  
## <a name="overview"></a>概要  
 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] での属性の操作は、要素の操作に似ています。 コンストラクターはほぼ同じです。 それぞれのコレクションの取得に使用するメソッドもほぼ同じです。 属性のコレクションの LINQ クエリ式は、要素のコレクションの LINQ クエリ式とよく似ています。  
  
 属性が要素に追加された順序は保持されます。 つまり、属性を反復処理する場合、属性は追加された順序と同じ順序で表示されます。  
  
## <a name="the-xattribute-constructor"></a>XAttribute コンストラクター  
 最もよく使用する <xref:System.Xml.Linq.XAttribute> クラスのコンストラクターを次に示します。  
  
|コンストラクター|説明|  
|-----------------|-----------------|  
|`XAttribute(XName name, object content)`|<xref:System.Xml.Linq.XAttribute> オブジェクトを作成します。 `name` 引数には属性の名前を指定し、`content` には属性のコンテンツを指定します。|  
  
### <a name="creating-an-element-with-an-attribute"></a>属性を持つ要素の作成  
 次のコードに示した要素には、Visual Basic で XML リテラルを使用して属性を格納しています。  
  
```vb  
Dim phone As XElement = <Phone Type="Home">555-555-5555</Phone>  
Console.WriteLine(phone)  
```  
  
 この例を実行すると、次の出力が生成されます。  
  
```xml  
<Phone Type="Home">555-555-5555</Phone>  
```  
  
### <a name="functional-construction-of-attributes"></a>属性の関数型構築  
 <xref:System.Xml.Linq.XAttribute> オブジェクトは、<xref:System.Xml.Linq.XElement> オブジェクトの構築と共にインラインで構築できます。  
  
```vb  
Dim c As XElement = _  
    <Customers>  
        <Customer>  
            <Name>John Doe</Name>  
            <PhoneNumbers>  
                <Phone type="home">555-555-5555</Phone>  
                <Phone type="work">666-666-6666</Phone>  
            </PhoneNumbers>  
        </Customer>  
    </Customers>  
Console.WriteLine(c)  
```  
  
 この例を実行すると、次の出力が生成されます。  
  
```xml  
<Customers>  
  <Customer>  
    <Name>John Doe</Name>  
    <PhoneNumbers>  
      <Phone type="home">555-555-5555</Phone>  
      <Phone type="work">666-666-6666</Phone>  
    </PhoneNumbers>  
  </Customer>  
</Customers>  
```  
  
### <a name="attributes-are-not-nodes"></a>属性はノードではない  
 属性と要素には、いくつかの違いがあります。 <xref:System.Xml.Linq.XAttribute> オブジェクトは、XML ツリーのノードではありません。 属性は、XML 要素に関連付けられている名前と値のペアです。 ドキュメント オブジェクト モデル (DOM) とは異なり、XML の構造をより密接に反映します。 <xref:System.Xml.Linq.XAttribute> オブジェクトは実際には XML ツリーのノードではありませんが、<xref:System.Xml.Linq.XAttribute> オブジェクトの操作は <xref:System.Xml.Linq.XElement> オブジェクトの操作とよく似ています。  
  
 属性と要素の区別は主に、ノード レベルで XML ツリーを操作するコードを記述する開発者にとってのみ重要な意味を持ちます。 多くの開発者は、この区別を考慮する必要はありません。  
  
## <a name="see-also"></a>関連項目

- [LINQ to XML プログラミングの概要 (Visual Basic)](linq-to-xml-programming-overview.md)
