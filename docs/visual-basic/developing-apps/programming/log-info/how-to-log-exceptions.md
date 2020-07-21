---
title: '方法 : 例外をログに記録する'
ms.date: 07/20/2015
helpviewer_keywords:
- exceptions, logging
- exceptions, tracking
ms.assetid: a26c60e2-ae39-444a-aebb-33eccadc0eeb
ms.openlocfilehash: 59ed7b836126a38f32b7c6f479570a566d236e6c
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84410115"
---
# <a name="how-to-log-exceptions-in-visual-basic"></a>方法: Visual Basic で例外をログに記録する

`My.Application.Log` オブジェクトおよび `My.Log` オブジェクトを使用すると、アプリケーション内で発生した例外に関する情報をログに記録できます。 以下の例では、`My.Application.Log.WriteException` メソッドを使用して、明示的にキャッチした例外および未処理の例外をログに記録する方法を示します。  
  
 トレース情報をログに記録するには、`My.Application.Log.WriteEntry` メソッドを使用します。 詳細については、「<xref:Microsoft.VisualBasic.Logging.Log.WriteEntry%2A>」を参照してください。  
  
### <a name="to-log-a-handled-exception"></a>処理した例外をログに記録するには  
  
1. 例外情報を生成するメソッドを作成します。  
  
     [!code-vb[VbVbalrMyApplicationLog#9](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyApplicationLog/VB/Form1.vb#9)]  
  
2. `Try...Catch` ブロックを使用して例外をキャッチします。  
  
     [!code-vb[VbVbalrMyApplicationLog#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyApplicationLog/VB/Form1.vb#6)]  
  
3. 例外が発生する可能性のあるコードを `Try` ブロックに記述します。  
  
     `Dim` 行と `MsgBox` 行のコメントを解除すると、<xref:System.NullReferenceException> 例外が発生します。  
  
     [!code-vb[VbVbalrMyApplicationLog#7](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyApplicationLog/VB/Form1.vb#7)]  
  
4. `Catch` ブロックで、`My.Application.Log.WriteException` メソッドを使用して例外情報を書き込みます。  
  
     [!code-vb[VbVbalrMyApplicationLog#8](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyApplicationLog/VB/Form1.vb#8)]  
  
     次の例は、処理した例外をログに記録するコード全体を示しています。  
  
     [!code-vb[VbVbalrMyApplicationLog#10](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyApplicationLog/VB/Form1.vb#10)]  
  
### <a name="to-log-an-unhandled-exception"></a>未処理の例外をログに記録するには  
  
1. **ソリューション エクスプローラー**でプロジェクトを選択します。 **[プロジェクト]** メニューの **[プロパティ]** をクリックします。  
  
2. **[アプリケーション]** タブをクリックします。  
  
3. **[アプリケーション イベントの表示]** をクリックしてコード エディターを開きます。  
  
     ApplicationEvents.vb ファイルが開かれます。  
  
4. コード エディターで ApplicationEvents.vb ファイルを開きます。 **[全般]** メニューの **[MyApplication イベント]** をクリックします。  
  
5. **[宣言]** メニューの **[UnhandledException]** をクリックします。  
  
     アプリケーションでは、メイン アプリケーションの実行前に <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.UnhandledException> イベントが発生します。  
  
6. `My.Application.Log.WriteException` イベント ハンドラーに `UnhandledException` メソッドを追加します。  
  
     [!code-vb[VbVbalrMyApplicationLog#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyApplicationLog/VB/MyEventsFake.vb#4)]  
  
     次の例は、未処理の例外をログに記録するためのコード全体を示しています。  
  
     [!code-vb[VbVbalrMyApplicationLog#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyApplicationLog/VB/MyEventsFake.vb#5)]  
  
## <a name="see-also"></a>参照

- <xref:Microsoft.VisualBasic.Logging.Log?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.Logging.Log.WriteEntry%2A>
- <xref:Microsoft.VisualBasic.Logging.Log.WriteException%2A>
- [アプリケーション ログの使用](working-with-application-logs.md)
- [方法: ログ メッセージを書き込む](how-to-write-log-messages.md)
- [チュートリアル : My.Application.Log による情報の書き込み先の確認](walkthrough-determining-where-my-application-log-writes-information.md)
- [チュートリアル : My.Application.Log による情報の書き込み先の変更](walkthrough-changing-where-my-application-log-writes-information.md)
