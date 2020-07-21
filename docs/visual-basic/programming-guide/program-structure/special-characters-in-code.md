---
title: コード内の特殊文字
ms.date: 07/20/2015
f1_keywords:
- vb.)
- vb.(
- vb.colon
- vb.!
- vb..
- 'vb.:'
helpviewer_keywords:
- special characters [Visual Basic], in code
- parentheses [Visual Basic], using in code
- colons (:)
- period character in code
- dot operator (.)
- dictionary access operator [Visual Basic]
- concatenation operators [Visual Basic], special characters in code
- concatenation operators [Visual Basic], vs. addition operator
- '! operator'
- separators [Visual Basic], using in code
- operators [Visual Basic], dictionary access
- ': separator character'
- member access operator [Visual Basic]
- addition operator [Visual Basic]
- operators [Visual Basic], member access
- . operator
- exclamation points
- separators
- exclamation point operator (!)
- Visual Basic code, special characters
ms.assetid: 310dce0c-45b5-4e0d-83e9-32df258d2a3e
ms.openlocfilehash: c9b170ed812474cdeee100f1dc388d5c7e85f2cc
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84400592"
---
# <a name="special-characters-in-code-visual-basic"></a>コード内の特殊文字 (Visual Basic)
コードで特殊文字 (アルファベットまたは数字以外の文字) を使用することが必要な場合があります。 Visual Basic の文字セットに含まれる区切り文字と特殊文字には、プログラム テキストの整理から、コンパイラやコンパイル済みプログラムが実行するタスクの定義まで、さまざまな用途があります。 実行するオペレーションを指定するのには使用されません。  
  
## <a name="parentheses"></a>かっこ  
 かっこは、`Sub` や `Function` などのプロシージャを定義するときに使用します。 プロシージャのすべての引数リストをかっこで囲む必要があります。 特に、複雑な式で演算子の既定の優先順位をオーバーライドするために、変数や引数を論理グループに配置する際にもかっこを使用します。 次の例を使って説明します。  
  
 [!code-vb[VbVbcnConventions#11](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnConventions/VB/Class1.vb#11)]  
  
 上記のコードの実行後、`d` の値は 8.225、`e` の値は 3 になります。 `d` の計算では、`+` よりも `/` が優先される既定の優先順位が使用されます。これは、`d = b + (c / a)` と同じです。 `e` の計算のかっこは、既定の優先順位をオーバーライドします。  
  
## <a name="separators"></a>[区切り記号]  
 区切り文字は、その名前が示すとおり、コードのセクションを区切ります。 Visual Basic では、区切り文字はコロン (`:`) です。 別々の行ではなく、1 つの行に複数のステートメントを含める場合は、区切り文字を使用します。 これにより、スペースが節約され、コードが読みやすくなります。 次の例は、コロンで区切られた 3 つのステートメントを示しています。  
  
 [!code-vb[VbVbcnConventions#12](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnConventions/VB/Class1.vb#12)]  
  
 詳細については、「[方法:コード内でステートメントを分割および連結する](how-to-break-and-combine-statements-in-code.md)」をご覧ください。  
  
 コロン (`:`) 文字は、ステートメント ラベルの識別にも使用されます。 詳細については、「[方法:ステートメントにラベルを付ける](how-to-label-statements.md)」をご覧ください。  
  
## <a name="concatenation"></a>連結  
 `&` 演算子は、"*連結*" (文字列の結合) に使用します。 数値を加算する `+` 演算子と混同しないでください。 数値を操作するときに `+` 演算子を使用して連結すると、間違った結果を得る可能性があります。 次に例を示します。  
  
 [!code-vb[VbVbcnConventions#13](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnConventions/VB/Class1.vb#13)]  
  
 上記のコードの実行後、`resultA` の値は 21.01、`resultB` の値は "10.0111" になります。  
  
## <a name="member-access-operators"></a>メンバー アクセス演算子  
 型のメンバーにアクセスするには、型名とメンバー名の間にドット (`.`) または感嘆符 (`!`) 演算子を使用します。  
  
### <a name="dot--operator"></a>ドット (.) 演算子  
 `.` 演算子は、クラス、構造体、インターフェイス、または列挙型でメンバー アクセス演算子として使用します。 メンバーには、フィールド、プロパティ、イベント、またはメソッドを指定できます。 次の例を使って説明します。  
  
 [!code-vb[VbVbcnConventions#14](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnConventions/VB/Class1.vb#14)]  
  
### <a name="exclamation-point--operator"></a>感嘆符 (!) 演算子  
 `!` 演算子は、ディクショナリ アクセス演算子としてクラスまたはインターフェイスでのみ使用します。 クラスまたはインターフェイスには、単一の `String` 引数を受け入れる既定のプロパティが必要です。 `!` 演算子の直後の識別子は、既定のプロパティに文字列として渡される引数値になります。 次に例を示します。  
  
 [!code-vb[VbVbcnConventions#15](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnConventions/VB/Class1.vb#15)]  
  
 `MsgBox` の 3 つの出力行では、いずれも値 `32856` が表示されます。 1 行目では、`index` プロパティへの従来のアクセスを使用し、2 行目では、`index` が `hasDefault` クラスの既定のプロパティであることを利用しています。3 行目では、クラスへのディクショナリ アクセスを使用しています。  
  
 `!` 演算子の 2 番目のオペランドは、二重引用符 (`" "`) で囲まれていない有効な Visual Basic 識別子である必要があります。 つまり、文字列リテラルや文字列変数は使用できません。 `"X"` は囲まれた文字列リテラルであるため、`MsgBox` 呼び出しの最後の行を次のように変更すると、エラーが生成されます。  
  
 `"Dictionary access returns " & hD!"X")`  
  
> [!NOTE]
> 既定のコレクションへの参照は明示的である必要があります。 特に、遅延バインディング変数で `!` 演算子を使用することはできません。  
  
 `!` 文字は、`Single` 型の文字としても使用されます。  
  
## <a name="see-also"></a>関連項目

- [プログラム構造とコード規則](program-structure-and-code-conventions.md)
- [型文字](../language-features/data-types/type-characters.md)
