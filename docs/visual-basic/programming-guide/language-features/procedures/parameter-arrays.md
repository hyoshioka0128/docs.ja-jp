---
title: パラメーター配列
ms.date: 07/20/2015
helpviewer_keywords:
- parameter arrays [Visual Basic], about parameter arrays
- ParamArray keyword [Visual Basic], parameter arrays
- Visual Basic code, procedures
- parameters [Visual Basic], parameter arrays
- arguments [Visual Basic], parameter arrays
- procedures [Visual Basic], indefinite number of argument values
- arrays [Visual Basic], parameter arrays
ms.assetid: c43edfae-9114-4096-9ebc-8c5c957a1067
ms.openlocfilehash: dac0575d73ffd4159e89bff344915a33b9d0e5d3
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84364280"
---
# <a name="parameter-arrays-visual-basic"></a>パラメーター配列 (Visual Basic)
通常、プロシージャ宣言で指定されている引数よりも多くの引数でプロシージャを呼び出すことはできません。 不特定数の引数が必要な場合は、"*パラメーター配列*" を宣言できます。これにより、プロシージャはパラメーターの値の配列を受け入れることができます。 プロシージャを定義するときに、パラメーター配列の要素の数がわかっている必要はありません。 配列のサイズは、プロシージャの呼び出しごとに個別に決定されます。  
  
## <a name="declaring-a-paramarray"></a>ParamArray の宣言  
 [ParamArray](../../../language-reference/modifiers/paramarray.md) キーワードを使用して、パラメーター リスト内のパラメーター配列を示します。 次の規則が適用されます。  
  
- プロシージャではパラメーター配列を 1 つだけ定義でき、プロシージャ定義の最後のパラメーターである必要があります。  
  
- パラメーター配列は値渡しにする必要があります。 プロシージャの定義に [ByVal](../../../language-reference/modifiers/byval.md) キーワードを明示的に含めることをお勧めします。  
  
- パラメーター配列は自動的に省略可能になります。 既定値は、パラメーター配列の要素型の空の 1 次元配列です。  
  
- パラメーター配列の前にあるすべてのパラメーターが必須である必要があります。 パラメーター配列が唯一の省略可能なパラメーターでなければなりません。  
  
## <a name="calling-a-paramarray"></a>ParamArray の呼び出し  
 パラメーター配列が定義されているプロシージャを呼び出すときは、次のいずれかの方法で引数を指定できます。  
  
- Nothing - つまり、[ParamArray](../../../language-reference/modifiers/paramarray.md) 引数を省略できます。 この場合、プロシージャに空の配列が渡されます。 [Nothing](../../../language-reference/nothing.md) キーワードを明示的に渡すと、プロシージャに null 配列が渡されます。呼び出されたプロシージャがこの条件をチェックしない場合、NullReferenceException が発生する可能性があります。
  
- コンマで区切られた任意の数の引数のリスト。 各引数のデータ型は、`ParamArray` 要素型に暗黙的に変換できる必要があります。  
  
- パラメーター配列の要素型と同じ要素型の配列。  
  
 どの場合も、プロシージャ内のコードは、パラメーター配列を、`ParamArray` のデータ型と同じデータ型の要素を含む 1 次元配列として扱います。  
  
> [!IMPORTANT]
> 無限に大きくなる可能性がある配列を処理する場合は常に、アプリケーションの何らかの内部容量が超過するリスクがあります。 パラメーター配列を受け入れる場合は、呼び出し元のコードから渡された配列のサイズをテストする必要があります。 アプリケーションにとって大きすぎる場合は、適切な手順を実行してください。 詳細については、「[配列](../arrays/index.md)」を参照してください。  
  
## <a name="example"></a>例  
 次の例では、`calcSum` 関数を定義して呼び出します。 `args` パラメーターの `ParamArray` 修飾子により、関数は可変数の引数を受け入れることができます。  
  
 [!code-vb[VbVbalrStatements#26](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#26)]  
  
 次の例では、パラメーター配列を使用するプロシージャを定義し、パラメーター配列に渡されたすべての配列要素の値を出力します。  
  
 [!code-vb[VbVbcnProcedures#48](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#48)]  
  
 [!code-vb[VbVbcnProcedures#49](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#49)]  
  
## <a name="see-also"></a>関連項目

- <xref:Microsoft.VisualBasic.Information.UBound%2A>
- [手順](./index.md)
- [プロシージャのパラメーターと引数](./procedure-parameters-and-arguments.md)
- [引数の値渡しと参照渡し](./passing-arguments-by-value-and-by-reference.md)
- [位置と名前による引数渡し](./passing-arguments-by-position-and-by-name.md)
- [省略可能なパラメーター](./optional-parameters.md)
- [プロシージャのオーバーロード](./procedure-overloading.md)
- [配列](../arrays/index.md)
- [Optional](../../../language-reference/modifiers/optional.md)
