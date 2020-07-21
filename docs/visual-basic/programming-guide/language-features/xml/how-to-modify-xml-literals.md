---
title: '方法: XML リテラルの変更'
ms.date: 07/20/2015
helpviewer_keywords:
- XML axis [Visual Basic], Value
- XML literals [Visual Basic]
- XML literals [Visual Basic], modifying
ms.assetid: 4e864522-a37a-43a2-8236-af80277c5482
ms.openlocfilehash: a2ac2e9802d4c8ab522bb430d15cce5616430437
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84374900"
---
# <a name="how-to-modify-xml-literals-visual-basic"></a>方法: XML リテラルの変更 (Visual Basic)

Visual Basic には、XML リテラルを変更する便利な方法が用意されています。 要素と属性を追加したり削除したりでき、既存の要素を新しい XML 要素に置き換えることもできます。 このトピックでは、既存の XML リテラルを変更する方法の例をいくつか紹介します。

### <a name="to-modify-the-value-of-an-xml-literal"></a>XML リテラルの値を変更するには

1. XML リテラルの値を変更するには、XML リテラルへの参照を取得し、`Value` プロパティを目的の値に設定します。

    次のコード例では、XML ドキュメント内のすべての \<Price> 要素の値が更新されます。

    [!code-vb[VbXmlSamples2#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXmlSamples2/VB/Module2.vb#4)]

    次に、このコード例のソースの XML と変更後の XML の例を示します。

    ソースの XML:

    ```xml
    <?xml version="1.0"?>
    <Catalog>
      <Book id="bk101">
        <Author>Garghentini, Davide</Author>
        <Title>XML Developer's Guide</Title>
        <Price>44.95</Price>
      </Book>
      <Book id="bk331">
        <Author>Spencer, Phil</Author>
        <Title>Developing Applications with Visual Basic .NET</Title>
        <Price>45.95</Price>
      </Book>
    </Catalog>
    ```

    変更後の XML:

    ```xml
    <?xml version="1.0"?>
    <Catalog>
      <Book id="bk101">
        <Author>Garghentini, Davide</Author>
        <Title>XML Developer's Guide</Title>
        <Price>47.20</Price>
      </Book>
      <Book id="bk331">
        <Author>Spencer, Phil</Author>
        <Title>Developing Applications with Visual Basic .NET</Title>
        <Price>48.25</Price>
      </Book>
    </Catalog>
    ```

    > [!NOTE]
    > `Value` プロパティを使用して、コレクション内の最初の XML 要素を参照します。 コレクション内に同じ名前の要素が複数ある場合、`Value` プロパティの設定は、コレクション内の最初の要素にのみ影響します。

### <a name="to-add-an-attribute-to-an-xml-literal"></a>XML リテラルに属性を追加するには

1. XML リテラルに属性を追加するには、最初に XML リテラルへの参照を取得します。 次に、新しい XML 属性軸プロパティを追加して、属性を追加できます。 また、<xref:System.Xml.Linq.XContainer.Add%2A> メソッドを使用して、新しい <xref:System.Xml.Linq.XAttribute> オブジェクトを XML リテラルに追加することもできます。 次の例は、両方のオプションを示しています。

    [!code-vb[VbXmlSamples2#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXmlSamples2/VB/Module2.vb#5)]

    次に、このコード例のソースの XML と変更後の XML の例を示します。

    ソースの XML:

    ```xml
    <?xml version="1.0"?>
    <Catalog>
      <Book id="bk101" >
        <Author>Garghentini, Davide</Author>
        <Title>XML Developer's Guide</Title>
        <Price>44.95</Price>
      </Book>
      <Book id="bk331">
        <Author>Spencer, Phil</Author>
        <Title>Developing Applications with Visual Basic .NET</Title>
        <Price>45.95</Price>
      </Book>
    </Catalog>
    ```

    変更後の XML:

    ```xml
    <?xml version="1.0"?>
    <Catalog>
      <Book id="bk101" genre="Computer" editorEmail="someone@example.com">
        <Author>Garghentini, Davide</Author>
        <Title>XML Developer's Guide</Title>
        <Price>44.95</Price>
      </Book>
      <Book id="bk331" genre="Computer" editorEmail="someone@example.com">
        <Author>Spencer, Phil</Author>
        <Title>Developing Applications with Visual Basic .NET</Title>
        <Price>45.95</Price>
      </Book>
    </Catalog>
    ```

    XML 属性軸プロパティの詳細については、[XML 属性軸プロパティ](../../../language-reference/xml-axis/xml-attribute-axis-property.md)に関する記事をご覧ください。

### <a name="to-add-an-element-to-an-xml-literal"></a>XML リテラルに要素を追加するには

1. XML リテラルに要素を追加するには、最初に XML リテラルへの参照を取得します。 次に、<xref:System.Xml.Linq.XContainer.Add%2A> メソッドを使用すると、新しい <xref:System.Xml.Linq.XElement> オブジェクトを要素の最後のサブ要素として追加できます。 <xref:System.Xml.Linq.XContainer.AddFirst%2A> メソッドを使用すると、新しい <xref:System.Xml.Linq.XElement> オブジェクトを最初のサブ要素として追加できます。

    他のサブ要素を基準として特定の位置に新しい要素を追加するには、最初に隣接するサブ要素への参照を取得します。 次に、<xref:System.Xml.Linq.XNode.AddBeforeSelf%2A> メソッドを使用して、隣接するサブ要素の前に新しい <xref:System.Xml.Linq.XElement> オブジェクトを追加できます。 また、<xref:System.Xml.Linq.XNode.AddAfterSelf%2A> メソッドを使用して、隣接するサブ要素の後に新しい <xref:System.Xml.Linq.XElement> オブジェクトを追加することもできます。

    次の例は、これらの各手法の例を示しています。

    [!code-vb[VbXmlSamples2#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXmlSamples2/VB/Module2.vb#6)]

    次に、このコード例のソースの XML と変更後の XML の例を示します。

    ソースの XML:

    ```xml
    <?xml version="1.0"?>
    <Catalog>
      <Book id="bk101" >
        <Author>Garghentini, Davide</Author>
        <Title>XML Developer's Guide</Title>
        <Price>44.95</Price>
      </Book>
      <Book id="bk331">
        <Author>Spencer, Phil</Author>
        <Title>Developing Applications with Visual Basic .NET</Title>
        <Price>45.95</Price>
      </Book>
    </Catalog>
    ```

    変更後の XML:

    ```xml
    <?xml version="1.0"?>
    <Catalog>
      <Book id="bk101" >
        <Author>Garghentini, Davide</Author>
        <Title>XML Developer's Guide</Title>
        <Price>44.95</Price>
      </Book>
      <Book id="bk000"></Book>
      <Book id="bk331">
        <Publisher>Microsoft Press</Publisher>
        <Author>Spencer, Phil</Author>
        <Title>Developing Applications with Visual Basic .NET</Title>
        <Price>45.95</Price>
        <PublishDate>2005-2-14</PublishDate>
      </Book>
      <Book id="bk999"></Book>
    </Catalog>
    ```

### <a name="to-remove-an-element-or-attribute-from-an-xml-literal"></a>XML リテラルから要素または属性を削除するには

1. XML リテラルから要素または属性を削除するには、次の例に示すように、要素または属性への参照を取得し、`Remove` メソッドを呼び出します。

    [!code-vb[VbXmlSamples2#7](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXmlSamples2/VB/Module2.vb#7)]

    次に、このコード例のソースの XML と変更後の XML の例を示します。

    ソースの XML:

    ```xml
    <?xml version="1.0"?>
    <Catalog>
      <Book id="bk101" genre="Computer" editorEmail="someone@example.com">
        <Author>Garghentini, Davide</Author>
        <Title>XML Developer's Guide</Title>
        <Price>44.95</Price>
      </Book>
      <Book id="bk000"></Book>
      <Book id="bk331" genre="Computer" editorEmail="someone@example.com">
        <Author>Spencer, Phil</Author>
        <Title>Developing Applications with Visual Basic .NET</Title>
        <Price>45.95</Price>
      </Book>
      <Book id="bk999"></Book>
    </Catalog>
    ```

    変更後の XML:

    ```xml
    <?xml version="1.0"?>
    <Catalog>
      <Book id="bk101" editorEmail="someone@example.com">
        <Author>Garghentini, Davide</Author>
        <Title>XML Developer's Guide</Title>
        <Price>44.95</Price>
      </Book>
      <Book id="bk000"></Book>
      <Book id="bk331" editorEmail="someone@example.com">
        <Author>Spencer, Phil</Author>
        <Title>Developing Applications with Visual Basic .NET</Title>
        <Price>45.95</Price>
      </Book></Catalog>
    ```

    XML リテラルからすべての要素または属性を削除するには、XML リテラルへの参照を取得し、<xref:System.Xml.Linq.XElement.RemoveAll%2A> メソッドを呼び出します。

### <a name="to-modify-an-xml-literal"></a>XML リテラルを変更するには

1. XML 要素の名前を変更するには、最初に要素への参照を取得します。 次に、新しい名前を持つ新しい <xref:System.Xml.Linq.XElement> オブジェクトを作成し、この新しい <xref:System.Xml.Linq.XElement> オブジェクトを既存の <xref:System.Xml.Linq.XElement> オブジェクトの <xref:System.Xml.Linq.XNode.ReplaceWith%2A> メソッドに渡すことができます。

    置換する要素に、保持が必要なサブ要素がある場合は、新しい <xref:System.Xml.Linq.XElement> オブジェクトの値を既存の要素の <xref:System.Xml.Linq.XContainer.Nodes%2A> プロパティに設定します。 これにより、新しい要素の値が既存の要素の内部 XML に設定されます。 それ以外の場合は、新しい要素の値を、既存の要素の `Value` プロパティに設定できます。

    次のコード例では、すべての \<Description> 要素が \<Abstract> 要素に置き換えられます。 \<Description> 要素の内容は、\<Description> <xref:System.Xml.Linq.XElement> オブジェクトの <xref:System.Xml.Linq.XContainer.Nodes%2A> プロパティを使用して、新しい \<Abstract> 要素に保持されます。

    [!code-vb[VbXmlSamples2#8](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXmlSamples2/VB/Module2.vb#8)]

    次に、このコード例のソースの XML と変更後の XML の例を示します。

    ソースの XML:

    ```xml
    <?xml version="1.0"?>
    <Catalog>
      <Book id="bk101">
        <Author>Garghentini, Davide</Author>
        <Title>XML Developer's Guide</Title>
        <Price>44.95</Price>
        <Description>
          An in-depth look at creating applications
          with <technology>XML</technology>. For
          <audience>beginners</audience> or
          <audience>advanced</audience> developers.
        </Description>
      </Book>
      <Book id="bk331">
        <Author>Spencer, Phil</Author>
        <Title>Developing Applications with Visual Basic .NET</Title>
        <Price>45.95</Price>
        <Description>
          Get the expert insights, practical code samples, and best
          practices you need to advance your expertise with
          <technology>Visual Basic .NET</technology>.
          Learn how to create faster, more reliable applications
          based on professional, pragmatic guidance by today's top
          <audience>developers</audience>.
        </Description>
      </Book>
    </Catalog>
    ```

    変更後の XML:

    ```xml
    <?xml version="1.0"?>
    <Catalog>
      <Book id="bk101">
        <Author>Garghentini, Davide</Author>
        <Title>XML Developer's Guide</Title>
        <MSRP>44.95</MSRP>    <Abstract>
          An in-depth look at creating applications
          with <technology>XML</technology>. For
          <audience>beginners</audience> or
          <audience>advanced</audience> developers.
        </Abstract>
      </Book>
      <Book id="bk331">
        <Author>Spencer, Phil</Author>
        <Title>Developing Applications with Visual Basic .NET</Title>
        <MSRP>45.95</MSRP>    <Abstract>
          Get the expert insights, practical code samples, and best
          practices you need to advance your expertise with
          <technology>Visual Basic .NET</technology>.
          Learn how to create faster, more reliable applications
          based on professional, pragmatic guidance by today's top
          <audience>developers</audience>.
        </Abstract>
      </Book>
    </Catalog>
    ```

## <a name="see-also"></a>関連項目

- [Visual Basic での XML の操作](manipulating-xml.md)
- [XML](index.md)
- [方法: ファイル、文字列、またはストリームからの XML の読み込み](how-to-load-xml-from-a-file-string-or-stream.md)
- [LINQ](../linq/index.md)
- [Visual Basic における LINQ の概要](../linq/introduction-to-linq.md)
