---
title: GoTo ステートメント
ms.date: 07/20/2015
f1_keywords:
- vb.GoTo
helpviewer_keywords:
- GoTo statement [Visual Basic]
- control flow [Visual Basic], branching
- unconditional branching [Visual Basic]
- branching [Visual Basic]
- branching [Visual Basic], unconditional
- branching [Visual Basic], conditional
- conditional statements [Visual Basic], GoTo statement
- GoTo statement [Visual Basic], syntax
ms.assetid: 313274c2-8ab3-4b9c-9ba3-0fd6798e4f6d
ms.openlocfilehash: eb6f48d04b7d14591003e340464451da7df45cd6
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84404616"
---
# <a name="goto-statement"></a>GoTo ステートメント
プロシージャ内の指定した行に無条件に分岐します。  
  
## <a name="syntax"></a>構文  
  
```vb  
GoTo line  
```  
  
## <a name="part"></a>パーツ  
 `line`  
 必須です。 任意の行ラベル。  
  
## <a name="remarks"></a>Remarks  
 `GoTo` ステートメントでは、それが存在するプロシージャ内の行にのみ分岐できます。 行には、`GoTo` で参照できる行ラベルが必要です。 詳細については、「[方法:ステートメントへのラベル付け](../../programming-guide/program-structure/how-to-label-statements.md)」を参照してください。  
  
> [!NOTE]
> `GoTo` ステートメントによって、コードの読み取りと保守が困難になる場合があります。 可能な限り、代わりに制御構造を使用してください。 詳細については、「 [Control Flow](../../programming-guide/language-features/control-flow/index.md)」を参照してください。  
  
 `GoTo` ステートメントを使用して、`For`...`Next`、`For Each`...`Next`、`SyncLock`...`End SyncLock`、`Try`...`Catch`...`Finally`、`With`...`End With`、または `Using`...`End Using` コンストラクションの外部から、内部のラベルに分岐することはできません。  
  
## <a name="branching-and-try-constructions"></a>分岐と Try コンストラクション  
 `Try`...`Catch``Finally` コンストラクション内では、`GoTo` ステートメントによる分岐に、次のルールが適用されます。  
  
|ブロックまたは領域|外部からの分岐|内部からの分岐|  
|---------------------|-------------------------------|-------------------------------|  
|`Try` ブロック|同じコンストラクションの `Catch` ブロックからのみ <sup>1</sup>|コンストラクション全体の外部へのみ|  
|`Catch` ブロック|許可されない|コンストラクション全体の外部、または同じコンストラクションの `Try` ブロックへのみ <sup>1</sup>|  
|`Finally` ブロック|許可されない|許可されない|  
  
 <sup>1</sup> 1 つの `Try`...`Catch`...`Finally` コンストラクションが別のコンストラクション内に入れ子になっている場合、`Catch` ブロックは自身の入れ子レベルにある `Try` ブロックに分岐できますが、他の `Try` ブロックには分岐できません。 入れ子になった `Try`...`Catch`...`Finally` コンストラクションは、それが中で入れ子になっているコンストラクションの `Try` または `Catch` ブロックに完全に含まれている必要があります。  
  
 次の図は、別のコンストラクション内に入れ子になっている `Try` コンストラクションを示しています。 2 つのコンストラクションのブロック間のさまざまな分岐は、有効または無効として示されます。  
  
 ![Try 構造内の分岐のグラフィック ダイアグラム](./media/goto-statement/try-construction-branching.gif)  
  
## <a name="example"></a>例  
 次の例では、`GoTo` ステートメントを使用して、プロシージャ内の行ラベルに分岐します。  
  
 [!code-vb[VbVbalrStatements#31](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#31)]  
  
## <a name="see-also"></a>関連項目

- [Do...Loop ステートメント](do-loop-statement.md)
- [For...Next ステートメント](for-next-statement.md)
- [For Each...Next ステートメント](for-each-next-statement.md)
- [If...Then...Else ステートメント](if-then-else-statement.md)
- [Select...Case ステートメント](select-case-statement.md)
- [Try...Catch...Finally ステートメント](try-catch-finally-statement.md)
- [While...End While ステートメント](while-end-while-statement.md)
- [With...End With ステートメント](with-end-with-statement.md)
