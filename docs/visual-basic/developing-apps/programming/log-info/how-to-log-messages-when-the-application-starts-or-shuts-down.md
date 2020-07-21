---
title: '方法 : アプリケーションの起動時または終了時にメッセージをログに記録する'
ms.date: 07/20/2015
helpviewer_keywords:
- event logs, shutdown
- My.Application.Log object, logging
- Startup event [Visual Basic]
- event logs, startup
- Shutdown event [Visual Basic]
- My.Log object, logging
ms.assetid: 67624d05-cddf-48b7-8c36-5c99baa4c621
ms.openlocfilehash: ac5fb17e527bcbcb55f98ec0ced06c152555ce6c
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84410076"
---
# <a name="how-to-log-messages-when-the-application-starts-or-shuts-down-visual-basic"></a>方法: アプリケーションの起動時または終了時にメッセージをログに記録する (Visual Basic)

`My.Application.Log` オブジェクトおよび `My.Log` オブジェクトを使用すると、アプリケーション内で発生したイベントに関する情報をログに記録できます。 この例では、 `My.Application.Log.WriteEntry` イベントおよび `Startup` イベントで `Shutdown` メソッドを使用してトレース情報を書き込む方法を示します。  
  
### <a name="to-access-the-applications-event-handler-code"></a>アプリケーションのイベント ハンドラー コードにアクセスするには  
  
1. **ソリューション エクスプローラー**でプロジェクトを選択します。 **[プロジェクト]** メニューの **[プロパティ]** をクリックします。  
  
2. **[アプリケーション]** タブをクリックします。  
  
3. **[アプリケーション イベントの表示]** をクリックしてコード エディターを開きます。  
  
     ApplicationEvents.vb ファイルが開かれます。  
  
### <a name="to-log-messages-when-the-application-starts"></a>アプリケーションの起動時にメッセージをログに記録するには  
  
1. コード エディターで ApplicationEvents.vb ファイルを開きます。 **[全般]** メニューの **[MyApplication イベント]** をクリックします。  
  
2. **[宣言]** メニューの **[スタートアップ]** をクリックします。  
  
     アプリケーションでは、メイン アプリケーションの実行前に <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.Startup> イベントが発生します。  
  
3. `My.Application.Log.WriteEntry` イベント ハンドラーに `Startup` メソッドを追加します。  
  
     [!code-vb[VbVbalrMyApplicationLog#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyApplicationLog/VB/MyEventsFake.vb#1)]  
  
### <a name="to-log-messages-when-the-application-shuts-down"></a>アプリケーションの終了時にメッセージをログに記録するには  
  
1. コード エディターで ApplicationEvents.vb ファイルを開きます。 **[全般]** メニューの **[MyApplication イベント]** をクリックします。  
  
2. **[宣言]** メニューの **[シャットダウン]** をクリックします。  
  
     アプリケーションでは、メイン アプリケーションが実行された後、終了前に <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.Shutdown> イベントが発生します。  
  
3. `My.Application.Log.WriteEntry` イベント ハンドラーに `Shutdown` メソッドを追加します。  
  
     [!code-vb[VbVbalrMyApplicationLog#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyApplicationLog/VB/MyEventsFake.vb#2)]  
  
## <a name="example"></a>例  

 **プロジェクト デザイナー** を使用して、コード エディターでアプリケーション イベントにアクセスできます。 詳細については、「[[アプリケーション] ページ (プロジェクト デザイナー) (Visual Basic)](/visualstudio/ide/reference/application-page-project-designer-visual-basic)」を参照してください。  
  
 [!code-vb[VbVbalrMyApplicationLog#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyApplicationLog/VB/MyEventsFake.vb#3)]  
  
## <a name="see-also"></a>参照

- <xref:Microsoft.VisualBasic.Logging.Log?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.Logging.Log.WriteEntry%2A>
- <xref:Microsoft.VisualBasic.Logging.Log.WriteException%2A>
- [[アプリケーション] ページ (プロジェクト デザイナー) (Visual Basic)](/visualstudio/ide/reference/application-page-project-designer-visual-basic)
- [アプリケーション ログの使用](working-with-application-logs.md)
