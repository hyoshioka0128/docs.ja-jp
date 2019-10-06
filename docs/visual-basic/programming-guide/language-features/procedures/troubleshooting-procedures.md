---
title: プロシージャのトラブルシューティング (Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- troubleshooting Visual Basic, procedures
- procedures [Visual Basic], troubleshooting
- Visual Basic code, procedures
- troubleshooting procedures
- procedures [Visual Basic], about procedures
ms.assetid: 525721e8-2e02-4f75-b5d8-6b893462cf2b
ms.openlocfilehash: d8309b9bd63a2a3d1b0b56f97be121a06b78d6b6
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/01/2019
ms.locfileid: "71700129"
---
# <a name="troubleshooting-procedures-visual-basic"></a>プロシージャのトラブルシューティング (Visual Basic)

このページでは、プロシージャの使用時に発生する可能性がある一般的な問題をいくつか紹介します。

## <a name="returning-an-array-type-from-a-function-procedure"></a>関数プロシージャから配列型を返す

 @No__t 0 のプロシージャが配列のデータ型を返す場合、`Function` の名前を使用して配列の要素に値を格納することはできません。 これを実行しようとすると、コンパイラは `Function` の呼び出しとして解釈します。 次の例では、コンパイラエラーが生成されます。

 ```vb
 Function AllOnes(n As Integer) As Integer()
     For i = 1 To n - 1
         ' The following statement generates a COMPILER ERROR.
         AllOnes(i) = 1
     Next
     ' The following statement generates a COMPILER ERROR.
     Return AllOnes()
 End Function
 ```
  
 ステートメント `AllOnes(i) = 1` は、間違ったデータ型 (`Integer` 配列ではなくスカラー `Integer`) の引数を指定して `AllOnes` を呼び出すと表示されるため、コンパイラエラーが生成されます。 ステートメント `Return AllOnes()` は、引数を指定せずに `AllOnes` を呼び出すように見えるため、コンパイラエラーが生成されます。

 **正しい方法:** 返される配列の要素を変更できるようにするには、内部配列をローカル変数として定義します。 次の例では、エラーなしでコンパイルされます。

 [!code-vb[VbVbcnProcedures#66](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#66)]

## <a name="argument-not-being-modified-by-procedure-call"></a>引数がプロシージャ呼び出しによって変更されていません

 プロシージャが、呼び出し元のコードの引数の基になるプログラミング要素を変更できるようにする場合は、参照渡しで渡す必要があります。 ただし、プロシージャは、値によって渡された場合でも、参照型引数の要素にアクセスできます。

- **基になる変数**。 プロシージャが基になる変数の要素自体の値を置き換えることができるようにするには、プロシージャで[ByRef](../../../language-reference/modifiers/byref.md)パラメーターを宣言する必要があります。 また、呼び出し元のコードでは、引数をかっこで囲む必要はありません。これは @no__t 0 渡しの機構をオーバーライドするためです。

- **参照型の要素**。 パラメーター [ByVal](../../../language-reference/modifiers/byval.md)を宣言する場合、プロシージャは、基になる変数要素自体を変更することはできません。 ただし、引数が参照型の場合、プロシージャは、変数の値を置き換えることができなくても、その参照先のオブジェクトのメンバーを変更できます。 たとえば、引数が配列変数の場合、プロシージャは新しい配列を割り当てることはできませんが、1つ以上の要素を変更することができます。 変更された要素は、呼び出し元のコード内の基になる配列変数に反映されます。

 次の例では、値によって配列変数を受け取り、その要素を操作する2つのプロシージャを定義します。 プロシージャ `increase` は、各要素に1つずつ追加します。 手順 `replace` @no__t 新しい配列をパラメーターに割り当ててから、各要素に1を追加します。 ただし、再割り当ては、`a()` が `ByVal` と宣言されているため、呼び出し元のコード内の基になる配列変数には影響しません。

 [!code-vb[VbVbcnProcedures#35](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#35)]

 [!code-vb[VbVbcnProcedures#38](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#38)]

 次の例では、`increase` および `replace` を呼び出します。

 [!code-vb[VbVbcnProcedures#37](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#37)]

 最初の `MsgBox` 呼び出しでは、"増加後 (n)" が表示されます。11、21、31、41 "。 @No__t-0 は参照型であるため、`increase` は `ByVal` で渡される場合でも、メンバーを変更できます。

 2番目の `MsgBox` 呼び出しは、"置換後 (n):11、21、31、41 "。 @No__t-0 が-1 @no__t 渡されるため、`replace` では、新しい配列を割り当てることによって変数 `n` を変更することはできません。 @No__t-0 @no__t 新しい配列インスタンスを作成して、それをローカル変数 `a` に割り当てると、呼び出し元のコードによって渡された `n` への参照が失われます。 @No__t-0 のメンバーをインクリメントすると、ローカル配列 `k` のみが影響を受けます。

 **正しい方法:** 基になる変数要素自体を変更できるようにするには、参照渡しで渡します。 次の例では、呼び出し元のコードで配列を別の配列に置き換えることができるようにする `replace` の宣言の変更を示しています。

 [!code-vb[VbVbcnProcedures#64](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#64)]

## <a name="unable-to-define-an-overload"></a>オーバーロードを定義できません

 オーバーロードされたバージョンのプロシージャを定義する場合は、同じ名前で、別のシグネチャを使用する必要があります。 コンパイラが同じシグネチャを持つオーバーロードから宣言を区別できない場合は、エラーが生成されます。

 プロシージャの*シグネチャ*は、プロシージャ名とパラメーターリストによって決まります。 各オーバーロードは、他のすべてのオーバーロードと同じ名前を持つ必要がありますが、シグネチャの他のコンポーネントの少なくとも1つでは、それらのすべてが異なる必要があります。 詳細については、「 [Procedure Overloading](procedure-overloading.md)」を参照してください。

 次の項目は、パラメーターリストに関連する場合でも、プロシージャのシグネチャのコンポーネントではありません。

- @No__t-0、`Shared`、`Static` などのプロシージャ修飾子キーワード

- パラメーター名

- パラメーター修飾子キーワード (`ByRef` および `Optional` など)

- 戻り値のデータ型 (変換演算子を除く)

 前の項目のうち1つ以上を変更してプロシージャをオーバーロードすることはできません。

 **正しい方法:** プロシージャオーバーロードを定義できるようにするには、シグネチャを変更する必要があります。 同じ名前を使用する必要があるため、パラメーターの数、順序、またはデータ型を変更する必要があります。 ジェネリックプロシージャでは、型パラメーターの数を変更できます。 変換演算子 ([CType 関数](../../../language-reference/functions/ctype-function.md)) では、戻り値の型を変更できます。

### <a name="overload-resolution-with-optional-and-paramarray-arguments"></a>省略可能な引数と ParamArray 引数を使用したオーバーロードの解決

 1つ以上の[省略可能](../../../language-reference/modifiers/optional.md)なパラメーターまたは[ParamArray](../../../language-reference/modifiers/paramarray.md)パラメーターを使用してプロシージャをオーバーロードする場合は、*暗黙的なオーバーロード*の複製を避ける必要があります。 詳細については、「[プロシージャのオーバーロードに関する考慮事項](considerations-in-overloading-procedures.md)」を参照してください。

## <a name="calling-a-wrong-version-of-an-overloaded-procedure"></a>オーバーロードされたプロシージャの間違ったバージョンの呼び出し

 プロシージャに複数のオーバーロードされたバージョンがある場合は、すべてのパラメーターリストを理解し、Visual Basic がオーバーロード間の呼び出しを解決する方法を理解しておく必要があります。 それ以外の場合は、意図したもの以外のオーバーロードを呼び出すことができます。

 呼び出すオーバーロードを決定したら、次の規則に注意してください。

- 正しい数の引数を正しい順序で指定してください。

- 理想的には、引数は、対応するパラメーターとまったく同じデータ型を持つ必要があります。 いずれの場合も、各引数のデータ型は、対応するパラメーターのデータ型に拡大変換する必要があります。 これは、 [Option Strict ステートメント](../../../language-reference/statements/option-strict-statement.md)が `Off` に設定されている場合でも同様です。 オーバーロードに引数リストからの縮小変換が必要な場合、そのオーバーロードは呼び出される対象ではありません。

- 拡張を必要とする引数を指定する場合は、対応するパラメーターのデータ型にできるだけ近いデータ型を指定してください。 引数のデータ型を受け入れるオーバーロードが2つ以上ある場合、コンパイラは、より少ない拡大率でを呼び出すオーバーロードの呼び出しを解決します。

 引数を準備するときに[CType 関数](../../../language-reference/functions/ctype-function.md)変換キーワードを使用すると、データ型の不一致の可能性を減らすことができます。

### <a name="overload-resolution-failure"></a>オーバーロードの解決エラー

 オーバーロードされたプロシージャを呼び出すと、コンパイラはオーバーロードの1つを除くすべてを削除しようとします。 成功した場合は、そのオーバーロードの呼び出しを解決します。 すべてのオーバーロードを除外する場合、または対象となるオーバーロードを1つの候補に減らすことができない場合は、エラーが生成されます。

 次の例は、オーバーロードの解決プロセスを示しています。

 [!code-vb[VbVbcnProcedures#62](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#62)]

 [!code-vb[VbVbcnProcedures#63](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#63)]

 最初の呼び出しでは、最初の引数の型 (`Short`) が対応するパラメーター (`Byte`) の型に限定されるため、コンパイラは最初のオーバーロードを削除します。 次に3番目のオーバーロードを削除します。これは、2番目のオーバーロード (`Short` および `Single`) の各引数の型が、3番目のオーバーロード (`Integer` および `Single`) の対応する型に拡大変換されるためです。 2番目のオーバーロードでは、より少ない拡大が必要になるため、コンパイラはこれを呼び出しに使用します。

 2番目の呼び出しでは、コンパイラは、縮小に基づいてオーバーロードのいずれかを削除することはできません。 最初の呼び出しの場合と同じ理由で3番目のオーバーロードを削除します。これは、引数の型をより拡大して、2番目のオーバーロードを呼び出すことができるためです。 ただし、コンパイラは1番目と2番目のオーバーロード間で解決できません。 各には、もう一方の型に拡大変換する定義済みのパラメーター型が1つあります (`Byte` ~ `Short`、`Single` から `Double`)。 そのため、コンパイラはオーバーロードの解決エラーを生成します。

 **正しい方法:** オーバーロードされたプロシージャをあいまいで呼び出すことができるようにするには、 [CType 関数](../../../language-reference/functions/ctype-function.md)を使用して、引数のデータ型をパラメーターの型と照合します。 次の例は、2番目のオーバーロードを強制的に解決する `z` の呼び出しを示しています。

 [!code-vb[VbVbcnProcedures#65](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#65)]

### <a name="overload-resolution-with-optional-and-paramarray-arguments"></a>省略可能な引数と ParamArray 引数を使用したオーバーロードの解決

 1つのプロシージャの2つのオーバーロードが同じシグネチャを持つ場合、最後のパラメーターは[省略可能](../../../language-reference/modifiers/optional.md)として宣言され、もう一方では[ParamArray](../../../language-reference/modifiers/paramarray.md)が適用されます。ただし、コンパイラは、最も近い一致に従って、そのプロシージャの呼び出しを解決します。 詳細については、「 [Overload Resolution](overload-resolution.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [手順](index.md)
- [Sub プロシージャ](sub-procedures.md)
- [Function プロシージャ](function-procedures.md)
- [Property プロシージャ](property-procedures.md)
- [演算子プロシージャ](operator-procedures.md)
- [プロシージャのパラメーターと引数](procedure-parameters-and-arguments.md)
- [プロシージャのオーバーロード](procedure-overloading.md)
- [プロシージャのオーバーロードに関する注意事項](considerations-in-overloading-procedures.md)
- [オーバーロードの解決](overload-resolution.md)
