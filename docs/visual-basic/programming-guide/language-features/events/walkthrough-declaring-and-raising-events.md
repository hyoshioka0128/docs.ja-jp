---
title: イベントの宣言と発生
ms.date: 07/20/2015
helpviewer_keywords:
- declarations [Visual Basic], events
- events [Visual Basic], walkthroughs
- declaring events [Visual Basic], walkthroughs
- events [Visual Basic], declaring
- events [Visual Basic], raising
- raising events [Visual Basic], walkthroughs
ms.assetid: 8ffb3be8-097d-4d3c-b71e-04555ebda2a2
ms.openlocfilehash: 3da60014d7ac95189c5d56c3e339ff1b054a40dc
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84405094"
---
# <a name="walkthrough-declaring-and-raising-events-visual-basic"></a>チュートリアル: イベントの宣言と発生 (Visual Basic)
このチュートリアルでは、`Widget` という名前のクラスのイベントを宣言し、発生させる方法について説明します。 この手順を完了したら、本トピックの対になっている「[チュートリアル: イベントの処理](walkthrough-handling-events.md)」も読むことをお勧めします。こちらでは、`Widget` オブジェクトのイベントを使用して、アプリケーションの状態に関する情報を示す方法について説明しています。  
  
## <a name="the-widget-class"></a>Widget クラス  
 このチュートリアルでは、`Widget` クラスがあるものと仮定します。 `Widget` クラスには、実行に時間のかかる可能性のあるメソッドが含まれているので、なんらかの完了率インジケーターをアプリケーションに表示することにします。  
  
 もちろん、完了率を示すダイアログ ボックスを `Widget` オブジェクトに表示してもかまいません。ただし、そうすると `Widget` クラスを使用するあらゆるプロジェクトで、このダイアログ ボックスが表示されることになります。 オブジェクト設計の原則は、オブジェクトの目的がフォームまたはダイアログ ボックスの管理だけである場合を除き、ユーザー インターフェイスの処理はオブジェクトを使用するアプリケーションに任せることです。  
  
 `Widget` の目的は別のタスクの実行ですので、`PercentDone` イベントを追加し、`Widget` のメソッドを呼び出すプロシージャにこのイベントを処理させて、最新の状態を表示させる方が適切です。 `PercentDone` イベントによって、タスクを取り消すメカニズムも提供できます。  
  
#### <a name="to-build-the-code-example-for-this-topic"></a>このトピックのコード例をビルドするには  
  
1. 新しい Visual Basic Windows アプリケーション プロジェクトを開き、`Form1` という名前のフォームを作成します。  
  
2. `Form1` にボタン 2 つとラベル 1 つを追加します。  
  
3. 次の表のように、各オブジェクトに名前を付けます。  
  
    |オブジェクト|プロパティ|設定|  
    |------------|--------------|-------------|  
    |`Button1`|`Text`|タスクの開始|  
    |`Button2`|`Text`|キャンセル|  
    |`Label`|`(Name)`、`Text`|lblPercentDone、0|  
  
4. **[プロジェクト]** メニューの **[クラスの追加]** を選択して、`Widget.vb` という名前のクラスをプロジェクトに追加します。  
  
#### <a name="to-declare-an-event-for-the-widget-class"></a>Widget クラスのイベントを宣言するには  
  
- `Event` キーワードを使用して、`Widget` クラス内でイベントを宣言します。 次の `Widget` の `PercentDone` イベントに示されているように、イベントには `ByVal` 引数と `ByRef` 引数を設定できます。  
  
     [!code-vb[VbVbcnWalkthroughDeclaringAndRaisingEvents#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnWalkthroughDeclaringAndRaisingEvents/VB/Widget.vb#1)]  
  
 呼び出し元オブジェクトが `PercentDone` イベントを受け取るとき、`Percent` 引数には完了したタスクの割合が含まれています。 `Cancel` 引数を `True` に設定すると、イベントを発生させたメソッドを取り消すことができます。  
  
> [!NOTE]
> イベントの引数は、プロシージャの引数と同様に宣言できますが、次のような例外があります。イベントに対して `Optional` 引数または `ParamArray` 引数を指定することはできません。また、イベントは値を返しません。  
  
 `PercentDone` イベントは、`Widget` クラスの `LongTask` メソッドで発生します。 `LongTask` は、メソッドの仮の実行時間と、`PercentDone` イベントの発生まで `LongTask` が一時停止する最短期間の 2 つを引数に取ります。  
  
#### <a name="to-raise-the-percentdone-event"></a>PercentDone イベントを発生させるには  
  
1. このクラスで使用する `Timer` プロパティにアクセスしやすくするため、`Imports` ステートメントを、クラス モジュールの宣言セクション先頭、`Class Widget` ステートメントの上に追加します。  
  
     [!code-vb[VbVbcnWalkthroughDeclaringAndRaisingEvents#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnWalkthroughDeclaringAndRaisingEvents/VB/Widget.vb#2)]  
  
2. `Widget` クラスに次のコードを追加します。  
  
     [!code-vb[VbVbcnWalkthroughDeclaringAndRaisingEvents#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnWalkthroughDeclaringAndRaisingEvents/VB/Widget.vb#3)]  
  
 アプリケーションで `LongTask` メソッドが呼び出されると、`MinimumInterval` 秒ごとに `Widget` クラスで `PercentDone` イベントが発生します。 イベントが返されると、`Cancel` 引数が `True` に設定されているかどうかが `LongTask` により確認されます。  
  
 ここで、いくつかの注意事項があります。 簡略化のため、`LongTask` プロシージャでは、タスクの実行所要時間があらかじめわかっているものと仮定しています。 このようなケースはほとんどありません。 タスクを均一サイズのチャンクに分割することは困難であり、また多くの場合、ユーザーにとって重要なことは、何かが起きたことを把握できるまでの時間の長さだけです。  
  
 お気付きのとおり、このサンプルには別の欠陥もあります。 `Timer` プロパティが返すのは、午前 0 時からの経過時間 (秒) です。そのため、アプリケーションは、午前 0 時の直前に開始された場合停止してしまいます。 より適切に時間を測定する方法としては、このような境界条件を考慮するか、`Now` などのプロパティを使用してこうした条件を完全に回避することが考えられます。  
  
 これで、`Widget` クラスでイベントを発生させられるようになり、次のチュートリアルに進む用意が整いました。 [チュートリアル: イベントの処理](walkthrough-handling-events.md)」で、`WithEvents` を使用してイベント ハンドラーを `PercentDone` イベントに関連付ける方法について学びましょう。  
  
## <a name="see-also"></a>関連項目

- <xref:Microsoft.VisualBasic.DateAndTime.Timer%2A>
- <xref:Microsoft.VisualBasic.DateAndTime.Now%2A>
- [チュートリアル: イベントの処理](walkthrough-handling-events.md)
- [イベント](index.md)
