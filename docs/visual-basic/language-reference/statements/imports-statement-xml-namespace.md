---
title: Imports ステートメント - XML 名前空間
ms.date: 07/20/2015
f1_keywords:
- vb.ImportsXmlns
helpviewer_keywords:
- XML namespace [Visual Basic], importing
- imports [Visual Basic]
- Imports statement [Visual Basic]
- namespaces [Visual Basic], importing
ms.assetid: 1f4d50a6-08c7-4c2e-8206-ccae35fcd1b4
ms.openlocfilehash: a3184d68b0e4cdff5d4296a5a638e22b4e83bcde
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84404538"
---
# <a name="imports-statement-xml-namespace"></a>Imports ステートメント (XML 名前空間)

XML リテラルおよび XML 軸プロパティで使用するために、XML 名前空間プレフィックスをインポートします。

## <a name="syntax"></a>構文

```vb
Imports <xmlns:xmlNamespacePrefix = "xmlNamespaceName">
```

## <a name="parts"></a>指定項目

`xmlNamespacePrefix`  
任意。 XML 要素と属性で `xmlNamespaceName` を参照できる文字列。 `xmlNamespacePrefix` を指定していない場合、インポートされた XML 名前空間が既定の XML 名前空間になります。 有効な XML 識別子である必要があります。 詳細については、「[宣言する XML 要素と属性の名前](../../programming-guide/language-features/xml/names-of-declared-xml-elements-and-attributes.md)」を参照してください。

`xmlNamespaceName`  
必須です。 インポートされる XML 名前空間を識別する文字列。

## <a name="remarks"></a>Remarks

`Imports` ステートメントを使用して、XML リテラルおよび XML 軸プロパティで、または `GetXmlNamespace` 演算子に渡されるパラメーターとして、使用できるグローバル XML 名前空間を定義できます。 (`Imports` ステートメントを使用して、コードで型名を使用する場所で使用できる別名をインポートする方法については、「[Imports ステートメント (.NET 名前空間および型)](imports-statement-net-namespace-and-type.md)」を参照してください。)`Imports` ステートメントを使用して XML 名前空間を宣言する構文は、XML で使用する構文と同じです。 そのため、XML ファイルから名前空間宣言をコピーし、それを `Imports` ステートメントで使用できます。

XML 名前空間プレフィックスは、同じ名前空間にある XML 要素を繰り返し作成する場合に便利です。 `Imports` ステートメントで宣言された XML 名前空間プレフィックスは、ファイル内のすべてのコードで使用できるという意味でグローバルです。 XML 要素リテラルを作成するとき、および XML 軸プロパティにアクセスするときにそれを使用できます。 詳細については、「[XML 要素リテラル](../xml-literals/xml-element-literal.md)」と「[XML 軸プロパティ](../xml-axis/index.md)」を参照してください。

名前空間プレフィックスを指定せずにグローバル XML 名前空間を定義した場合 (`Imports <xmlns="http://SomeNameSpace>"` など)、その名前空間は既定の XML 名前空間と見なされます。 既定の XML 名前空間は、名前空間を明示的に指定していない XML 要素リテラルまたは XML 属性軸プロパティに使用されます。 さらに既定の名前空間は、指定された名前空間が空の名前空間 (つまり、`xmlns=""`) の場合にも使用されます。 既定の XML 名前空間は、XML リテラルの XML 属性、または名前空間を持たない XML 属性軸プロパティには適用されません。

XML リテラルに定義されている XML 名前空間は、*ローカル XML 名前空間*と呼ばれ、`Imports` ステートメントでグローバルとして定義されている XML 名前空間よりも優先されます。 `Imports` ステートメントで定義された XML 名前空間は、Visual Basic プロジェクトにインポートされた XML 名前空間よりも優先されます。 XML リテラルで XML 名前空間を定義している場合、そのローカル名前空間は埋め込み式に適用されません。

グローバル XML 名前空間は .NET Framework 名前空間と同じスコープおよび定義ルールに従います。 そのため、.NET Framework 名前空間をインポート可能などこでも、`Imports` ステートメントを含めてグローバル XML 名前空間を定義できます。 これには、コード ファイルとプロジェクトレベルの両方でインポートされた名前空間が含まれます。 プロジェクトレベルでインポートされた名前空間については、「[[参照設定] ページ (プロジェクト デザイナー) (Visual Basic)](/visualstudio/ide/reference/references-page-project-designer-visual-basic)」を参照してください。

各ソース ファイルには、任意の数の `Imports` ステートメントを含めることができます。 これらは、`Option Strict` ステートメントなど、オプションの宣言の後に続く必要があり、`Module` や `Class` ステートメントなどのプログラミング要素の宣言の前に記述する必要があります。

## <a name="example"></a>例

次の例では、既定の XML 名前空間と、プレフィックス `ns` で識別される XML 名前空間をインポートしています。 次に、両方の名前空間を使用する XML リテラルを作成しています。

[!code-vb[VbXMLSamples#45](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/Module1.vb#45)]

このコードを実行すると、次のテキストが表示されます。

```xml
<ns:outer xmlns="http://DefaultNamespace"
          xmlns:ns="http://NewNamespace">
  <ns:innerElement></ns:innerElement>
  <siblingElement></siblingElement>
  <innerElement />
</ns:outer>
```

## <a name="example"></a>例

次の例では、名前空間プレフィックス `ns` をインポートしています。 次に、名前空間プレフィックスを使用する XML リテラルを作成し、要素の最終形式を表示します。

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

コンパイラによって、XML 名前空間プレフィックスがグローバル プレフィックスからローカル プレフィックス定義に変換されていることに注意してください。

## <a name="example"></a>例

次の例では、名前空間プレフィックス `ns` をインポートしています。 その後、この名前空間のプレフィックスを使用して XML リテラルを作成し、修飾名 `ns:name` を持つ最初の子ノードにアクセスします。

[!code-vb[VbXMLSamples#19](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples8.vb#19)]

このコードを実行すると、次のテキストが表示されます。

`Patrick Hines`

## <a name="see-also"></a>関連項目

- [XML 要素リテラル](../xml-literals/xml-element-literal.md)
- [XML 軸プロパティ](../xml-axis/index.md)
- [宣言する XML 要素と属性の名前](../../programming-guide/language-features/xml/names-of-declared-xml-elements-and-attributes.md)
- [GetXmlNamespace 演算子](../operators/getxmlnamespace-operator.md)
