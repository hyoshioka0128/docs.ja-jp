---
title: ローカル型の推論
ms.date: 07/20/2015
f1_keywords:
- local type inference
- vb.TypeInfer
helpviewer_keywords:
- Option Infer statement [Visual Basic]
- local type inference [Visual Basic]
- implicitly-typed local variables [Visual Basic]
- variables [Visual Basic], type inference
- inference [Visual Basic]
- type inference [Visual Basic]
ms.assetid: b8307f18-2e56-4ab3-a45a-826873f400f6
ms.openlocfilehash: 3979396d32aa5d3b853aa087d43f70d5987e510b
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84410400"
---
# <a name="local-type-inference-visual-basic"></a>ローカル型の推論 (Visual Basic)

Visual Basic コンパイラは、"*型推論*" を使用し、`As` 句を使用しないで宣言されたローカル変数のデータ型を判定します。 コンパイラは、初期化式の型から変数の型を推論します。 これにより、次の例で示すように、明示的に型を指定せずに変数を宣言できます。 この宣言の結果として、`num1` と `num2` の両方が整数として厳密に型指定されます。

[!code-vb[VbVbalrTypeInference#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrTypeInference/VB/Class1.vb#1)]

> [!NOTE]
> 前の例の `num2` を `Integer` として型指定しない場合は、`Dim num3 As Object = 3` や `Dim num4 As Double = 3` などの宣言を使用して別の型を指定できます。

> [!NOTE]
> 型推論は、非静的なローカル変数に対してのみ使用できます。クラス フィールド、プロパティ、または関数の型を判定するために使用することはできません。

ローカル型推論は、プロシージャ レベルで適用されます。 モジュール レベル (プロシージャまたはブロック内ではなく、クラス、構造体、モジュール、またはインターフェイス内) での変数の宣言に使用することはできません。 前述の例の `num2` が、プロシージャ内のローカル変数ではなくクラスのフィールドである場合、`Option Strict` が on に設定されている場合は宣言でエラーが発生し、`Option Strict` が off に設定されている場合は `num2` が `Object` として分類されます。 同様に、ローカル型推論は、`Static` として宣言されたプロシージャ レベルの変数に適用されません。

## <a name="type-inference-vs-late-binding"></a>型推論と遅延バインディング

型推論を使用するコードは、遅延バインディングに依存するコードに似ています。 ただし、型推論では、変数は `Object` のままではなく、厳密に型指定されます。 コンパイラは、コンパイル時に変数の初期化子を使用して変数の型を判定し、事前バインド コードを生成します。 前述の例では、`num2` は、`num1` と同様、`Integer` として型指定されます。

事前バインド変数の動作は、型が実行時にしか認識されない遅延バインド変数の動作とは異なります。 型が早期に認識されることにより、コンパイラは、実行前に問題を特定し、メモリを正確に割り当て、その他の最適化も行うことができます。 また、事前バインディングにより、Visual Basic 統合開発環境 (IDE) では、オブジェクトのメンバーに関する IntelliSense ヘルプを提供できます。 事前バインディングは、パフォーマンスのためにも推奨されます。 遅延バインド変数に格納されるデータはすべて `Object` 型としてラップする必要があり、実行時にその型のメンバーにアクセスすると、プログラムの速度が低下するためです。

## <a name="examples"></a>使用例

型推論は、ローカル変数が `As` 句を使用しないで宣言され、初期化されたときに発生します。 コンパイラは、割り当てられた初期値の型を変数の型として使用します。 たとえば、次のコード行はそれぞれ、`String` 型の変数を宣言します。

[!code-vb[VbVbalrTypeInference#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrTypeInference/VB/Class1.vb#2)]

次のコードは、同じ整数の配列を作成する 2 通りの同等の方法を示しています。

[!code-vb[VbVbalrTypeInference#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrTypeInference/VB/Class1.vb#3)]

ループ制御変数の型を判定するには、型推論を使用すると便利です。 次のコードでは、前述の例の `someNumbers2` が整数の配列であるため、コンパイラは、`number` が `Integer` であると推論します。

[!code-vb[VbVbalrTypeInference#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrTypeInference/VB/Class1.vb#4)]

次の例で示すように、ローカル型推論を `Using` ステートメントで使用して、リソース名の型を確定することができます。

[!code-vb[VbVbalrTypeInference#7](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrTypeInference/VB/Class1.vb#7)]

次の例で示すように、変数の型を関数の戻り値から推論することもできます。 `Process.GetProcesses` はプロセスの配列を返すため、`pList1` と `pList2` は両方ともプロセスの配列です。

[!code-vb[VbVbalrTypeInference#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrTypeInference/VB/Class1.vb#5)]

## <a name="option-infer"></a>Option Infer

`Option Infer` を使用すると、特定のファイルでローカル型推論を許可するかどうかを指定できます。 このオプションを有効化またはブロックするには、次のステートメントのいずれかをファイルの先頭に入力します。

`Option Infer On`

`Option Infer Off`

コードで `Option Infer` の値を指定しない場合、コンパイラの既定値は、`Option Infer On` です。

ファイルの `Option Infer` に設定した値が IDE またはコマンド ラインに設定した値と競合した場合は、ファイルの値が優先されます。

詳細については、「[Option Infer ステートメント](../../../language-reference/statements/option-infer-statement.md)」および「[[コンパイル] ページ、プロジェクト デザイナー (Visual Basic)](/visualstudio/ide/reference/compile-page-project-designer-visual-basic)」を参照してください。

## <a name="see-also"></a>関連項目

- [匿名型](../objects-and-classes/anonymous-types.md)
- [事前バインディングと遅延バインディング](../early-late-binding/index.md)
- [For Each...Next ステートメント](../../../language-reference/statements/for-each-next-statement.md)
- [For...Next ステートメント](../../../language-reference/statements/for-next-statement.md)
- [Option Infer ステートメント](../../../language-reference/statements/option-infer-statement.md)
- [-optioninfer](../../../reference/command-line-compiler/optioninfer.md)
- [Visual Basic における LINQ の概要](../linq/introduction-to-linq.md)
