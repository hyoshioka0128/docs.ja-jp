---
title: '方法: コード内でステートメントを分割および連結する'
ms.date: 07/20/2015
f1_keywords:
- vb._
helpviewer_keywords:
- colons (:)
- line continuation
- _ line-continuation character
- ': line separator character'
- Visual Basic code, line breaks in
- Visual Basic code, line breaks
- Visual Basic code, line continuation
- long lines of code
- line terminator
- line-continuation sequence
- underscores [Visual Basic], in code
- statements [Visual Basic], line continuation in
- line breaks [Visual Basic], in code
- line-continuation character [Visual Basic]
- Visual Basic code, line continuation in
- statements [Visual Basic], line breaks in
ms.assetid: dea01dad-a8ac-484a-bb3a-8c45a1b1eccc
ms.openlocfilehash: c78cbeaa5c2df2d4f2e3cce2b5b3fb8048ff3388
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84403253"
---
# <a name="how-to-break-and-combine-statements-in-code-visual-basic"></a>方法: コード内でステートメントを分割および連結する (Visual Basic)

コードを記述するときに、コード エディターで水平スクロールを必要とする長いステートメントを作成する場合があります。 これはコードの実行方法には影響しませんが、モニターに表示されたコードを読みにくくなります。 このような場合は、1 つの長いステートメントを複数の行に分割することを検討してください。

## <a name="to-break-a-single-statement-into-multiple-lines"></a>1 つのステートメントを複数の行に分割するには

行を分割する位置で行連結文字 (アンダースコア (`_`)) を使用します。 アンダースコアの直前にスペースを入力し、直後に行終端記号 (キャリッジ リターン) を入力するか、(バージョン 16.0 以降では) 直後にコメントを入力し、その後にキャリッジ リターンを入力する必要があります。

  > [!NOTE]
  > 場合によっては、行連結文字を省略すると、Visual Basic コンパイラはステートメントを暗黙的に次のコード行に継続します。 行連結文字を省略できる構文要素の一覧については、[ステートメント](../language-features/statements.md)に関する記事の「暗黙的な行連結」をご覧ください。

  次の例では、最後の行を除くすべての行を行連結文字で終了して、ステートメントが 4 行に分割されています。

  [!code-vb[VbVbcnConventions#20](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnConventions/VB/Class1.vb#20)]

  このシーケンスを使用すると、オンラインでも印刷された場合でもコードが読みやすくなります。

  行連結文字は、行の最後の文字である必要があります。 同じ行でその後に何かを続けることはできません。

  行連結文字を使用できる場所については、いくつかの制限があります。たとえば、引数名の途中で使用することはできません。 引数リストを行連結文字で分割することはできますが、引数の個々の名前はそのままにしておく必要があります。

  行連結文字を使用してコメントを継続することはできません。 コンパイラは、コメント内の文字に特別な意味があるかどうかを調べるわけではありません。 複数行のコメントでは、各行でコメント記号 (`'`) を繰り返します。

 各ステートメントを別々の行に配置するのが推奨される方法ですが、Visual Basic では同じ行に複数のステートメントを配置することもできます。

## <a name="to-place-multiple-statements-on-the-same-line"></a>同じ行に複数のステートメントを配置するには

次の例のように、ステートメントをコロン (`:`) で区切ります。

  [!code-vb[VbVbcnConventions#10](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnConventions/VB/Class1.vb#10)]

## <a name="see-also"></a>関連項目

- [プログラム構造とコード規則](program-structure-and-code-conventions.md)
- [ステートメント](../language-features/statements.md)
