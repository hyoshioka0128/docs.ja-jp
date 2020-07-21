---
title: Yield ステートメント
ms.date: 07/20/2015
f1_keywords:
- vb.Yield
helpviewer_keywords:
- iterators, Yield statement [Visual Basic]
- iterators [Visual Basic]
- Yield statement [Visual Basic]
ms.assetid: f33126c5-d7c4-43e2-8e36-4ae3f0703d97
ms.openlocfilehash: cc89e6f9bc2ccb4fff9a9fe12cd190a6b2d212dc
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84401369"
---
# <a name="yield-statement-visual-basic"></a>Yield ステートメント (Visual Basic)
コレクションの次の要素を `For Each...Next` ステートメントに送ります。  
  
## <a name="syntax"></a>構文  
  
```vb  
Yield expression  
```  
  
## <a name="parameters"></a>パラメーター  
  
|用語|定義|  
|---|---|  
|`expression`|必須です。 `Yield` ステートメントを含む iterator 関数または `Get` アクセサーの型に暗黙的に変換可能な式。|  
  
## <a name="remarks"></a>Remarks  
 `Yield` ステートメントでは、コレクションの要素を一度に 1 つずつ返します。 `Yield` ステートメントは、コレクションに対してカスタムの反復を実行する iterator 関数または `Get` アクセサーに含まれます。  
  
 iterator 関数を使用するには、[For Each...Next ステートメント](for-each-next-statement.md)または LINQ クエリを使用します。 `For Each` ループの各反復は、iterator 関数を呼び出します。 `Yield` ステートメントが iterator 関数に到達すると、`expression` が返され、コードの現在の位置が保持されます。 次回、Iterator 関数が呼び出されると、この位置から実行が再開されます。  
  
 `Yield` ステートメント内の `expression` の型から、iterator の戻り値の型への暗黙的な変換が存在する必要があります。  
  
 `Exit Function` または `Return` ステートメントを使用すると、反復を終了できます。  
  
 "Yield" は予約語ではなく、`Iterator` 関数または `Get` アクセサーで使用される場合にのみ特別な意味を持ちます。  
  
 iterator 関数と `Get` アクセサーの詳細については、「[反復子](../../programming-guide/concepts/iterators.md)」を参照してください。  
  
## <a name="iterator-functions-and-get-accessors"></a>iterator 関数と Get アクセサー  
 iterator 関数または `Get` アクセサーの宣言では、次の要件を満たしている必要があります。  
  
- [Iterator](../modifiers/iterator.md) 修飾子を含める必要があります。  
  
- 戻り値の型は、<xref:System.Collections.IEnumerable>、<xref:System.Collections.Generic.IEnumerable%601>、<xref:System.Collections.IEnumerator>、または <xref:System.Collections.Generic.IEnumerator%601> であることが必要です。  
  
- `ByRef` パラメーターを使用することはできません。  
  
 iterator 関数を、イベント、インスタンス コンストラクター、静的コンストラクター、静的デストラクターで指定することはできません。  
  
 iterator 関数は、匿名関数にすることができます。 詳細については、「 [反復子](../../programming-guide/concepts/iterators.md)」を参照してください。  
  
## <a name="exception-handling"></a>例外処理  
 `Yield` ステートメントは [Try...Catch...Finally ステートメント](try-catch-finally-statement.md)の `Try` ブロック内に指定できます。 `Yield` ステートメントがある `Try` ブロックには、`Catch` ブロックと `Finally` ブロックを記述することができます。  
  
 `Yield` ステートメントを `Catch` ブロックや `Finally` ブロックに記述することはできません。  
  
 (iterator 関数の外部の) `For Each` 本体で例外がスローされた場合、iterator 関数の `Catch` ブロックは実行されず、iterator 関数の `Finally` ブロックが実行されます。 iterator 関数内の `Catch` ブロックでキャッチされるのは、iterator 関数内で発生した例外だけです。  
  
## <a name="technical-implementation"></a>技術的な実装  
 次のコードでは、iterator 関数から `IEnumerable (Of String)` を返した後、`IEnumerable (Of String)` の要素を反復処理しています。  
  
```vb  
Dim elements As IEnumerable(Of String) = MyIteratorFunction()  
    …  
For Each element As String In elements  
Next  
```  
  
 `MyIteratorFunction` への呼び出しでは、関数の本体は実行されません。 この呼び出しでは、`IEnumerable(Of String)` が `elements` 変数に返されます。  
  
 `For Each` ループの反復処理では、<xref:System.Collections.IEnumerator.MoveNext%2A> について `elements` メソッドが呼び出されます。 この呼び出しでは、次の `MyIteratorFunction` ステートメントに到達するまで、`Yield` の本体が実行されます。 `Yield` ステートメントによって、ループ本体で使用するための `element` 変数の値だけでなく、`IEnumerable (Of String)` である要素の <xref:System.Collections.Generic.IEnumerator%601.Current%2A> プロパティも判断する式が返されます。  
  
 `For Each` ループの以降の各反復処理では、反復子本体の実行が中断した場所から続行し、`Yield` ステートメントに到達したときに再度停止します。 iterator 関数または `Return` または `Exit Function` ステートメントの最後に到達すると、`For Each` ループは完了します。  
  
## <a name="example"></a>例  
 次の例では、[For…Next](for-next-statement.md) ループ内に `Yield` ステートメントが含まれます。 `Main` 内の [For Each](for-each-next-statement.md) ステートメント本体の各反復処理では、`Power` Iterator 関数が呼び出されます。 Iterator 関数を呼び出すごとに、`Yield` ステートメントの次の実行に進みます。これは、`For…Next` ループの次の反復処理で行われます。  
  
 Iterator メソッドの戻り値の型は、反復子インターフェイス型の <xref:System.Collections.Generic.IEnumerable%601> です。 Iterator メソッドが呼び出されると、数値の累乗を含む列挙可能なオブジェクトが返されます。  
  
 [!code-vb[VbVbalrStatements#98](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class2.vb#98)]  
  
## <a name="example"></a>例  
 次の例は、反復子である `Get` アクセサーを示しています。 プロパティの宣言には、`Iterator` 修飾子が含まれます。  
  
 [!code-vb[VbVbalrStatements#99](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class2.vb#99)]  
  
 その他の例については、「[反復子](../../programming-guide/concepts/iterators.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- [ステートメント](index.md)
