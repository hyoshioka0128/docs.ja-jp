---
title: Imports ステートメント - .NET 名前空間および型
ms.date: 07/20/2015
f1_keywords:
- vb.Imports
- imports
helpviewer_keywords:
- declared element names [Visual Basic], qualification
- imports [Visual Basic]
- Imports statement [Visual Basic]
- aliases [Visual Basic], Imports statement
- container elements [Visual Basic]
- namespaces [Visual Basic], importing
- Imports statement [Visual Basic], syntax
- import aliases [Visual Basic]
- aliases [Visual Basic], import
- declared elements [Visual Basic], container elements
ms.assetid: 7062f8aa-d890-4232-9eed-92836e13fb6e
ms.openlocfilehash: 39fa4e74f973bcb575b5751c387c0b879f4e398d
ms.sourcegitcommit: 17ee6605e01ef32506f8fdc686954244ba6911de
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74351066"
---
# <a name="imports-statement-net-namespace-and-type"></a>Imports ステートメント (.NET 名前空間および型)

名前空間の修飾なしで型名を参照できます。

## <a name="syntax"></a>構文

```vb
Imports [ aliasname = ] namespace
' -or-
Imports [ aliasname = ] namespace.element
```

## <a name="parts"></a>指定項目

|用語|定義|
|---|---|
|`aliasname`|任意。 コードで完全修飾文字列の代わりに `namespace` を参照できる*インポート エイリアス*または名前。 「 [Declared Element Names](../../programming-guide/language-features/declared-elements/declared-element-names.md)」を参照してください。|
|`namespace`|必須です。 インポートする名前空間の完全修飾名。 任意のレベルに入れ子になった名前空間の文字列を指定できます。|
|`element`|任意。 名前空間に宣言されているプログラミング要素の名前。 任意のコンテナー要素を指定できます。|

## <a name="remarks"></a>Remarks

`Imports` ステートメントを使用すると、特定の名前空間に含まれている型を直接参照できます。

1 つの名前空間名または入れ子になった名前空間の文字列を指定できます。 次の例に示すように、入れ子になった各名前空間は、ピリオド (`.`) で次の上位の名前空間と区別します。

```vb
Imports System.Collections.Generic
```

各ソース ファイルには、任意の数の `Imports` ステートメントを含めることができます。 これらは、`Option Strict` ステートメントなど、任意のオプションの宣言の後に続く必要があり、`Module` や `Class` ステートメントなどのプログラミング要素の宣言の前に記述する必要があります。

`Imports` は、ファイル レベルでのみ使用できます。 つまり、インポートの宣言コンテキストはソース ファイルである必要があり、名前空間、クラス、構造体、モジュール、インターフェイス、プロシージャ、またはブロックでは宣言できません。

`Imports` ステートメントによって、他のプロジェクトおよびアセンブリの要素をプロジェクトで使用できなくなることに注意してください。 インポートは、参照の設定の代わりになりません。 これにより、プロジェクトで既に使用可能な名前を修飾する必要がなくなるだけです。 詳細については、「[宣言された要素の参照](../../programming-guide/language-features/declared-elements/references-to-declared-elements.md)」の "コンテナー要素のインポート" に関するセクションを参照してください。

> [!NOTE]
> 暗黙的な `Imports` ステートメントを定義するには、「[[参照設定] ページ (プロジェクト デザイナー) (Visual Basic)](/visualstudio/ide/reference/references-page-project-designer-visual-basic)」を使用します。 詳細については、[方法:インポートした名前空間を追加または削除する (Visual Basic)](/visualstudio/ide/how-to-add-or-remove-imported-namespaces-visual-basic)」を参照してください。

## <a name="import-aliases"></a>インポート エイリアス

*インポート エイリアス*では、名前空間または型のエイリアスを定義します。 インポート エイリアスは、1 つまたは複数の名前空間で宣言されている、同じ名前の項目を使用する必要がある場合に便利です。 詳細と例については、「[宣言された要素の参照](../../programming-guide/language-features/declared-elements/references-to-declared-elements.md)」の「要素名を修飾する」を参照してください。

モジュール レベルで `aliasname` と同じ名前のメンバーを宣言することはできません。 そうすると、Visual Basic コンパイラでは、宣言されたメンバーに対してのみ `aliasname` が使用され、それをインポート エイリアスとして認識されなくなります。

インポート エイリアスの宣言に使用される構文は、XML 名前空間プレフィックスのインポートに使用されるものと似ていますが、結果は異なります。 インポート エイリアスは、コードで式として使用できますが、XML 名前空間プレフィックスは、XML リテラルまたは XML 軸プロパティで、修飾される要素名または属性名のプレフィックスとしてのみ使用できます。

### <a name="element-names"></a>要素の名前

`element` を指定する場合、*コンテナー要素*、つまり他の要素を含むことができるプログラミング要素を表す必要があります。 コンテナー要素には、クラス、構造体、モジュール、インターフェイス、および列挙が含まれます。

`Imports` ステートメントで使用できる要素のスコープは、`element`を指定したかどうかによって異なります。 `namespace` だけを指定する場合、その名前空間の一意の名前を持つすべてのメンバーと、その名前空間内のコンテナー要素のメンバーは、修飾なしで使用できます。 `namespace` と `element` の両方を指定すると、その要素のメンバーだけが修飾なしで使用できます。

## <a name="example"></a>例

次の例では、<xref:System.IO.DirectoryInfo> クラスを使用して、*C:\\* ディレクトリにあるすべてのフォルダーを返しています。

コードでは、ファイルの先頭に `Imports` ステートメントがありません。 そのため、<xref:System.IO.DirectoryInfo>、<xref:System.Text.StringBuilder>、および <xref:Microsoft.VisualBasic.ControlChars.CrLf> 参照はすべて、名前空間で完全修飾されています。

[!code-vb[VbVbalrStatements#152](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/class12.vb#152)]

## <a name="example"></a>例

次の例には、参照先の名前空間の `Imports` ステートメントが含まれています。 そのため、型は名前空間で完全修飾されている必要はありません。

[!code-vb[VbVbalrStatements#153](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/class12.vb#153)]

[!code-vb[VbVbalrStatements#154](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/class12.vb#154)]
  
## <a name="example"></a>例

次の例には、参照先の名前空間のエイリアスを作成する `Imports` ステートメントが含まれています。 型はエイリアスで修飾されています。

[!code-vb[VbVbalrStatements#155](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/class12.vb#155)]

[!code-vb[VbVbalrStatements#156](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/class12.vb#156)]

## <a name="example"></a>例

次の例には、参照先の型のエイリアスを作成する `Imports` ステートメントが含まれています。 エイリアスは、型を指定するために使用されています。

[!code-vb[VbVbalrStatements#157](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/class12.vb#157)]

[!code-vb[VbVbalrStatements#158](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/class12.vb#158)]
  
## <a name="see-also"></a>関連項目

- [Namespace ステートメント](namespace-statement.md)
- [Visual Basic における名前空間](../../programming-guide/program-structure/namespaces.md)
- [参照と Imports ステートメント](../../programming-guide/program-structure/references-and-the-imports-statement.md)
- [Imports ステートメント (XML 名前空間)](imports-statement-xml-namespace.md)
- [宣言された要素の参照](../../programming-guide/language-features/declared-elements/references-to-declared-elements.md)
