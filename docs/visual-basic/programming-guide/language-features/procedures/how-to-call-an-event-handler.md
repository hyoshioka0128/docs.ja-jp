---
title: '方法: イベント ハンドラーを呼び出す'
ms.date: 07/20/2015
helpviewer_keywords:
- Visual Basic code, procedures
- event handlers [Visual Basic], calling
- event handlers
- procedures [Visual Basic], event handlers
- procedures [Visual Basic], calling
ms.assetid: 72e18ef8-144e-40df-a1f4-066a57271e28
ms.openlocfilehash: 0c626a9ad92fe2cd0ea117a9abdd2965a09df2ea
ms.sourcegitcommit: 17ee6605e01ef32506f8fdc686954244ba6911de
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74340428"
---
# <a name="how-to-call-an-event-handler-in-visual-basic"></a>方法: Visual Basic でイベント ハンドラーを呼び出す

"*イベント*" とは、何らかのプログラム コンポーネントによって認識されるアクションまたは発生 (マウス クリックやクレジット限度額の超過など) であり、それらに対して応答するコードを記述することができます。 "*イベント ハンドラー*" とは、イベントに応答するために記述するコードです。

 Visual Basic のイベント ハンドラーは `Sub` プロシージャです。 ただし、通常は、これを他の `Sub` プロシージャと同じ方法で呼び出すことはありません。 代わりに、プロシージャをイベントのハンドラーとして指定します。 これを行うには、[Handles](../../../language-reference/statements/handles-clause.md) 句と [WithEvents](../../../language-reference/modifiers/withevents.md) 変数を使用することも、[AddHandler ステートメント](../../../language-reference/statements/addhandler-statement.md)を使用することもできます。 `Handles` 句の使用が、Visual Basic でイベント ハンドラーを宣言する場合の既定の方法となります。 統合開発環境 (IDE) でプログラミングする場合、デザイナーではこの方法を使用してイベント ハンドラーが記述されます。 `AddHandler` ステートメントは、実行時にイベントを動的に発生させるのに適しています。

 イベントが発生すると、イベント ハンドラー プロシージャが Visual Basic によって自動的に呼び出されます。 イベントへのアクセス権を持つコードいずれも、[RaiseEvent ステートメント](../../../language-reference/statements/raiseevent-statement.md)を実行することによってそれを発生させることができます。

 複数のイベント ハンドラーを同じイベントに関連付けることができます。 場合によっては、ハンドラーとイベントとの関連付けを解除することができます。 詳細については、「[イベント](../events/index.md)」を参照してください。

### <a name="to-call-an-event-handler-using-handles-and-withevents"></a>Handles および WithEvents を使用してイベント ハンドラーを呼び出すには

1. [Event ステートメント](../../../language-reference/statements/event-statement.md)を使用してイベントが宣言されていることを確認します。

2. [WithEvents](../../../language-reference/modifiers/withevents.md) キーワードを使用して、モジュール レベルまたはクラス レベルでオブジェクト変数を宣言します。 この変数の `As` 句で、イベントを発生させるクラスを指定する必要があります。

3. イベント処理プロシージャ `Sub` の宣言内に、`WithEvents` 変数とイベント名を指定する [Handles](../../../language-reference/statements/handles-clause.md) 句を追加します。

4. イベントが発生すると、`Sub` プロシージャが Visual Basic によって自動的に呼び出されます。 コードでは、`RaiseEvent` ステートメントを使用してイベントを発生させることができます。

     次の例では、イベントと共に、そのイベントを発生させるクラスを参照する `WithEvents` 変数を定義します。 イベント処理プロシージャ `Sub` では、`Handles` 句を使用して、処理するクラスとイベントが指定されます。

     [!code-vb[VbVbcnProcedures#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#4)]

### <a name="to-call-an-event-handler-using-addhandler"></a>AddHandler を使用してイベント ハンドラーを呼び出すには

1. `Event` ステートメントを使用してイベントが宣言されていることを確認します。

2. [AddHandler ステートメント](../../../language-reference/statements/addhandler-statement.md)を実行して、イベント処理プロシージャ `Sub` をイベントに動的に接続します。

3. イベントが発生すると、`Sub` プロシージャが Visual Basic によって自動的に呼び出されます。 コードでは、`RaiseEvent` ステートメントを使用してイベントを発生させることができます。

     次の例では、フォームの <xref:System.Windows.Forms.Form.Closing> イベントを処理するための `Sub` プロシージャを定義します。 次に、[AddHandler ステートメント](../../../language-reference/statements/addhandler-statement.md)を使用して、`catchClose` プロシージャを <xref:System.Windows.Forms.Form.Closing> のイベント ハンドラーとして関連付けます。

     [!code-vb[VbVbcnProcedures#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#5)]

     イベント ハンドラーとイベントの関連付けを解除するには、[RemoveHandler ステートメント](../../../language-reference/statements/removehandler-statement.md)を実行します。

## <a name="see-also"></a>関連項目

- [手順](index.md)
- [Sub プロシージャ](sub-procedures.md)
- [Sub ステートメント](../../../language-reference/statements/sub-statement.md)
- [AddressOf 演算子](../../../language-reference/operators/addressof-operator.md)
- [方法: プロシージャを作成する](how-to-create-a-procedure.md)
- [方法: 値を返さないプロシージャを呼び出す](how-to-call-a-procedure-that-does-not-return-a-value.md)
