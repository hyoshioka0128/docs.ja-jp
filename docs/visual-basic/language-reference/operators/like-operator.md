---
title: Like 演算子
ms.date: 07/20/2015
f1_keywords:
- Like
- vb.Like
helpviewer_keywords:
- similar to
- pattern matching
- Like operator [Visual Basic]
- '? symbol, wildcard character'
- string comparison [Visual Basic], Like operator
- strings [Visual Basic], comparing
- comparison operators [Visual Basic]
- symbols, wildcard
- wildcards, Like operator
- strings [Visual Basic], matching
- string comparison [Visual Basic], sorting data
- data [Visual Basic], sorting
- text [Visual Basic], comparing
- operators [Visual Basic], pattern-matching
- data [Visual Basic], string comparisons
- string comparison [Visual Basic], Like operators
ms.assetid: 966283ec-80e2-4294-baa8-c75baff804f9
ms.openlocfilehash: 4279d90c74c80403146448a8ba5a6051ec9d12f6
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84401558"
---
# <a name="like-operator-visual-basic"></a>Like 演算子 (Visual Basic)
文字列をパターンと比較します。  

> [!IMPORTANT]
> `Like` 演算子は、現在、.NET Core および .NET Standard のプロジェクトではサポートされていません。

## <a name="syntax"></a>構文  
  
```vb  
result = string Like pattern  
```  
  
## <a name="parts"></a>指定項目  
 `result`  
 必須です。 任意の `Boolean` 変数。 結果は、`string` が `pattern` を満たすかどうか示す `Boolean` 値です。  
  
 `string`  
 必須です。 任意のブール型 ( `String` ) の式を指定します。  
  
 `pattern`  
 必須です。 「解説」で説明されているパターン マッチング規則に準拠した `String` 式を指定します。  
  
## <a name="remarks"></a>Remarks  
 `string` の値が `pattern` に格納されているパターンを満たす場合、`result` は `True` になります。 文字列がパターンを満たさない場合、`result` は `False` になります。 `string` と `pattern` の両方が空の文字列の場合、結果は `True` になります。  
  
## <a name="comparison-method"></a>比較方法  
 `Like` 演算子の動作は、[Option Compare ステートメント](../statements/option-compare-statement.md)に基づきます。 各ソース ファイルの既定の文字列比較方法は `Option Compare Binary` です。  
  
## <a name="pattern-options"></a>パターンのオプション  
 組み込みのパターン マッチングでは、文字列比較に使用できるさまざまなツールが用意されています。 パターン マッチング機能を使用すると、`string` 内の各文字を、特定の文字、ワイルドカード文字、文字リスト、または文字範囲と一致させることができます。 次の表に、`pattern` で使用できる文字と、それらが何に一致するかを示します。  
  
|`pattern` 内の文字|`string` 内の以下に一致|  
|-----------------------------|-------------------------|  
|`?`|任意の 1 文字|  
|`*`|0 個以上の文字|  
|`#`|任意の 1 つの数字 (0 ～ 9)|  
|`[charlist]`|`charlist` 内の任意の 1 文字|  
|`[!charlist]`|`charlist` 内にない任意の 1 文字|  
  
## <a name="character-lists"></a>文字リスト  
 角かっこ (`[ ]`) で囲まれた 1 つ以上の文字のグループ (`charlist`) と、`string` 内の任意の 1 文字を一致させることができます。このグループには、数字を含むほぼすべての文字コードを含めることができます。  
  
 `charlist` の先頭にある感嘆符 (`!`) は、`charlist` 内の文字を除く任意の文字が `string` で見つかった場合に一致することを意味します。 感嘆符を角かっこの外側で使用すると、感嘆符自体を照合できます。  
  
## <a name="special-characters"></a>特殊文字  
 特殊文字の左角かっこ (`[`)、疑問符 (`?`)、番号記号 (`#`)、およびアスタリスク (`*`) を一致させるには、これらを角かっこで囲みます。 右角かっこ (`]`) は、グループ内でそれ自体を一致させるために使用できませんが、グループの外側で個別の文字として使用できます。  
  
 文字シーケンス `[]` は、長さが 0 の文字列 (`""`) と見なされます。 ただし、これを角かっこで囲まれた文字リストの一部にすることはできません。 `Like` を 2 回使用すると、`string` 内のある場所に、文字グループのいずれかの文字が含まれているか、または文字がまったく含まれていないか確認できます。 例については、「[方法: 文字列がパターンに一致するかを調べる](../../programming-guide/language-features/operators-and-expressions/how-to-match-a-string-against-a-pattern.md)」を参照してください。  
  
## <a name="character-ranges"></a>文字範囲  
 ハイフン (`–`) を使用して範囲の下限と上限を区切ることにより、`charlist` で文字の範囲を指定できます。 たとえば、`string` 内の対応する文字位置に、`A`–`Z` の範囲の任意の文字が含まれている場合、`[A–Z]` は一致と見なされます。また、対応する文字位置に `H`–`L` の範囲外の文字が含まれている場合、`[!H–L]` は一致と見なされます。  
  
 文字の範囲を指定する場合、昇順の並べ替え順序、つまり、最小から最大の順序で指定する必要があります。 したがって、`[A–Z]` は有効なパターンですが、`[Z–A]` は有効ではありません。  
  
### <a name="multiple-character-ranges"></a>複数の文字範囲  
 同じ文字位置の複数の範囲を指定するには、区切り記号を使用せずに同じ角かっこ内にそれらの範囲を配置します。 たとえば、`string` 内の対応する文字位置に範囲 `A`–`C` または範囲 `X`–`Z` 内の文字が含まれる場合、`[A–CX–Z]` は一致と見なされます。  
  
### <a name="usage-of-the-hyphen"></a>ハイフンの使用  
 ハイフン (`–`) を `charlist` の先頭 (感嘆符がある場合はその後)、または末尾に配置することで、ハイフン自体と一致させることができます。 その他の場所では、ハイフンは、ハイフンの両側の文字によって定められた文字の範囲を示します。  
  
## <a name="collating-sequence"></a>照合順序  
 指定した範囲の意味は、実行時の文字の順序によって異なります。`Option Compare` と、コードが実行されるシステムのロケール設定によって決まります。 `Option Compare Binary` を使用すると、範囲 `[A–E]` は `A`、`B`、`C`、`D`、および `E` と一致します。 `Option Compare Text` を使用すると、`[A–E]` は `A`、`a`、`À`、`à`、`B`、`b`、`C`、`c`、`D`、`d`、`E`、および `e` と一致します。 この範囲は `Ê` および `ê` とは一致しません。これは、並べ替え順序で、アクセント記号付き文字がアクセント記号なし文字の後になるためです。  
  
## <a name="digraph-characters"></a>digraph 文字  
 言語によっては、2 つの個別の文字を表すアルファベット文字があります。 たとえば、いくつかの言語では、文字 `æ` を使用して文字 `a` と文字 `e` (これらが一緒に現れる場合) を表します。 `Like` 演算子は、1 つの digraph 文字と 2 つの個別文字が同等であると認識します。  
  
 digraph 文字を使用する言語がシステムのロケール設定で指定されている場合、`pattern` または `string` に 1 つの digraph 文字があると、その digraph 文字は他の文字列内の同等の連続する 2 文字に一致します。 同様に、角かっこ (それ自体、リスト内、または範囲内) で囲まれた `pattern` 内の digraph 文字は、`string` 内の同等の連続する 2 文字と一致します。  
  
## <a name="overloading"></a>オーバーロード  
 `Like` 演算子は "*オーバーロード*" できます。つまり、オペランドがクラスまたは構造体の型を持っているときに、クラスまたは構造体はその動作を再定義できます。 コードで、そのようなクラスまたは構造体に対してこの演算子が使用される場合は、再定義された動作を理解していることを確認してください。 詳細については、「 [Operator Procedures](../../programming-guide/language-features/procedures/operator-procedures.md)」を参照してください。  
  
## <a name="example"></a>例  
 この例では、`Like` 演算子を使用して、文字列をさまざまなパターンと比較します。 結果は、各文字列がパターンを満たすかどうかを示す `Boolean` 変数に格納されます。  
  
 [!code-vb[VbVbalrOperators#30](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#30)]  
  
## <a name="see-also"></a>関連項目

- <xref:Microsoft.VisualBasic.Strings.InStr%2A>
- <xref:Microsoft.VisualBasic.Strings.StrComp%2A>
- [比較演算子](comparison-operators.md)
- [Visual Basic における演算子の優先順位](operator-precedence.md)
- [機能別の演算子一覧](operators-listed-by-functionality.md)
- [Option Compare ステートメント](../statements/option-compare-statement.md)
- [演算子および式](../../programming-guide/language-features/operators-and-expressions/index.md)
- [方法: 文字列がパターンに一致するかを調べる](../../programming-guide/language-features/operators-and-expressions/how-to-match-a-string-against-a-pattern.md)
