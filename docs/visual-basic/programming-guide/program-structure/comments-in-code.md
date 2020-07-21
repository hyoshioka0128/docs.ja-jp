---
title: コード内のコメント
ms.date: 07/20/2015
helpviewer_keywords:
- Uncomment button
- REM statement [Visual Basic]
- comments [Visual Basic], in code
- comments [Visual Basic], Visual Basic code
- Comment button
- buttons [Visual Basic], Uncomment
- buttons [Visual Basic], Comment
- code comments [Visual Basic], Visual Basic
- Visual Basic code, comments
- comments
- code comments
ms.assetid: 90136fba-22eb-49f9-ba81-63db629b4a47
ms.openlocfilehash: b50e76b8f832c3a214ca54f97bab8b0b6789ac25
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84403318"
---
# <a name="comments-in-code-visual-basic"></a>コード内のコメント (Visual Basic)
コード例にはコメント記号 (`'`) がしばしば見られます。 この記号は、後続のテキスト ("*コメント*") を無視するように Visual Basic コンパイラに指示します。 コメントは、コードを読むユーザーに役立つように追加される簡単な説明です。  
  
 プロシージャの先頭に、そのプロシージャの機能の特性 (何を実行するか) について説明する簡単なコメントを常に配置するのは、推奨されるプログラミング方法です。 コードを作成した本人にとっても、コードを調べる他人にとっても、この説明は役に立ちます。 実装の詳細 (プロシージャの実行手順) は、機能の特性を説明するコメントとは別に記述する必要があります。 実装の詳細を記述に入れる場合は、関数を更新するときにその説明も更新してください。  
  
 同じ行のステートメントの後にコメントを入れたり、1 行全体をコメントにしたりできます。 両方の例を次のコードに示します。  
  
 [!code-vb[VbVbcnConventions#16](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnConventions/VB/Class1.vb#16)]  
  
 コメントを複数行に記述する必要がある場合は、以下に例を示すとおりに、各行にコメント記号を記述します。  
  
 [!code-vb[VbVbcnConventions#17](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnConventions/VB/Class1.vb#17)]  
  
## <a name="commenting-guidelines"></a>コメントのガイドライン  
 次の表は、どの種類のコメントをコードのセクションの前に配置できるかに関する一般的なガイドラインを示しています。 これらは推奨事項です。Visual Basic にはコメントの追加に関する規則はありません。 コードの作成者自身およびコードを読む他のユーザーに最適な内容を記述してください。  
  
|||  
|---|---|  
|コメント タイプ|コメントの説明|  
|目的|プロシージャが行う内容 (手順ではありません) を説明します。|  
|外部からの影響|各外部変数、コントロール、開いているファイル、またはプロシージャからアクセスされるその他の要素の一覧を示します。|  
|エフェクト|影響を受ける外部変数、コントロール、またはファイル、およびその効果 (明白でない場合のみ) の一覧を示します。|  
|受け取る値|引数の目的を指定します。|  
|戻り値|プロシージャから返される値について説明します。|  
  
 次のことに留意してください。  
  
- 重要な変数を宣言する場合は、宣言した変数の用途を説明するためのインライン コメントを必ず前に配置します。  
  
- コメントには複雑な実装の詳細だけを記述して済むように、変数、コントロール、およびプロシージャにはわかりやすい名前を付けます。  
  
- 同じ行の行連結シーケンスの後にコメントを付けることはできません。  
  
 コード ブロックのコメント記号を追加または削除するには、1 行以上のコードを選択し、 **[編集]** ツールバーの **[コメント]** (![Visual Studio の Visual Basic の [コメント] ボタン](./media/comments-in-code/visual-basic-comment-button.gif)) および **[コメント解除]** (![Visual Studio の Visual Basic の [コメント解除] ボタン](./media/comments-in-code/visual-basic-uncomment-button.gif)) ボタンを選択します。  
  
> [!NOTE]
> テキストの前に `REM` キーワードを付けて、コードにコメントを追加することもできます。 ただし、`'` 記号および **[コメント]** / **[コメント解除]** ボタンの方が使いやすく、必要なスペースとメモリが少なくて済みます。  
  
## <a name="see-also"></a>関連項目

- [基本的な機能 - XML コメントによるコードの文書化](https://docs.microsoft.com/archive/msdn-magazine/2009/may/documenting-your-code-with-xml-comments)
- [方法: XML ドキュメントを作成する](how-to-create-xml-documentation.md)
- [XML のコメント用タグ](../../language-reference/xmldoc/index.md)
- [プログラム構造とコード規則](program-structure-and-code-conventions.md)
- [REM ステートメント](../../language-reference/statements/rem-statement.md)
