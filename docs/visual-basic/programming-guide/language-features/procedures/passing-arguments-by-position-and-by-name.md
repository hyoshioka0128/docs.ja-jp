---
title: 位置と名前による引数渡し
ms.date: 02/01/2018
helpviewer_keywords:
- arguments [Visual Basic], passing by name
- procedures [Visual Basic], arguments
- := passing arguments
- procedure arguments
- Visual Basic code, procedures
- named arguments [Visual Basic], passing arguments
- arguments [Visual Basic], passing by position
- Function procedures [Visual Basic], passing arguments
- named parameters [Visual Basic], passing arguments
- named arguments
- passing parameters [Visual Basic], named parameter arguments
- passing parameters [Visual Basic], by position
- procedures [Visual Basic], calling
- named parameters
- Sub procedures [Visual Basic], passing arguments
- argument passing
- passing parameters [Visual Basic], by name
- argument passing [Visual Basic], by position
- arguments [Visual Basic], listing by name
ms.assetid: 1ad7358f-1da9-48da-a95b-f3c7ed41eff3
ms.openlocfilehash: 686b64977f086c8128e56298a0ed8c5aa0c51efa
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84364033"
---
# <a name="passing-arguments-by-position-and-by-name-visual-basic"></a>位置と名前による引数渡し (Visual Basic)

`Sub` または `Function` プロシージャを呼び出すときに、引数を "*位置*" (プロシージャの定義に表示されている順序) で渡すことができます。また、位置に関係なく、"*名前*" で渡すこともできます。

引数を名前で渡す場合は、引数の宣言名の後にコロンと等号 (`:=`) を入力し、その後に引数の値を指定します。 名前付き引数は任意の順序で指定できます。

たとえば、次の `Sub` プロシージャは 3 つの引数を受け取ります。

[!code-vb[SampleProcedure](../../../../../samples/snippets/visualbasic/programming-guide/language-features/passing-named-arguments/module1.vb#1)]

このプロシージャを呼び出すときに、位置、名前、またはこの両方の組み合わせを使用して引数を指定できます。

## <a name="passing-arguments-by-position"></a>引数を位置で渡す

次の例に示すように、位置で渡す引数をコンマで区切って指定して、`Display` メソッドを呼び出すことができます。

[!code-vb[ByPosition](../../../../../samples/snippets/visualbasic/programming-guide/language-features/passing-named-arguments/module1.vb#2)]

位置引数リストで省略可能な引数を省略する場合は、コンマを使用してその場所を保持する必要があります。 次の例では、`age` 引数を指定せずに `Display` メソッドを呼び出します。

[!code-vb[ByPositionWithOptionalArgument](../../../../../samples/snippets/visualbasic/programming-guide/language-features/passing-named-arguments/module1.vb#3)]

## <a name="passing-arguments-by-name"></a>引数を名前で渡す

次の例に示すように、名前で渡す引数をコンマで区切って指定して、`Display` メソッドを呼び出すこともできます。

[!code-vb[ByName](../../../../../samples/snippets/visualbasic/programming-guide/language-features/passing-named-arguments/module1.vb#4)]

このような名前による引数渡しは、省略可能な引数が複数あるプロシージャを呼び出すときに特に役立ちます。 引数を名前で指定する場合、連続するコンマを使用して欠けている位置引数を示す必要はありません。 また、引数を名前で渡すと、渡す引数と省略する引数を追跡しやすくなります。

## <a name="mixing-arguments-by-position-and-by-name"></a>位置と名前の組み合わせで引数を渡す

次の例に示すように、1 つのプロシージャ呼び出しで、位置と名前の両方で引数を指定できます。

[!code-vb[ByNameAndPosition](../../../../../samples/snippets/visualbasic/programming-guide/language-features/passing-named-arguments/module1.vb#5)]

前の例では、`birth` が名前で渡されているため、省略された `age` 引数の場所を保持するためにコンマを追加する必要はありません。

Visual Basic 15.5 より前のバージョンでは、位置と名前の組み合わせで引数を指定するときに、位置引数を常に最初に指定する必要があります。 引数を名前で指定したら、残りの引数はすべて名前で渡す必要があります。  たとえば、次の `Display` メソッドの呼び出しでは、"[BC30241: Named argument expected\(名前付き引数が必要です\)](../../../misc/bc30241.md)" というコンパイラ エラーが表示されます。

[!code-vb[ByNameAndPosition](../../../../../samples/snippets/visualbasic/programming-guide/language-features/passing-named-arguments/module1.vb#6)]

Visual Basic 15.5 以降では、末尾の位置引数が正しい位置にあれば、位置引数を名前付き引数の後に指定できます。 Visual Basic 15.5 でコンパイルすると、前の `Display` メソッドの呼び出しは正常にコンパイルされ、コンパイラ エラー [BC30241](../../../misc/bc30241.md) は生成されなくなりました。

名前付き引数と位置引数を任意の順序で組み合わせるこの機能は、名前付き引数を使用してコードを読みやすくする場合に特に役立ちます。 たとえば、次の `Person` クラスのコンストラクターには、`Person` 型の 2 つの引数が必要であり、どちらも `Nothing` にすることができます。

[!code-vb[ByNameAndPosition](../../../../../samples/snippets/visualbasic/programming-guide/language-features/passing-named-arguments/module1.vb#7)]

名前付き引数と位置引数の組み合わせを使用すると、`father` および `mother` 引数の値が `Nothing` の場合に、コードの意図を明確にすることができます。

[!code-vb[ByNameAndPosition](../../../../../samples/snippets/visualbasic/programming-guide/language-features/passing-named-arguments/module1.vb#8)]

位置引数の後に名前付き引数を指定するには、Visual Basic プロジェクト (\*.vbproj) ファイルに次の要素を追加する必要があります。

```xml
<PropertyGroup>
  <LangVersion>15.5</LangVersion>
</PropertyGroup>
```

詳細については、[Visual Basic 言語バージョンの設定](../../../language-reference/configure-language-version.md)に関するページを参照してください。

## <a name="restrictions-on-supplying-arguments-by-name"></a>引数を名前で指定する場合の制限事項

必須の引数の入力を避けるために、引数を名前で渡すことはできません。 省略できるのは、省略可能な引数だけです。

パラメーター配列を名前で渡すことはできません。 これは、プロシージャを呼び出すときに、パラメーター配列に対して不特定数のコンマ区切りの引数を指定しますが、コンパイラは複数の引数を 1 つの名前に関連付けることができないためです。

## <a name="see-also"></a>関連項目

- [手順](./index.md)
- [プロシージャのパラメーターと引数](./procedure-parameters-and-arguments.md)
- [方法: プロシージャに引数を渡す](./how-to-pass-arguments-to-a-procedure.md)
- [引数の値渡しと参照渡し](./passing-arguments-by-value-and-by-reference.md)
- [省略可能なパラメーター](./optional-parameters.md)
- [パラメーター配列](./parameter-arrays.md)
- [Optional](../../../language-reference/modifiers/optional.md)
- [ParamArray](../../../language-reference/modifiers/paramarray.md)
