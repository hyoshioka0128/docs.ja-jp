---
title: '方法 : XML 要素および XML 属性名を修飾する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- qualifying XML names
- qualifying XML elements
- XML namespaces, qualifying elements and names in
ms.assetid: 44719f90-7e15-42e8-a9e2-282287e2b5bf
ms.openlocfilehash: 1f79caf6ff295d793c615b17d387cdd165e440e7
ms.sourcegitcommit: 17ee6605e01ef32506f8fdc686954244ba6911de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74353095"
---
# <a name="how-to-qualify-xml-element-and-xml-attribute-names"></a>方法 : XML 要素および XML 属性名を修飾する

<xref:System.Xml.Serialization.XmlSerializerNamespaces> クラスのインスタンスに含まれる XML 名前空間は、 [xml の名前空間](https://www.w3.org/TR/REC-xml-names/)と呼ばれる WORLD WIDE WEB コンソーシアム (W3C) の仕様に準拠している必要があります。

XML 名前空間を使用すると、XML ドキュメント内の XML 要素および XML 属性の名前を修飾できます。 修飾名は、プレフィックスとローカル名がコロンで区切られた構成になっています。 プレフィックスはプレースホルダーとしてのみ機能し、名前空間を指定する URI に割り当てられます。 汎用的に管理される URI 名前空間とローカル名を組み合わせることにより、生成される名前は、必ず汎用的に一意になります。

`XmlSerializerNamespaces` のインスタンスを作成し、そのオブジェクトに名前空間のペアを追加することで、XML ドキュメントで使用されるプレフィックスを指定できます。

## <a name="to-create-qualified-names-in-an-xml-document"></a>XML ドキュメントにおける修飾名を作成するには

1. `XmlSerializerNamespaces` クラスのインスタンスを作成します。

2. すべてのプレフィックスと名前空間のペアを `XmlSerializerNamespaces` に追加します。

3. `System.Xml.Serialization` が XML ドキュメントにシリアル化する各メンバーやクラスに、適切な <xref:System.Xml.Serialization.XmlSerializer> 属性を適用します。

    適用できる属性は、<xref:System.Xml.Serialization.XmlAnyElementAttribute>、<xref:System.Xml.Serialization.XmlArrayAttribute>、<xref:System.Xml.Serialization.XmlArrayItemAttribute>、<xref:System.Xml.Serialization.XmlAttributeAttribute>、<xref:System.Xml.Serialization.XmlElementAttribute>、<xref:System.Xml.Serialization.XmlRootAttribute>、および <xref:System.Xml.Serialization.XmlTypeAttribute> です。

4. 各属性の `Namespace` プロパティを、`XmlSerializerNamespaces` のいずれかの名前空間値に設定します。

5. `XmlSerializerNamespaces` を `Serialize` の `XmlSerializer` メソッドに渡します。

## <a name="example"></a>例

`XmlSerializerNamespaces` を作成し、このオブジェクトにプレフィックスと名前空間のペアを 2 つ追加する例を次に示します。 このコードでは、`XmlSerializer` クラスのインスタンスをシリアル化するために使用される `Books` を作成します。 また、`Serialize` を使用して `XmlSerializerNamespaces` メソッドを呼び出し、XML にプレフィックス付き名前空間を含めることができるようにします。

<!-- TODO: THE FOLLOWING VB SNIPPET ISN'T CORRECT!! -->
```vb
Option Explicit
public class Price
{
    [XmlAttribute(Namespace = "http://www.cpandl.com")]
    public string currency;
    [XmlElement(Namespace = "http://www.cohowinery.com")]
    public decimal price;
}

Option Strict

Imports System
Imports System.IO
Imports System.Xml
Imports System.Xml.Serialization

Public Class Run

    Public Shared Sub Main()
        Dim test As New Run()
        test.SerializeObject("XmlNamespaces.xml")
    End Sub 'Main

    Public Sub SerializeObject(filename As String)
        Dim mySerializer As New XmlSerializer(GetType(Books))
        ' Writing a file requires a TextWriter.
        Dim myWriter As New StreamWriter(filename)

        ' Creates an XmlSerializerNamespaces and adds two
        ' prefix-namespace pairs.
        Dim myNamespaces As New XmlSerializerNamespaces()
        myNamespaces.Add("books", "http://www.cpandl.com")
        myNamespaces.Add("money", "http://www.cohowinery.com")

        ' Creates a Book.
        Dim myBook As New Book()
        myBook.TITLE = "A Book Title"
        Dim myPrice As New Price()
        myPrice.price = CDec(9.95)
        myPrice.currency = "US Dollar"
        myBook.PRICE = myPrice
        Dim myBooks As New Books()
        myBooks.Book = myBook
        mySerializer.Serialize(myWriter, myBooks, myNamespaces)
        myWriter.Close()
    End Sub
End Class

Public Class Books
    <XmlElement([Namespace] := "http://www.cohowinery.com")> _
    Public Book As Book
End Class 'Books

<XmlType([Namespace] := "http://www.cpandl.com")> _
Public Class Book

    <XmlElement([Namespace] := "http://www.cpandl.com")> _
    Public TITLE As String
    <XmlElement([Namespace] := "http://www.cohowinery.com")> _
    Public PRICE As Price
End Class

Public Class Price
    <XmlAttribute([Namespace] := "http://www.cpandl.com")> _
    Public currency As String
    Public <XmlElement([Namespace] := "http://www.cohowinery.com")> _
        price As Decimal
End Class
```

```csharp
using System;
using System.IO;
using System.Xml;
using System.Xml.Serialization;

public class Run
{
    public static void Main()
    {
        Run test = new Run();
        test.SerializeObject("XmlNamespaces.xml");
    }
    public void SerializeObject(string filename)
    {
        XmlSerializer mySerializer = new XmlSerializer(typeof(Books));
        // Writing a file requires a TextWriter.
        TextWriter myWriter = new StreamWriter(filename);

        // Creates an XmlSerializerNamespaces and adds two
        // prefix-namespace pairs.
        XmlSerializerNamespaces myNamespaces =
        new XmlSerializerNamespaces();
        myNamespaces.Add("books", "http://www.cpandl.com");
        myNamespaces.Add("money", "http://www.cohowinery.com");

        // Creates a Book.
        Book myBook = new Book();
        myBook.TITLE = "A Book Title";
        Price myPrice = new Price();
        myPrice.price = (decimal) 9.95;
        myPrice.currency = "US Dollar";
        myBook.PRICE = myPrice;
        Books myBooks = new Books();
        myBooks.Book = myBook;
        mySerializer.Serialize(myWriter,myBooks,myNamespaces);
        myWriter.Close();
    }
}

public class Books
{
    [XmlElement(Namespace = "http://www.cohowinery.com")]
    public Book Book;
}

[XmlType(Namespace ="http://www.cpandl.com")]
public class Book
{
    [XmlElement(Namespace = "http://www.cpandl.com")]
    public string TITLE;
    [XmlElement(Namespace ="http://www.cohowinery.com")]
    public Price PRICE;
}
```

## <a name="see-also"></a>参照

- <xref:System.Xml.Serialization.XmlSerializer>
- [XML スキーマ定義ツールと XML シリアル化](the-xml-schema-definition-tool-and-xml-serialization.md)
- [XML シリアル化の概要](introducing-xml-serialization.md)
- [XmlSerializer クラス](xref:System.Xml.Serialization.XmlSerializer)
- [XML シリアル化を制御する属性](attributes-that-control-xml-serialization.md)
- [方法 : XML ストリームの代替要素名を指定する](how-to-specify-an-alternate-element-name-for-an-xml-stream.md)
- [方法 : オブジェクトをシリアル化する](how-to-serialize-an-object.md)
- [方法 : オブジェクトを逆シリアル化する](how-to-deserialize-an-object.md)
