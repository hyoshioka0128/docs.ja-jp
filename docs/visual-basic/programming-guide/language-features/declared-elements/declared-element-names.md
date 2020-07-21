---
title: 宣言された要素の名前
ms.date: 07/20/2015
helpviewer_keywords:
- declared elements [Visual Basic], case sensitivity
- names [Visual Basic], Visual Basic rules
- naming conventions [Visual Basic]
- element names [Visual Basic]
- declared elements [Visual Basic], identifiers
- declarations [Visual Basic], elements
- declared elements [Visual Basic], valid names
- '[] escape characters [Visual Basic]'
- names [Visual Basic], elements
- declaration statements [Visual Basic], declared elements
- declaring elements [Visual Basic]
- identifiers [Visual Basic], declared elements
- case sensitivity, declared element names
- escape characters [Visual Basic]
- names [Visual Basic], declared elements
- declared elements [Visual Basic], about declared elements
- escaped names [Visual Basic]
- declared elements [Visual Basic], names
- names [Visual Basic], naming conventions
- identifiers [Visual Basic], elements
ms.assetid: 09d8843b-c0dc-4afe-9dab-87c439a69e66
ms.openlocfilehash: cdba2b5f3e17fc6666ca653abd7f4bd7dfb31c4a
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84392923"
---
# <a name="declared-element-names-visual-basic"></a>宣言された要素の名前 (Visual Basic)
宣言されたすべての要素には名前が付いています。これは*識別子*とも呼ばれ、コードが参照するために使用するものです。  
  
## <a name="rules"></a>ルール  
 Visual Basic 内の要素名は、次のルールを守る必要があります。  
  
- 先頭は英文字またはアンダースコア (`_`) にする必要があります。  
  
- 含めることができるのは、英字、10 進数の数字、アンダースコアのみです。  
  
- アンダースコアで始まる場合は、少なくとも 1 つの英字または 10 進数の数字が含まれている必要があります。  
  
- 1023 文字以下にする必要があります。  
  
 1023 文字の長さの制限は、`outerNamespace.middleNamespace.innerNamespace.thisClass.thisElement` など、完全修飾名の文字列全体にも適用されます。  
  
 いくつかの有効な要素名を次の例に示します。  
  
 `aB123__45`  
  
 `_567`  
  
 いくつかの無効な要素名を次の例に示します。 1 つ目にはアンダースコアのみが含まれ、2 つ目は 10 進数の数字で始まり、3 つ目には無効な文字 ($) が含まれています。  
  
 `' Three INVALID element names`  
  
 `_`  
  
 `12ABC`  
  
 `xyz$wv`  
  
> [!CAUTION]
> アンダースコア (`_`) で始まる要素名は、[言語への非依存性、および言語非依存コンポーネント](../../../../standard/language-independence-and-language-independent-components.md) (CLS) の一部ではないため、CLS 準拠のコードでは、このような名前を定義するコンポーネントを使用できません。 ただし、要素名の他の位置にあるアンダースコアは CLS に準拠しています。  
  
### <a name="name-length-guidelines"></a>名前の長さのガイドライン  
 現実問題として、名前は、可能な限り短くしながらも、要素の性質を明確に特定するものにする必要があります。 これにより、コードの読みやすさが向上し、行の長さとソース ファイルのサイズが減少します。  
  
 一方、要素が何を表し、コードがそれをどのように使用するかを適切に説明できないほど短い名前にはしないでください。 これはコードの読みやすさのために重要です。 他のユーザーが理解しようとするとき、またはユーザー自身がそれを記述してから長い間が経っている場合でも、適切な要素名にすることでかなりの時間を節約できます。  
  
## <a name="escaped-names"></a>エスケープされた名前  
 一般に、要素名は、Visual Basic によって予約されているキーワード (`Case` や `Friend` など) と一致しないようにする必要があります。 ただし、*エスケープされた名前*を定義できます。これは、角かっこ (`[ ]`) で囲まれています。 エスケープされた名前は、角かっこによってあいまいさが解消されるため、どの Visual Basic キーワードとも一致させることができます。 また、コード内で後で名前を参照するときにも、角かっこを使用します。  
  
 通常、エスケープされた名前は、次の場合にのみ使用してください。  
  
- コードが、名前として使用されるキーワードを予約しなかった以前のバージョンの Visual Basic から移行された。または、  
  
- 指定されたキーワードが予約されていない別の言語で記述されたコードを操作している。  
  
 それ以外の場合、名前がキーワードと競合する場合は、要素の名前を変更することを検討してください。 統合開発環境 (IDE) を使用すると、この操作を簡単に実行できます。 詳細については、[リファクタリング](/visualstudio/ide/refactoring-in-visual-studio)に関するページを参照してください。  
  
## <a name="case-sensitivity-in-names"></a>名前の大文字と小文字の区別  
 Visual Basic の要素名は、大文字と小文字を区別しません。 つまり、英字の大文字と小文字の違いしかない 2 つの名前を比較した場合、コンパイラはそれらを同じ名前と解釈します。 たとえば、 `ABC` と `abc` は、宣言された同じ要素を参照していると見なされます。  
  
 しかし、共通言語ランタイム (CLR) のバインディングでは大文字と小文字が区別されます。 このため、アセンブリまたは DLL を作成し、他のアセンブリで使用できるようにすると、名前の大文字と小文字が区別されるようになります。 たとえば、 `ABC`という名前の要素を持つクラスを定義し、他のアセンブリから共通言語ランタイムを通じてこのクラスを使用する場合は、この要素を `ABC`として参照する必要があります。 後でクラスを再コンパイルして要素の名前を `abc` に変更すると、このクラスを使用していた他のアセンブリがこの要素にアクセスできなくなります。 したがって、アセンブリを更新してリリースするときは、パブリックな要素の名前の大文字と小文字を変更しないでください。  
  
## <a name="names-and-locales"></a>名前とロケール  
 名前の比較は、ロケールに依存しません。 2 つの名前が 1 つのロケールで一致する場合は、すべてのロケールで一致することが保証されます。  
  
## <a name="see-also"></a>関連項目

- [宣言された要素](index.md)
- [宣言された要素の特性](declared-element-characteristics.md)
- [宣言された要素の参照](references-to-declared-elements.md)
- [ステートメント](../../../language-reference/statements/index.md)
