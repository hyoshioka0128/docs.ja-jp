---
title: 条件判断構造
ms.date: 07/20/2015
helpviewer_keywords:
- statements [Visual Basic], control flow
- If statement [Visual Basic], decision structures
- If statement [Visual Basic], If...Then...Else
- control flow [Visual Basic], decision structures
- decision structures [Visual Basic]
- conditional statements [Visual Basic], decision structures
ms.assetid: 2e2e0895-4483-442a-b17c-26aead751ec2
ms.openlocfilehash: aac9844240defc5a21a3f4e6090fa8f49e6348a1
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84403519"
---
# <a name="decision-structures-visual-basic"></a>条件判断構造 (Visual Basic)
Visual Basic では、条件をテストし、そのテストの結果に応じてさまざまな操作を実行できます。 true または false の条件、式のさまざまな値、または一連のステートメントを実行するときに生成されるさまざまな例外に対して、テストを実行できます。  
  
 次の図は、条件が true であるかをテストし、true か false かに応じて異なるアクションを実行する決定構造を示しています。  
  
 ![If...Then...Else コンストラクションのフロー チャート。](./media/decision-structures/if-then-else-construction.gif)  
  
## <a name="ifthenelse-construction"></a>If...Then...Else コンストラクション  
 `If...Then...Else` コンストラクションを使用すると、1 つ以上の条件をテストし、各条件に応じて 1 つ以上のステートメントを実行できます。 次の方法で、条件をテストし、アクションを実行できます。  
  
- 条件が `True` の場合、1 つ以上のステートメントを実行する  
  
- 条件が `False` の場合、1 つ以上のステートメントを実行する  
  
- 条件が `True` 場合は、ステートメントをいくつか実行し、`False` の場合は、別のステートメントをいくつか実行する  
  
- 前の条件が `False` の場合、追加の条件をテストする  
  
 これらのすべての可能性を提供する制御構造が [If...Then...Else ステートメント](../../../language-reference/statements/if-then-else-statement.md)です。 実行するテストとステートメントがそれぞれ 1 つしかない場合は、単一行バージョンを使用できます。 より複雑な条件とアクションのセットがある場合は、複数行バージョンを使用できます。  
  
## <a name="selectcase-construction"></a>Select...Case コンストラクション  
 `Select...Case` コンストラクションを使用すると、式を 1 回評価し、使用できるさまざまな値に基づいてさまざまなステートメント セットを実行できます。 詳細については、「[Select...Case ステートメント](../../../language-reference/statements/select-case-statement.md)」を参照してください。  
  
## <a name="trycatchfinally-construction"></a>Try...Catch...Finally コンストラクション  
 `Try...Catch...Finally` コンストラクションを使用すると、使っているステートメントのいずれかによって例外が引き起こされた場合に、コントロールが保持されている環境で一連のステートメントを実行できます。 さまざまな例外に対して、さまざまなアクションを実行できます。 発生する事象を問わず、`Try...Catch...Finally` コンストラクション全体を終了する前に実行されるコード ブロックを、必要に応じて指定できます。 詳しくは、「[Try...Catch...Finally ステートメント](../../../language-reference/statements/try-catch-finally-statement.md)」をご覧ください。  
  
> [!NOTE]
> 多くの制御構造で、キーワードの 1 つをクリックすると、構造内のすべてのキーワードが強調表示されます。 たとえば、`If...Then...Else` コンストラクションで `If` をクリックすると、コンストラクション内の `If`、`Then`、`ElseIf`、`Else`、および `End If` のすべてのインスタンスが強調表示されます。 次または前の強調表示されたキーワードに移動するには、Ctrl + Shift + ↓キーを押すか、Ctrl + Shift + ↑キーを押します。  
  
## <a name="see-also"></a>関連項目

- [制御フロー](index.md)
- [ループ構造](loop-structures.md)
- [その他の制御構造](other-control-structures.md)
- [入れ子になった制御構造](nested-control-structures.md)
- [If 演算子](../../../language-reference/operators/if-operator.md)
