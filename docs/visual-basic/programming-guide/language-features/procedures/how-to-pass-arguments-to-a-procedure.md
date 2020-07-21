---
title: '方法: プロシージャに引数を渡す'
ms.date: 07/20/2015
helpviewer_keywords:
- arguments [Visual Basic], passing to procedures
- procedures [Visual Basic], arguments
- procedures [Visual Basic], parameters
- procedure arguments
- Visual Basic code, procedures
- procedure parameters
- procedures [Visual Basic], calling
- argument passing [Visual Basic], procedures
ms.assetid: 08723588-3890-4ddc-8249-79e049e0f241
ms.openlocfilehash: 903e05facccd1f2afdf4bb51b200531feb64aa79
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84387778"
---
# <a name="how-to-pass-arguments-to-a-procedure-visual-basic"></a>方法: プロシージャに引数を渡す (Visual Basic)
プロシージャを呼び出すときは、プロシージャ名の後に、かっこで囲んだ引数リストを追加します。 プロシージャで定義されているすべての必須パラメーターに対応する引数を指定します。また、必要に応じて `Optional` パラメーターに引数を指定することもできます。 呼び出しに `Optional` パラメーターを指定しない場合に、後続の引数を指定するのであれば、引数リスト内にコンマを含めてその位置をマークする必要があります。  
  
 対応するパラメーターとは異なるデータ型の引数 (`Byte` など) を `String` に渡す場合は、型チェック スイッチ ([Option Strict ステートメント](../../../language-reference/statements/option-strict-statement.md)) を `Off` に設定できます。 `Option Strict` が `On` の場合は、拡大変換または明示的な変換キーワードのいずれかを使用する必要があります。 詳細については、「[拡大変換と縮小変換](../data-types/widening-and-narrowing-conversions.md)」および「[データ型変換関数](../../../language-reference/functions/type-conversion-functions.md)」を参照してください。  
  
 詳細については、「[プロシージャのパラメーターと引数](./procedure-parameters-and-arguments.md)」を参照してください。  
  
### <a name="to-pass-one-or-more-arguments-to-a-procedure"></a>プロシージャに 1 つ以上の引数を渡すには  
  
1. 呼び出し元のステートメントで、プロシージャ名の後にかっこを付けます。  
  
2. かっこ内に引数リストを入力します。 プロシージャによって定義される必須パラメーターごとに引数を含め、引数をコンマで区切ります。  
  
3. 各引数が、対応するパラメーターに対してプロシージャによって定義される型に変換できるデータ型に評価される、有効な式であることを確認します。  
  
4. パラメーターが[省略可能](../../../language-reference/modifiers/optional.md)として定義されている場合は、引数リストに追加するか、または省略することができます。 省略した場合、プロシージャでは、そのパラメーターに対して定義された既定値が使用されます。  
  
5. `Optional` パラメーターの引数を省略していて、パラメーター リスト内に後続の別のパラメーターがある場合は、引数リスト内の省略された引数の位置を追加のコンマでマークします。  
  
     次の例では、Visual Basic <xref:Microsoft.VisualBasic.Interaction.MsgBox%2A> 関数を呼び出します。  
  
     [!code-vb[VbVbcnProcedures#34](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#34)]  
  
     前の例では、必要な最初の引数が指定されています。これは、表示されるメッセージ文字列です。 メッセージ ボックスに表示するボタンを指定する、省略可能な 2 番目のパラメーターの引数は省略されています。 呼び出しで値が指定されていないため、`MsgBox` では既定値の `MsgBoxStyle.OKOnly` が使用されます。これにより、 **[OK]** ボタンのみが表示されます。  
  
     引数リスト内の 2 番目のコンマは、省略された 2 番目の引数の位置をマークするもので、最後の文字列は、省略可能な 3 番目のパラメーター `MsgBox` (タイトル バーに表示されるテキスト) に渡されます。  
  
## <a name="see-also"></a>関連項目

- [Sub プロシージャ](./sub-procedures.md)
- [Function プロシージャ](./function-procedures.md)
- [Property プロシージャ](./property-procedures.md)
- [演算子プロシージャ](./operator-procedures.md)
- [方法: プロシージャのパラメーターを定義する](./how-to-define-a-parameter-for-a-procedure.md)
- [引数の値渡しと参照渡し](./passing-arguments-by-value-and-by-reference.md)
- [再帰プロシージャ](./recursive-procedures.md)
- [プロシージャのオーバーロード](./procedure-overloading.md)
- [クラスとオブジェクト](../objects-and-classes/index.md)
- [オブジェクト指向プログラミング (Visual Basic)](../../concepts/object-oriented-programming.md)
