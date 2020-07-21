---
title: '方法: プロシージャを別のプロシージャに渡す'
ms.date: 07/20/2015
helpviewer_keywords:
- AddressOf operator [Visual Basic]
- delegates [Visual Basic], passing procedures
ms.assetid: 5adbba15-5a1d-413f-ab3e-3ff6cc0a4669
ms.openlocfilehash: 36f623068372614ae034a8a7b31bffb7496f98b1
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84410696"
---
# <a name="how-to-pass-procedures-to-another-procedure-in-visual-basic"></a>方法: Visual Basic でプロシージャを別のプロシージャに渡す
この例では、デリゲートを使用してプロシージャを別のプロシージャに渡す方法を示します。  
  
 デリゲートは、Visual Basic で他の型と同じように使用できる型です。 `AddressOf` 演算子は、プロシージャ名に適用されるときにデリゲート オブジェクトを返します。  
  
 この例は、プロシージャと、`AddressOf` 演算子で取得した別のプロシージャへの参照を取ることができるデリゲート パラメーターを示しています。  
  
### <a name="create-the-delegate-and-matching-procedures"></a>デリゲートおよび一致するプロシージャを作成する  
  
1. `MathOperator` という名前のデリゲートを作成します。  
  
     [!code-vb[VbVbalrDelegates#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrDelegates/VB/Class1.vb#1)]  
  
2. `MathOperator` のパラメーターと一致するパラメーターと戻り値を持つ、`AddNumbers` という名前のプロシージャを作成します。これによりシグネチャが一致します。  
  
     [!code-vb[VbVbalrDelegates#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrDelegates/VB/Class1.vb#2)]  
  
3. `MathOperator` と一致するシグネチャを持つ `SubtractNumbers` という名前のプロシージャを作成します。  
  
     [!code-vb[VbVbalrDelegates#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrDelegates/VB/Class1.vb#3)]  
  
4. デリゲートをパラメーターとして取る `DelegateTest` という名前のプロシージャを作成します。  
  
     このプロシージャは `AddNumbers` または `SubtractNumbers` への参照を受け入れることができます。なぜなら、そのシグネチャが `MathOperator` シグネチャと一致するためです。  
  
     [!code-vb[VbVbalrDelegates#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrDelegates/VB/Class1.vb#4)]  
  
5. `Test` という名前のプロシージャを作成します。このプロシージャは、`DelegateTest` を、`AddNumbers` のデリゲートでパラメーターとして 1 回呼び出し、`SubtractNumbers` のデリゲートでパラメーターとしてもう 1 回呼び出します。  
  
     [!code-vb[VbVbalrDelegates#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrDelegates/VB/Class1.vb#5)]  
  
     `Test` が呼び出されると、最初は `5` および `3` で動作している `AddNumbers` の結果である 8 が表示されます。 次に、`9` と `3` で動作している `SubtractNumbers` の結果である 6 が表示されます。  
  
## <a name="see-also"></a>関連項目

- [デリゲート](index.md)
- [AddressOf 演算子](../../../language-reference/operators/addressof-operator.md)
- [Delegate ステートメント](../../../language-reference/statements/delegate-statement.md)
- [方法: デリゲート メソッドを呼び出す](how-to-invoke-a-delegate-method.md)
