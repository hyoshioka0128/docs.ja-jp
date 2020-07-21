---
title: '方法: LINQ を使用した XML の変換'
ms.date: 07/20/2015
helpviewer_keywords:
- XML [Visual Basic], transforming
- LINQ to XML [Visual Basic], transforming XML
ms.assetid: 815687f4-0bc2-4c0b-adc6-d78744aa356f
ms.openlocfilehash: dab394ec45567589e002b5d2ac76ec19fb0f76c6
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84374883"
---
# <a name="how-to-transform-xml-by-using-linq-visual-basic"></a>方法: LINQ を使用して XML を変換する (Visual Basic)

[XML リテラル](../../../language-reference/xml-literals/index.md)を使用すると、XML を 1 つのソースから簡単に読み取って、新しい XML 形式に変換することできます。 LINQ クエリを利用して、変換するコンテンツを取得したり、既存のドキュメントの内容を新しい XML 形式に変更したりできます。

このトピックの例では、XML ソース ドキュメントから HTML にコンテンツを変換して、ブラウザーで表示されるようにします。

[!INCLUDE[note_settings_general](~/includes/note-settings-general-md.md)]

### <a name="to-transform-an-xml-document"></a>XML ドキュメントを変換するには

1. Visual Studio で、**コンソール アプリケーション** プロジェクト テンプレートで新しい Visual Basic プロジェクトを作成します。

2. プロジェクトで作成された Module1.vb ファイルをダブルクリックして、Visual Basic コードを変更します。 次のコードを `Module1` モジュールの `Sub Main` に追加します。 このコードでは、ソース XML ドキュメントを <xref:System.Xml.Linq.XDocument> オブジェクトとして作成します。

    ```vb
    Dim catalog =
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
              Get the expert insights, practical code samples,
              and best practices you need
              to advance your expertise with <technology>Visual
              Basic .NET</technology>.
              Learn how to create faster, more reliable applications
              based on professional,
              pragmatic guidance by today's top <audience>developers</audience>.
            </Description>
          </Book>
        </Catalog>
    ```

     [方法: ファイル、文字列、またはストリームからの XML の読み込み](how-to-load-xml-from-a-file-string-or-stream.md)。

3. ソースの XML ドキュメントを作成するコードの後に、次のコードを追加してオブジェクトからすべての \<Book> 要素を取得し、それらを HTML ドキュメントに変換します。 \<Book> 要素の一覧は、変換された HTML を含む <xref:System.Xml.Linq.XElement> オブジェクトのコレクションを返す LINQ クエリを使用して作成されます。 埋め込み式を使用して、ソース ドキュメントの値を新しい XML 形式で入力できます。

     結果として得られる HTML ドキュメントは、<xref:System.Xml.Linq.XElement.Save%2A> メソッドを使用してファイルに書き込まれます。

    ```vb
    Dim htmlOutput =
      <html>
        <body>
          <%= From book In catalog.<Catalog>.<Book>
              Select <div>
                       <h1><%= book.<Title>.Value %></h1>
                       <h3><%= "By " & book.<Author>.Value %></h3>
                        <h3><%= "Price = " & book.<Price>.Value %></h3>
                        <h2>Description</h2>
                        <%= TransformDescription(book.<Description>(0)) %>
                        <hr/>
                      </div> %>
        </body>
      </html>

    htmlOutput.Save("BookDescription.html")
    ```

4. `Module1` の `Sub Main` の後ろに新しいメソッド (`Sub`) を追加して、\<Description> ノードを指定された HTML 形式に変換します。 このメソッドは、前のステップのコードによって呼び出され、\<Description> 要素の形式を保持するために使用されます。

     このメソッドは、\<Description> 要素のサブ要素を HTML に置き換えます。 `ReplaceWith` メソッドは、サブ要素の場所を保持するために使用されます。 \<Description> 要素の変換されたコンテンツは、HTML 段落 (\<p>) 要素に含まれます。 <xref:System.Xml.Linq.XContainer.Nodes%2A> プロパティは、\<Description> 要素の変換されたコンテンツを取得するために使用されます。 これにより、変換されたコンテンツにサブ要素が含まれるようになります。

     次のコードを `Module1` の `Sub Main` の後ろに追加します。

    ```vb
    Public Function TransformDescription(ByVal desc As XElement) As XElement

      ' Replace <technology> elements with <b>.
      Dim content = (From element In desc...<technology>).ToList()

      If content.Count > 0 Then
        For i = 0 To content.Count - 1
          content(i).ReplaceWith(<b><%= content(i).Value %></b>)
        Next
      End If

      ' Replace <audience> elements with <i>.
      content = (From element In desc...<audience>).ToList()

      If content.Count > 0 Then
        For i = 0 To content.Count - 1
          content(i).ReplaceWith(<i><%= content(i).Value %></i>)
        Next
      End If

      ' Return the updated contents of the <Description> element.
      Return <p><%= desc.Nodes %></p>
    End Function
    ```

5. 変更内容を保存します。

6. F5 キーを押してコードを実行します。 結果として保存されるドキュメントは、次のようになります。

    ```html
    <?xml version="1.0"?>
    <html>
      <body>
        <div>
          <h1>XML Developer's Guide</h1>
          <h3>By Garghentini, Davide</h3>
          <h3>Price = 44.95</h3>
          <h2>Description</h2>
          <p>
            An in-depth look at creating applications
            with <b>XML</b>. For
            <i>beginners</i> or
            <i>advanced</i> developers.
          </p>
          <hr />
        </div>
        <div>
          <h1>Developing Applications with Visual Basic .NET</h1>
          <h3>By Spencer, Phil</h3>
          <h3>Price = 45.95</h3>
          <h2>Description</h2>
          <p>
            Get the expert insights, practical code
            samples, and best practices you need
            to advance your expertise with <b>Visual
            Basic .NET</b>. Learn how to create faster,
            more reliable applications based on
            professional, pragmatic guidance by today's
            top <i>developers</i>.
          </p>
          <hr />
        </div>
      </body>
    </html>
    ```

## <a name="see-also"></a>関連項目

- [XML リテラル](../../../language-reference/xml-literals/index.md)
- [Visual Basic での XML の操作](manipulating-xml.md)
- [XML](index.md)
- [方法: ファイル、文字列、またはストリームからの XML の読み込み](how-to-load-xml-from-a-file-string-or-stream.md)
- [LINQ](../linq/index.md)
- [Visual Basic における LINQ の概要](../linq/introduction-to-linq.md)
