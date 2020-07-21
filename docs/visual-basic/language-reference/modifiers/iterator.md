---
title: Iterator
ms.date: 07/20/2015
f1_keywords:
- vb.Iterator
helpviewer_keywords:
- Iterator keyword [Visual Basic]
ms.assetid: 69cb0b04-ac87-49d0-bcfe-810c0d60daff
ms.openlocfilehash: bb19289c69f4c523363e88e91a58f37d232b07df
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84396234"
---
# <a name="iterator-visual-basic"></a>反復子 (Visual Basic)
関数または `Get` アクセサーが反復子であることを示します。  
  
## <a name="remarks"></a>Remarks  
 *反復子*は、コレクションに対するカスタム イテレーションを実行します。 反復子は、[Yield](../statements/yield-statement.md) ステートメントを使用して、コレクションの各要素を 1 回に 1 つ返します。 `Yield` ステートメントに達すると、コードの現在の場所が保持されます。 次回、Iterator 関数が呼び出されると、この位置から実行が再開されます。  
  
 反復子は、関数として実装することも、プロパティ定義の `Get` アクセサーとして実装することもできます。 `Iterator` 修飾子は、Iterator 関数または `Get` アクセサーの宣言に記述されます。  
  
 [For Each...Next ステートメント](../statements/for-each-next-statement.md)を使用して、クライアント コードから反復子を呼び出します。  
  
 Iterator 関数または `Get` アクセサーの戻り値の型は、<xref:System.Collections.IEnumerable>、<xref:System.Collections.Generic.IEnumerable%601>、<xref:System.Collections.IEnumerator>、または <xref:System.Collections.Generic.IEnumerator%601> となります。  
  
 反復子に `ByRef` パラメーターを指定することはできません。  
  
 反復子を、イベント、インスタンス コンストラクター、静的コンストラクター、静的デストラクターで指定することはできません。  
  
 反復子は、匿名関数にすることができます。 詳細については、「 [反復子](../../programming-guide/concepts/iterators.md)」を参照してください。  
  
## <a name="usage"></a>使用方法  
 `Iterator` 修飾子は、次のコンテキストで使用できます。  
  
- [Function ステートメント](../statements/function-statement.md)  
  
- [Property ステートメント](../statements/property-statement.md)  
  
## <a name="example"></a>例  
 次の例では、Iterator 関数を示します。 Iterator 関数には、[For…Next](../statements/for-next-statement.md) ループ内に `Yield` ステートメントがあります。 `Main` 内の [For Each](../statements/for-each-next-statement.md) ステートメント本体の各反復処理では、`Power` Iterator 関数が呼び出されます。 Iterator 関数を呼び出すごとに、`Yield` ステートメントの次の実行に進みます。これは、`For…Next` ループの次の反復処理で行われます。  
  
 [!code-vb[VbVbalrStatements#98](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class2.vb#98)]  
  
## <a name="example"></a>例  
 次の例は、反復子である `Get` アクセサーを示しています。 `Iterator` 修飾子は、プロパティ宣言にあります。  
  
 [!code-vb[VbVbalrStatements#99](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class2.vb#99)]  
  
 その他の例については、「[反復子](../../programming-guide/concepts/iterators.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Runtime.CompilerServices.IteratorStateMachineAttribute>
- [反復子](../../programming-guide/concepts/iterators.md)
- [Yield ステートメント](../statements/yield-statement.md)
