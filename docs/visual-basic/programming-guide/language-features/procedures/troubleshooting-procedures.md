---
title: プロシージャのトラブルシューティング
ms.date: 07/20/2015
helpviewer_keywords:
- troubleshooting Visual Basic, procedures
- procedures [Visual Basic], troubleshooting
- Visual Basic code, procedures
- troubleshooting procedures
- procedures [Visual Basic], about procedures
ms.assetid: 525721e8-2e02-4f75-b5d8-6b893462cf2b
ms.openlocfilehash: 8d4c4929e299efb12d283492a101c18ae794110b
ms.sourcegitcommit: 17ee6605e01ef32506f8fdc686954244ba6911de
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74352515"
---
# <a name="troubleshooting-procedures-visual-basic"></a>プロシージャのトラブルシューティング (Visual Basic)

このページでは、プロシージャを使用しているときに発生する可能性のある一般的な問題について説明します。  
  
## <a name="returning-an-array-type-from-a-function-procedure"></a>関数プロシージャから配列の型を返す

`Function` プロシージャが配列のデータ型を返す場合、`Function` 名を使用して配列の要素に値を格納することはできません。 これを行おうとすると、コンパイラは `Function` の呼び出しと解釈します。 次の例ではコンパイラ エラーが生成されます。
  
```vb
Function AllOnes(n As Integer) As Integer()
   For i As Integer = 1 To n - 1  
      ' The following statement generates a COMPILER ERROR.  
      AllOnes(i) = 1  
   Next  

   ' The following statement generates a COMPILER ERROR.  
   Return AllOnes()  
End Function
```

`AllOnes(i) = 1` ステートメントは、間違ったデータ型の引数 (`Integer` 配列ではなく、スカラー `Integer`) で `AllOnes` を呼び出しているように見えるため、コンパイラ エラーが生成されます。 `Return AllOnes()` ステートメントは、引数なしで `AllOnes` を呼び出しているように見えるため、コンパイラ エラーが生成されます。  
  
 **正しい方法:** 返される配列の要素を変更できるようにするには、内部配列をローカル変数として定義します。 次の例はエラーなしでコンパイルされます。

 [!code-vb[VbVbcnProcedures#66](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#66)]

## <a name="argument-not-modified-by-procedure-call"></a>プロシージャ呼び出しによって引数が変更されない

プロシージャが、引数の基になる呼び出し元のコードのプログラミング要素を変更できるようにする場合は、参照渡しにする必要があります。 ただし、値渡しにした場合でも、プロシージャは参照型引数の要素にアクセスできます。

- **基になる変数**: プロシージャが、基になる変数要素自体の値を置き換えることができるようにするには、プロシージャでパラメーターを [ByRef](../../../language-reference/modifiers/byref.md) として宣言する必要があります。 また、呼び出し元のコードでは、引数をかっこで囲むことはできません。これを行うと、引渡し方法 `ByRef` がオーバーライドされるためです。

- **参照型の要素**: パラメーターを [ByVal](../../../language-reference/modifiers/byval.md) として宣言した場合、プロシージャは基になる変数要素自体を変更することはできません。 ただし、引数が参照型の場合、プロシージャは変数の値を置き換えることはできなくても、参照先のオブジェクトのメンバーを変更できます。 たとえば、引数が配列変数の場合、プロシージャは新しい配列を割り当てることはできませんが、1 つ以上の要素を変更できます。 変更された要素は、呼び出し元のコードの基になる配列変数に反映されます。

次の例では、配列変数を値で受け取り、その要素を操作する 2 つのプロシージャを定義します。 `increase` プロシージャは、各要素に 1 を加算するだけです。 `replace` プロシージャは、`a()` パラメーターに新しい配列を割り当ててから、各要素に 1 を加算します。 ただし、`a()` は `ByVal` として宣言されているため、再割り当ては呼び出し元のコードの基になる配列変数には影響しません。

[!code-vb[VbVbcnProcedures#35](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#35)]

[!code-vb[VbVbcnProcedures#38](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#38)]

次の例では、`increase` と `replace` を呼び出します。

[!code-vb[VbVbcnProcedures#37](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#37)]
  
最初の `MsgBox` 呼び出しでは、"After increase(n): 11, 21, 31, 41" と表示されます。 `n` は参照型であるため、`ByVal` で渡されても、`increase` はそのメンバーを変更できます。

2 番目の `MsgBox` 呼び出しでは、"After replace(n): 11, 21, 31, 41" と表示されます。 `n` は `ByVal` で渡されるため、`replace` は変数 `n` に新しい配列を割り当てて変更することはできません。 `replace` が新しい配列インスタンス `k` を作成し、ローカル変数 `a` に割り当てると、呼び出し元のコードによって渡された `n` への参照は失われます。 `a` のメンバーをインクリメントすると、ローカル配列 `k` だけが影響を受けます。

**正しい方法:** 基になる変数要素自体を変更できるようにするには、参照渡しにします。 次の例は、呼び出し元のコードの配列を別の配列に置き換えることができるようにするための、`replace` の宣言の変更を示しています。

[!code-vb[VbVbcnProcedures#64](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#64)]

## <a name="unable-to-define-an-overload"></a>オーバーロードを定義できない

プロシージャのオーバーロードされたバージョンを定義する場合は、同じ名前を使用し、異なるシグネチャを使用する必要があります。 コンパイラが、同じシグネチャを持つオーバーロードと宣言を区別できない場合、エラーが生成されます。

プロシージャの "*シグネチャ*" は、プロシージャ名とパラメーター リストによって決まります。 各オーバーロードの名前は、他のすべてのオーバーロードと同じである必要がありますが、シグネチャの他の構成要素の少なくとも 1 つですべてのオーバーロードを区別できる必要があります。 詳細については、「 [Procedure Overloading](./procedure-overloading.md)」を参照してください。

次の項目はパラメーター リストに関連するものですが、プロシージャのシグネチャの構成要素ではありません。

- プロシージャ修飾子キーワード (`Public`、`Shared`、`Static` など)
- パラメーター名
- パラメーター修飾子キーワード (`ByRef` や `Optional` など)
- 戻り値のデータ型 (変換演算子を除く)

上記の 1 つ以上の項目を変えるだけでは、プロシージャをオーバーロードすることはできません。

**正しい方法:** プロシージャのオーバーロードを定義できるようにするには、シグネチャを変える必要があります。 同じ名前を使用する必要があるため、パラメーターの数、順序、またはデータ型を変える必要があります。 ジェネリック プロシージャでは、型パラメーターの数を変えることができます。 変換演算子 ([CType 関数](../../../language-reference/functions/ctype-function.md)) では、戻り値の型を変えることができます。

### <a name="overload-resolution-with-optional-and-paramarray-arguments"></a>Optional および ParamArray 引数によるオーバーロードの解決

1 つ以上の [Optional](../../../language-reference/modifiers/optional.md) パラメーターまたは [ParamArray](../../../language-reference/modifiers/paramarray.md) パラメーターでプロシージャをオーバーロードする場合は、"*暗黙的なオーバーロード*" のいずれかと重複しないようにする必要があります。 詳細については、「[プロシージャのオーバーロードに関する注意事項](./considerations-in-overloading-procedures.md)」をご覧ください。

## <a name="calling-the-wrong-version-of-an-overloaded-procedure"></a>オーバーロードされたプロシージャの間違ったバージョンの呼び出し

プロシージャに複数のオーバーロードされたバージョンがある場合は、すべてのパラメーター リストを把握し、Visual Basic がオーバーロード間で呼び出しを解決する方法を理解しておく必要があります。 そうしないと、目的のもの以外のオーバーロードを呼び出す可能性があります。

呼び出すオーバーロードを決定したら、次の規則に従うよう注意してください。

- 正しい数の引数を正しい順序で指定します。  
- 引数は、対応するパラメーターとまったく同じデータ型であるのが理想的です。 いずれにしても、各引数のデータ型は、対応するパラメーターのデータ型に拡大変換する必要があります これは、[Option Strict ステートメント](../../../language-reference/statements/option-strict-statement.md)が `Off` に設定されている場合でも同様です。 オーバーロードが引数リストからの縮小変換を必要とする場合、そのオーバーロードは呼び出し対象にはなりません。
- 拡大変換を必要とする引数を指定する場合は、それらのデータ型を、対応するパラメーターのデータ型にできるだけ近いものにします。 2 つ以上のオーバーロードが引数のデータ型を受け入れる場合、コンパイラは、必要な拡大変換が最も少ないオーバーロードに呼び出しを解決します。

引数を準備するときに、[CType 関数](../../../language-reference/functions/ctype-function.md)変換キーワードを使用すると、データ型の不一致の可能性を低減できます。

### <a name="overload-resolution-failure"></a>オーバーロードの解決の失敗

オーバーロードされたプロシージャを呼び出すと、コンパイラはオーバーロードの 1 つを除くすべてを排除することを試みます。 これが成功すると、呼び出しがそのオーバーロードに解決されます。 すべてのオーバーロードが排除された場合や、対象となるオーバーロードを 1 つの候補に絞り込むことができない場合は、エラーが生成されます。

次の例は、オーバーロード解決プロセスを示しています。

[!code-vb[VbVbcnProcedures#62](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#62)]

[!code-vb[VbVbcnProcedures#63](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#63)]
  
最初の呼び出しでは、最初の引数の型 (`Short`) が対応するパラメーターの型 (`Byte`) に縮小変換されるため、コンパイラは最初のオーバーロードを排除します。 次に、2 番目のオーバーロードの各引数の型 (`Short` と `Single`) は、3 番目のオーバーロードの対応する型 (`Integer` と `Single`) に拡大変換されるため、3 番目のオーバーロードが排除されます。 2 番目のオーバーロードは必要な拡大変換が少ないため、コンパイラはこれを呼び出しに使用します。

2 番目の呼び出しでは、コンパイラは縮小変換に基づいてオーバーロードのいずれかを排除することができません。 最初の呼び出しと同じ理由で、3 番目のオーバーロードが排除されます。引数の型の拡大変換が少ない 2 番目のオーバーロードを呼び出すことができるためです。 ただし、コンパイラは最初と 2 番目のオーバーロード間で解決することはできません。 それぞれ、もう一方の対応する型に拡大変換されるパラメーターの型が定義されています (`Byte` から `Short`、`Single` から `Double`)。 そのため、コンパイラはオーバーロード解決エラーを生成します。

**正しい方法:** あいまいさを伴わずに、オーバーロードされたプロシージャを呼び出すことができるようにするには、[CType 関数](../../../language-reference/functions/ctype-function.md)を使用して、引数のデータ型をパラメーターの型と一致させます。 次の例は、2 番目のオーバーロードへの解決を強制する `z` の呼び出しを示しています。

[!code-vb[VbVbcnProcedures#65](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#65)]

### <a name="overload-resolution-with-optional-and-paramarray-arguments"></a>Optional および ParamArray 引数によるオーバーロードの解決

最後のパラメーターが一方では [Optional](../../../language-reference/modifiers/optional.md)、もう一方では [ParamArray](../../../language-reference/modifiers/paramarray.md) として宣言されている点を除き、プロシージャの 2 つのオーバーロードが同じシグネチャを持つ場合、コンパイラは最も一致するものに従って、そのプロシージャの呼び出しを解決します。 詳細については、「 [Overload Resolution](./overload-resolution.md)」を参照してください。

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
