---
title: イベントの処理
ms.date: 07/20/2015
helpviewer_keywords:
- event handling [Visual Basic], walkthroughs
- walkthroughs [Visual Basic], event handling
- variables [Visual Basic], WithEvents
- events [Visual Basic], walkthroughs
- WithEvents keyword [Visual Basic], walkthroughs
- event handlers [Visual Basic], walkthroughs
ms.assetid: f145b3fc-5ae0-4509-a2aa-1ff6934706bd
ms.openlocfilehash: 29d878afbe3669fc88e62b1fec98b306918c303d
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84405081"
---
# <a name="walkthrough-handling-events-visual-basic"></a>チュートリアル: イベントの処理 (Visual Basic)
これは、イベントの処理方法について説明した 2 つのトピックのうちの 2 番目にあたります。 1 番目のトピックである「[チュートリアル: イベントの宣言と発生](walkthrough-declaring-and-raising-events.md)」では、イベントを宣言し、発生させる方法について説明しました。 このセクションでは、そのチュートリアルのフォームとクラスを使用して、イベントの発生時にそれらを処理する方法を示します。  
  
 `Widget` クラスの例では、従来のイベント処理ステートメントを使用しています。 Visual Basic には、別のイベント処理手法も用意されています。 演習として、この例を変更し、`AddHandler` ステートメントと `Handles` ステートメントを使用してみましょう。  
  
### <a name="to-handle-the-percentdone-event-of-the-widget-class"></a>Widget クラスの PercentDone イベントを処理するには  
  
1. `Form1` に次のコードを挿入します。  
  
     [!code-vb[VbVbcnWalkthroughDeclaringAndRaisingEvents#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnWalkthroughDeclaringAndRaisingEvents/VB/Form1.vb#4)]  
  
     `WithEvents` キーワードにより、オブジェクトのイベントの処理に変数 `mWidget` が使用されるように指定しています。 オブジェクトの種類は、オブジェクトの作成元にするクラスの名前を記載することで指定します。  
  
     `WithEvents` 変数はクラスレベルである必要があるため、変数 `mWidget` は `Form1` 内で宣言します。 これは、挿入先のクラスの型に左右されません。  
  
     変数 `mblnCancel` は、`LongTask` メソッドを取り消すためのものです。  
  
## <a name="writing-code-to-handle-an-event"></a>イベントを処理するコードの作成  
 `WithEvents` を使用して変数を宣言すると、このクラスの**コード エディター**の左側にあるドロップダウン リストに、その変数の名前が表示されます。 `mWidget` を選択すると、右側のドロップダウン リストに `Widget` クラスのイベントが表示されます。 イベントを選択すると、対応するイベント プロシージャが、接頭辞 `mWidget` とアンダースコア付きで表示されます。 `WithEvents` 変数に関連するすべてのイベント プロシージャに、変数名が接頭辞として付与されます。  
  
#### <a name="to-handle-an-event"></a>イベントを処理するには  
  
1. **コード エディター**の左側のドロップダウン リストで、[`mWidget`] を選択します。  
  
2. 右側のドロップダウン リストで `PercentDone` イベントを選択します。 **コード エディター**に `mWidget_PercentDone` イベント プロシージャが表示されます。  
  
    > [!NOTE]
    > 新しいイベント ハンドラーを挿入する場合、**コード エディター**は便利ですが、使用は必須ではありません。 今回のチュートリアルでは、コードにイベント ハンドラーを直接コピーする方が簡単です。  
  
3. `mWidget_PercentDone` イベント ハンドラーに次のコードを追加します。  
  
     [!code-vb[VbVbcnWalkthroughDeclaringAndRaisingEvents#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnWalkthroughDeclaringAndRaisingEvents/VB/Form1.vb#5)]  
  
     `PercentDone` イベントが発生するたびに、イベント プロシージャにより `Label` コントロールに完了率が表示されます。 `DoEvents` メソッドによって、ラベルの再描画を許可すると同時に、 **[キャンセル]** ボタンをクリックする機会をユーザーに提供しています。  
  
4. `Button2_Click` イベント ハンドラーに次のコードを追加します。  
  
     [!code-vb[VbVbcnWalkthroughDeclaringAndRaisingEvents#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnWalkthroughDeclaringAndRaisingEvents/VB/Form1.vb#6)]  
  
 `LongTask` の実行中にユーザーが **[キャンセル]** ボタンをクリックすると、`DoEvents` ステートメントによりイベント処理の実行が許可されしだい、`Button2_Click` イベントが実行されます。 クラスレベルの変数 `mblnCancel` が `True` に設定された後、`mWidget_PercentDone` イベントによりテストが行われ、`ByRef Cancel` 引数が `True` に設定されます。  
  
## <a name="connecting-a-withevents-variable-to-an-object"></a>オブジェクトへの WithEvents 変数の接続  
 これで、`Widget` オブジェクトのイベントを処理するように `Form1` を設定できました。 あとは、`Widget` を見つけるだけです。  
  
 デザイン時に変数 `WithEvents` を宣言しても、変数にオブジェクトは関連付けられません。 `WithEvents` 変数は、単に他のオブジェクト変数と似たものです。 オブジェクトを作成してから、そのオブジェクトに対する参照を `WithEvents` 変数に割り当てる必要があります。  
  
#### <a name="to-create-an-object-and-assign-a-reference-to-it"></a>オブジェクトを作成して参照を割り当てるには  
  
1. **コード エディター**の左側のドロップダウン リストで、 **[(Form1 イベント)]** を選択します。  
  
2. 右側のドロップダウン リストで `Load` イベントを選択します。 **コード エディター**に `Form1_Load` イベント プロシージャが表示されます。  
  
3. `Form1_Load` イベント プロシージャに、`Widget` を作成する次のコードを追加します。  
  
     [!code-vb[VbVbcnWalkthroughDeclaringAndRaisingEvents#7](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnWalkthroughDeclaringAndRaisingEvents/VB/Form1.vb#7)]  
  
 このコードを実行すると、Visual Basic により `Widget` オブジェクトが作成され、そのイベントが `mWidget` に関連付けられているイベント プロシージャと接続されます。 この時点以降、`Widget` で `PercentDone` イベントが発生するたびに、`mWidget_PercentDone` イベント プロシージャが実行されます。  
  
#### <a name="to-call-the-longtask-method"></a>LongTask メソッドを呼び出すには  
  
- `Button1_Click` イベント ハンドラーに次のコードを追加します。  
  
     [!code-vb[VbVbcnWalkthroughDeclaringAndRaisingEvents#8](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnWalkthroughDeclaringAndRaisingEvents/VB/Form1.vb#8)]  
  
 `LongTask` メソッドを呼び出す前に、完了率を示すラベルを初期化する必要があります。また、メソッド取り消し用のクラスレベルの `Boolean` フラグを `False` に設定する必要があります。  
  
 タスクの実行時間を 12.2 秒に指定したうえで、`LongTask` が呼び出されています。 `PercentDone` イベントは 3 分の 1 秒ごとに発生します。 イベントが発生するたびに、`mWidget_PercentDone` イベント プロシージャが実行されます。  
  
 `LongTask` が完了すると `mblnCancel` がテストされ、`LongTask` が正常に完了したか、または `mblnCancel` が `True` に設定されていたために中止されたかどうかが確認されます。 完了率は、前者の場合にのみ更新されます。  
  
#### <a name="to-run-the-program"></a>プログラムを実行するには  
  
1. F5 キーを押して、プロジェクトを実行モードに切り替えます。  
  
2. **[タスクの開始]** をクリックします。 `PercentDone` イベントが発生するたびにラベルが更新され、完了したタスクの割合が示されます。  
  
3. タスクを停止するには、 **[キャンセル]** ボタンをクリックします。 **[キャンセル]** ボタンの外観は、クリックしてもすぐには変わらないことに注意してください。 `Click` イベントは、`My.Application.DoEvents` ステートメントでイベント処理が許可されるまで発生しません。  
  
    > [!NOTE]
    > `My.Application.DoEvents` メソッドがイベントを処理する方法は、フォームによる方法とは一部異なります。 たとえば、このチュートリアルでは、 **[キャンセル]** ボタンを 2 回クリックする必要があります。 フォームでイベントを直接処理できるようにするには、マルチスレッドを使用します。 詳細については、「[マネージド スレッド処理](../../../../standard/threading/index.md)」を参照してください。
  
 F11 キーを使用してプログラムを実行し、コードを一度に 1 行ずつステップ実行することをお勧めします。 `LongTask` の実行が開始された後、`PercentDone` イベントが発生するたびに `Form1` が一時的に再度開始されるようすを明確に確認できます。  
  
 `Form1` のコードが再実行されている間に、`LongTask` メソッドが再び呼び出されたらどうなるでしょうか。 イベント発生時に毎回 `LongTask` が呼び出されると、最悪の場合スタック オーバーフローが発生する可能性があります。  
  
 変数 `mWidget` に新しい `Widget` オブジェクトへの参照を割り当てることで、別の `Widget` のイベントを `mWidget` で処理できます。 実際には、ボタンをクリックするたびに、`Button1_Click` のコードでこの処理を実行可能です。  
  
#### <a name="to-handle-events-for-a-different-widget"></a>別のウィジェットのイベントを処理するには  
  
- `Button1_Click` プロシージャの `mWidget.LongTask(12.2, 0.33)` という行のすぐ下に、次のコード行を追加します。  
  
     [!code-vb[VbVbcnWalkthroughDeclaringAndRaisingEvents#9](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnWalkthroughDeclaringAndRaisingEvents/VB/Form1.vb#9)]  
  
 上記のコードでは、ボタンがクリックされるたびに新しい `Widget` を作成します。 `LongTask` メソッドが完了するとすぐに `Widget` への参照が解放され、`Widget` が破棄されます。  
  
 `WithEvents` 変数に含められるオブジェクト参照は一度に 1 つだけです。そのため、別の `Widget` オブジェクトを `mWidget` に割り当てると、前の `Widget` オブジェクトのイベントは処理されなくなります。 古い `Widget` への参照を含むオブジェクト変数が `mWidget` のみである場合、オブジェクトは破棄されます。 複数の `Widget` オブジェクトのイベントを処理する場合は、`AddHandler` ステートメントを使用して、各オブジェクトのイベントを個別に処理します。  
  
> [!NOTE]
> `WithEvents` 変数は必要な数だけ宣言できますが、`WithEvents` 変数の配列はサポートされません。  
  
## <a name="see-also"></a>関連項目

- [チュートリアル: イベントの宣言と発生](walkthrough-declaring-and-raising-events.md)
- [イベント](index.md)
