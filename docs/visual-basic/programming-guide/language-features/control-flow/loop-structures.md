---
title: ループ構造
ms.date: 07/20/2015
helpviewer_keywords:
- control flow [Visual Basic], loops
- For keyword [Visual Basic], loop structures
- loops
- loop structures [Visual Basic]
- statements [Visual Basic], loop
- Do statement [Visual Basic], Do loops
- conditional statements [Visual Basic], loop structures
ms.assetid: ecacb09b-a4c9-42be-98b2-a15d368b5db8
ms.openlocfilehash: 3f60e9dc83dc7174e765903be13f2870ea40ce4c
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84403520"
---
# <a name="loop-structures-visual-basic"></a>ループ構造 (Visual Basic)
Visual Basic ループ構造を使用すると、1 行または複数行のコードを繰り返し実行できます。 ループ構造では、条件が `True` または `False` になるまで、指定された回数だけ、またはコレクション内の要素ごとに 1 回、ステートメントを繰り返すことができます。  
  
 次の図は、条件が true になるまで、一連のステートメントを実行するループ構造を示しています。  
  
 ![Do...Until ループを示すフロー チャート。](./media/loop-structures/do-until-loop-true-condition.gif)  
  
## <a name="while-loops"></a>While ループ  
 `While`...`End While` コンストラクションでは、`While` ステートメントで指定された条件が `True` である限り、一連のステートメントが実行されます。 詳細については、「[While...End While ステートメント](../../../language-reference/statements/while-end-while-statement.md)」を参照してください。  
  
## <a name="do-loops"></a>Do ループ  
 `Do`...`Loop` コンストラクションを使用すると、ループ構造の最初または最後で条件をテストできます。 また、条件が `True` の間、または `True` になるまで、ループを繰り返すかどうかを指定することもできます。 詳細については、「[Do...Loop ステートメント](../../../language-reference/statements/do-loop-statement.md)」を参照してください。  
  
## <a name="for-loops"></a>For ループ  
 `For`...`Next` コンストラクションでは、設定された回数だけループが実行されます。 繰り返しの追跡には、"*カウンター*" とも呼ばれるループ制御変数が使用されます。 このカウンターの開始値と終了値を指定し、必要に応じて、ある繰り返しから次の繰り返しまでの増加量を指定できます。 詳細については、「[For...Next ステートメント](../../../language-reference/statements/for-next-statement.md)」を参照してください。  
  
## <a name="for-each-loops"></a>For Each ループ  
 `For Each`...`Next` コンストラクションでは、コレクション内の要素ごとに 1 回、一連のステートメントが実行されます。 ループ制御変数を指定しますが、その開始値と終了値を決める必要はありません。 詳細については、[For Each...Next ステートメント](../../../language-reference/statements/for-each-next-statement.md) を参照してください。  
  
## <a name="see-also"></a>関連項目

- [制御フロー](index.md)
- [条件判断構造](decision-structures.md)
- [その他の制御構造](other-control-structures.md)
- [入れ子になった制御構造](nested-control-structures.md)
