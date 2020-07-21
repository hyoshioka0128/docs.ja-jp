---
title: XML 要素リテラル
ms.date: 07/20/2015
f1_keywords:
- vb.XmlLiteralElement
helpviewer_keywords:
- XML element literal [Visual Basic]
- element literal [Visual Basic]
- XML literals [Visual Basic], element
ms.assetid: 95039642-7893-48b7-b23f-45a6c55d8f67
ms.openlocfilehash: d6a91de4e279816bafd29f46bb4f5422cbd934ff
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84400190"
---
# <a name="xml-element-literal-visual-basic"></a>XML 要素リテラル (Visual Basic)

<xref:System.Xml.Linq.XElement> オブジェクトを表すリテラル。

## <a name="syntax"></a>構文

```xml
<name [ attributeList ] />
-or-
<name [ attributeList ] > [ elementContents ] </[ name ]>
```

## <a name="parts"></a>指定項目

- `<`

  必須です。 開始要素タグを開きます。

- `name`

  必須です。 要素名 形式は次のいずれかです。

  - 要素名のリテラル テキスト。`[ePrefix:]eName` の形式で指定します。各項目の内容を次に示します。

    |パーツ|説明|
    |---|---|
    |`ePrefix`|任意。 要素の XML 名前空間プレフィックス。 ファイル内またはプロジェクト レベルで `Imports` ステートメントで定義されたグローバル XML 名前空間か、この要素または親要素で定義されたローカル XML 名前空間である必要があります。|
    |`eName`|必須です。 要素名 形式は次のいずれかです。<br /><br /> - リテラル テキスト。 「[宣言する XML 要素と属性の名前](../../programming-guide/language-features/xml/names-of-declared-xml-elements-and-attributes.md)」を参照してください。<br />- `<%= eNameExp %>` 形式の埋め込み式。 `eNameExp` の型は `String` か、暗黙的に <xref:System.Xml.Linq.XName> に変換可能な型である必要があります。|

  - `<%= nameExp %>` 形式の埋め込み式。 `nameExp` の型は `String` か、暗黙的に <xref:System.Xml.Linq.XName> に変換可能な型である必要があります。 埋め込み式は、要素の終了タグでは使用できません。

- `attributeList`

  任意。 リテラルで宣言された属性のリスト。

  `attribute [ attribute ... ]`

  各 `attribute` の構文は次のいずれかです。

  - 属性割り当て。`[aPrefix:]aName=aValue` の形式で指定します。各項目の内容を次に示します。

    |パーツ|説明|
    |---|---|
    |`aPrefix`|任意。 属性の XML 名前空間プレフィックス。 `Imports` ステートメントで定義されたグローバル XML 名前空間か、この要素または親要素で定義されたローカル XML 名前空間である必要があります。|
    |`aName`|必須です。 属性の名前。 形式は次のいずれかです。<br /><br /> - リテラル テキスト。 「[宣言する XML 要素と属性の名前](../../programming-guide/language-features/xml/names-of-declared-xml-elements-and-attributes.md)」を参照してください。<br />- `<%= aNameExp %>` 形式の埋め込み式。 `aNameExp` の型は `String` か、暗黙的に <xref:System.Xml.Linq.XName> に変換可能な型である必要があります。|
    |`aValue`|任意。 属性の値。 形式は次のいずれかです。<br /><br /> - 引用符で囲まれたリテラル テキスト。<br />- `<%= aValueExp %>` 形式の埋め込み式。 任意の型を使用できます。|

  - `<%= aExp %>` 形式の埋め込み式。

- `/>`

  任意。 コンテンツのない空の要素であることを示します。

- `>`

  必須です。 開始タグまたは空の要素タグを終了します。

- `elementContents`

  任意。 要素のコンテンツ。

  `content [ content ... ]`

  各 `content` に次のいずれかを指定できます。

  - リテラル テキスト。 リテラル テキストがある場合、`elementContents` のすべての空白が有意になります。

  - `<%= contentExp %>` 形式の埋め込み式。

  - XML 要素リテラル。

  - XML コメント リテラル。 「[XML コメント リテラル](xml-comment-literal.md)」を参照してください。

  - XML 処理命令リテラル。 「[XML 処理命令リテラル](xml-processing-instruction-literal.md)」を参照してください。

  - XML CDATA リテラル。 「[XML CDATA リテラル](xml-cdata-literal.md)」を参照してください。

- `</[name]>`

  任意。 要素の終了タグを表します。 埋め込み式の結果である場合、省略可能な `name` パラメーターは使用できません。

## <a name="return-value"></a>戻り値

<xref:System.Xml.Linq.XElement> オブジェクト。

## <a name="remarks"></a>Remarks

XML 要素リテラル構文を使用して、コード内に <xref:System.Xml.Linq.XElement> オブジェクトを作成できます。

> [!NOTE]
> XML リテラルは、行連結文字を使用せずに、複数行にまたがることができます。 この機能を使用すると、XML ドキュメントからコンテンツをコピーして、Visual Basic プログラムに直接貼り付けることができます。

`<%= exp %>` 形式の埋め込み式を使用すると、XML 要素リテラルに動的な情報を追加できます。 詳細については、「[XML での埋め込み式](../../programming-guide/language-features/xml/embedded-expressions-in-xml.md)」を参照してください。

XML 要素リテラルは、Visual Basic コンパイラによって、<xref:System.Xml.Linq.XElement.%23ctor%2A> コンストラクターへの呼び出しに変換されます。また、必要に応じて、<xref:System.Xml.Linq.XAttribute.%23ctor%2A> コンストラクターへの呼び出しに変換されます。

## <a name="xml-namespaces"></a>XML 名前空間

XML 名前空間プレフィックスは、コード内で同じ名前空間の要素を使用して XML リテラルを何度も作成する必要がある場合に役立ちます。 グローバル XML 名前空間プレフィックス (`Imports` ステートメントを使用して定義) またはローカル プレフィックス (`xmlns:xmlPrefix="xmlNamespace"` 属性構文を使用して定義) を使用できます。 詳細については、「[Imports ステートメント (XML 名前空間)](../statements/imports-statement-xml-namespace.md)」を参照してください。

XML 名前空間のスコープ規則に従って、ローカル プレフィックスはグローバル プレフィックスよりも優先されます。 ただし、XML リテラルで XML 名前空間が定義されている場合、その名前空間は、埋め込み式に出現する式では使用できません。 埋め込み式は、グローバル XML 名前空間だけにアクセスできます。

XML リテラルで使用されているグローバル XML 名前空間はそれぞれ、Visual Basic コンパイラによって生成されたコード内では、1 つのローカル名前空間定義に変換されます。 使用されていないグローバル XML 名前空間は、生成されたコードに表示されません。

## <a name="example"></a>例

次の例は、入れ子にされた 2 つの空の要素が含まれる、シンプルな XML 要素を作成する方法を示しています。

[!code-vb[VbXMLSamples#20](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples9.vb#20)]

この例では、次のテキストが表示されます。 リテラルでは空の要素の構造が保持されることに注意してください。

```xml
<outer>
  <inner1></inner1>
  <inner2 />
</outer>
```

## <a name="example"></a>例

次の例は、埋め込み式を使用して要素に名前を付けて、属性を作成する方法を示しています。

[!code-vb[VbXMLSamples#21](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples9.vb#21)]

このコードを実行すると、次のテキストが表示されます。

```xml
<book isbn="1234" author="My Author" year="1999" title="My Book" />
```

## <a name="example"></a>例

次の例では、`ns` を名前空間プレフィックスとして宣言します。 その後、名前空間のプレフィックスを使用して XML リテラルを作成し、要素の最終形式を表示します。

[!code-vb[VbXMLSamples#22](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples10.vb#22)]

このコードを実行すると、次のテキストが表示されます。

```xml
<ns:outer xmlns:ns="http://SomeNamespace">
  <ns:middle xmlns:ns="http://NewNamespace">
    <ns:inner1 />
    <inner2 xmlns="http://SomeNamespace" />
  </ns:middle>
</ns:outer>
```

コンパイラによって、グローバル XML 名前空間のプレフィックスが、XML 名前空間のプレフィックス定義に変換されていることに注意してください。 \<ns:middle> 要素により、\<ns:inner1> 要素の XML 名前空間プレフィックスが再定義されます。 ただし、\<ns:inner2> 要素では、`Imports` ステートメントで定義された名前空間が使用されます。

## <a name="see-also"></a>関連項目

- <xref:System.Xml.Linq.XElement>
- [宣言する XML 要素と属性の名前](../../programming-guide/language-features/xml/names-of-declared-xml-elements-and-attributes.md)
- [XML コメント リテラル](xml-comment-literal.md)
- [XML CDATA リテラル](xml-cdata-literal.md)
- [XML リテラル](index.md)
- [Visual Basic での XML の作成](../../programming-guide/language-features/xml/creating-xml.md)
- [XML での埋め込み式](../../programming-guide/language-features/xml/embedded-expressions-in-xml.md)
- [Imports ステートメント (XML 名前空間)](../statements/imports-statement-xml-namespace.md)
