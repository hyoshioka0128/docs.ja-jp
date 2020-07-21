---
title: 厳密でないデリゲート変換
ms.date: 07/20/2015
helpviewer_keywords:
- relaxed delegate conversion [Visual Basic]
- delegates [Visual Basic], relaxed conversion
- conversions [Visual Basic], relaxed delegate
ms.assetid: 64f371d0-5416-4f65-b23b-adcbf556e81c
ms.openlocfilehash: a581ffae77c496908d2e4e38df53491a54ae2ab8
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84410671"
---
# <a name="relaxed-delegate-conversion-visual-basic"></a>厳密でないデリゲート変換 (Visual Basic)
厳密でないデリゲート変換を使用すると、シグネチャが同じでない場合でも、Sub プロシージャや関数をデリゲートまたはハンドラーに割り当てることができます。 したがって、デリゲートへのバインドは、メソッドの呼び出しに対して既に許可されているバインドと整合します。  
  
## <a name="parameters-and-return-type"></a>パラメーターと戻り値の型  
 厳密なシグネチャ一致の代わりに、厳密でない変換では、`Option Strict` が `On` に設定されている場合は次の条件を満たす必要があります。  
  
- 各デリゲート パラメーターのデータ型から、割り当てられた関数または `Sub` の対応するパラメーターのデータ型に、拡大変換が存在する必要があります。 次の例では、デリゲート `Del1` に 1 つのパラメーター `Integer` があります。 割り当てられたラムダ式のパラメーター `m` には、`Integer` からの拡大変換に対するデータ型、`Long` や `Double` などが含まれている必要があります。  
  
     [!code-vb[VbVbalrRelaxedDelegates#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrRelaxedDelegates/VB/Module1.vb#1)]  
  
     [!code-vb[VbVbalrRelaxedDelegates#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrRelaxedDelegates/VB/Module1.vb#2)]  
  
     縮小変換が許可されるのは、`Option Strict` が `Off` に設定されている場合のみです。  
  
     [!code-vb[VbVbalrRelaxedDelegates#8](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrRelaxedDelegates/VB/Module2.vb#8)]  
  
- 割り当てられた関数または `Sub` の戻り値の型から、デリゲートの戻り値の型への逆方向に、拡大変換が存在する必要があります。 次の例では、`del1` の戻り値の型が `Integer` であるため、割り当てられている各ラムダ式の本体は、`Integer` に拡大変換されるデータ型に評価される必要があります。  
  
     [!code-vb[VbVbalrRelaxedDelegates#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrRelaxedDelegates/VB/Module1.vb#3)]  
  
 `Option Strict` が `Off` に設定されている場合、拡大制限は両方向で削除されます。  
  
 [!code-vb[VbVbalrRelaxedDelegates#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrRelaxedDelegates/VB/Module2.vb#4)]  
  
## <a name="omitting-parameter-specifications"></a>パラメーターの指定値の省略  
 厳密でないデリゲートを使用すると、割り当てられたメソッドで、パラメーターの指定値を完全に省略することもできます。  
  
 [!code-vb[VbVbalrRelaxedDelegates#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrRelaxedDelegates/VB/Module1.vb#5)]  
  
 [!code-vb[VbVbalrRelaxedDelegates#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrRelaxedDelegates/VB/Module1.vb#6)]  
  
 一部のパラメーターを指定する一方で他のパラメーターを省略することはできません。  
  
 [!code-vb[VbVbalrRelaxedDelegates#15](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrRelaxedDelegates/VB/Module1.vb#15)]  
  
 パラメーターを省略する機能は、イベント ハンドラーを定義する状況などで役立ちます。このような場合、複雑なパラメーターが複数関係しています。 一部のイベント ハンドラーについては、そのハンドラーに対する引数が使用されません。 ハンドラーは、イベントが登録されているコントロールの状態に直接アクセスし、引数を無視します。 厳密でないデリゲートを使用すると、あいまいな結果がないときに、このような宣言の引数を省略できます。 次の例では、完全に指定されたメソッド `OnClick` を `RelaxedOnClick` として書き直すことができます。  
  
```vb  
Sub OnClick(ByVal sender As Object, ByVal e As EventArgs) Handles b.Click  
    MessageBox.Show("Hello World from" + b.Text)  
End Sub  
  
Sub RelaxedOnClick() Handles b.Click  
    MessageBox.Show("Hello World from" + b.Text)  
End Sub  
```  
  
## <a name="addressof-examples"></a>AddressOf の例  
 前の例では、ラムダ式を使用して、型の関係を簡単に確認できます。 ただし、`AddressOf`、`Handles`、または `AddHandler` が使用されているデリゲート割り当てに対して、同じ緩和が許可されています。  
  
 次の例では、関数 `f1`、`f2`、`f3`、`f4` のすべてを `Del1` に割り当てることができます。  
  
 [!code-vb[VbVbalrRelaxedDelegates#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrRelaxedDelegates/VB/Module1.vb#1)]  
  
 [!code-vb[VbVbalrRelaxedDelegates#7](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrRelaxedDelegates/VB/Module1.vb#7)]  
  
 [!code-vb[VbVbalrRelaxedDelegates#9](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrRelaxedDelegates/VB/Module1.vb#9)]  
  
 次の例は、`Option Strict` が `Off` に設定されている場合にのみ有効です。  
  
 [!code-vb[VbVbalrRelaxedDelegates#14](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrRelaxedDelegates/VB/Module2.vb#14)]  
  
## <a name="dropping-function-returns"></a>関数の戻り値の破棄  
 厳密でないデリゲート変換を使用すると、関数を `Sub` デリゲートに割り当てて、関数の戻り値を効果的に無視できます。 ただし、`Sub` を関数デリゲートに割り当てることはできません。 次の例では、関数 `doubler` のアドレスが `Sub` デリゲート `Del3` に割り当てられています。  
  
 [!code-vb[VbVbalrRelaxedDelegates#10](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrRelaxedDelegates/VB/Module1.vb#10)]  
  
 [!code-vb[VbVbalrRelaxedDelegates#11](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrRelaxedDelegates/VB/Module1.vb#11)]  
  
## <a name="see-also"></a>関連項目

- [ラムダ式](../procedures/lambda-expressions.md)
- [拡大変換と縮小変換](../data-types/widening-and-narrowing-conversions.md)
- [デリゲート](index.md)
- [方法: Visual Basic でプロシージャを別のプロシージャに渡す](how-to-pass-procedures-to-another-procedure.md)
- [ローカル型の推論](../variables/local-type-inference.md)
- [Option Strict ステートメント](../../../language-reference/statements/option-strict-statement.md)
