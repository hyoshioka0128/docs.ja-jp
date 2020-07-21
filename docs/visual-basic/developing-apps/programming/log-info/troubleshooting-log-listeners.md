---
title: 'トラブルシューティング : ログ リスナー'
ms.date: 07/20/2015
helpviewer_keywords:
- event logs, troubleshooting
- troubleshooting Visual Basic, event logs
- troubleshooting event logs
ms.assetid: ac6eb760-3d5d-461e-aedd-40599ee22e49
ms.openlocfilehash: 8d2d8294d9e9bb42d72fe4f6c37bf846bd644907
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84398319"
---
# <a name="troubleshooting-log-listeners-visual-basic"></a>トラブルシューティング: ログ リスナー (Visual Basic)

`My.Application.Log` オブジェクトおよび `My.Log` オブジェクトを使用すると、アプリケーション内で発生したイベントに関する情報をログに記録できます。  
  
 これらのメッセージをどのログ リスナーが受け取るかを確認するには、「[チュートリアル : My.Application.Log による情報の書き込み先の確認](walkthrough-determining-where-my-application-log-writes-information.md)」をご覧ください。  
  
 `Log` オブジェクトでログ フィルターを使って、ログに記録される情報の量を制限できます。 フィルターが正しく構成されていない場合、ログに誤った情報が含まれる可能性があります。 フィルターについて詳しくは、「[チュートリアル: My.Application.Log の出力をフィルター処理する](walkthrough-filtering-my-application-log-output.md)」をご覧ください。  
  
 一方、ログが正しく構成されていない場合は、現在の構成についてさらに情報が必要な場合があります。 ログの高度な `TraceSource` プロパティを使って、この情報を取得できます。  
  
### <a name="to-determine-the-log-listeners-for-the-log-object-in-code"></a>コードで Log オブジェクトのログ リスナーを特定するには  
  
1. コード ファイルの先頭に <xref:System.Diagnostics> 名前空間をインポートします。 詳細については、「[Imports ステートメント (.NET 名前空間および型)](../../../language-reference/statements/imports-statement-net-namespace-and-type.md)」を参照してください。  
  
     [!code-vb[VbVbalrMyApplicationLog#13](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyApplicationLog/VB/Form1.vb#13)]  
  
2. 各ログ リスナーの情報で構成される文字列を返す関数を作成します。  
  
     [!code-vb[VbVbalrMyApplicationLog#14](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyApplicationLog/VB/Form1.vb#14)]  
  
3. ログのトレース リスナーのコレクションを `GetListeners` 関数に渡し、戻り値を表示します。  
  
     [!code-vb[VbVbalrMyApplicationLog#19](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyApplicationLog/VB/Form1.vb#19)]  
  
     詳細については、<xref:Microsoft.VisualBasic.Logging.Log.TraceSource%2A> を参照してください。  
  
## <a name="see-also"></a>参照

- <xref:Microsoft.VisualBasic.Logging.Log?displayProperty=nameWithType>
- [アプリケーション ログの使用](working-with-application-logs.md)
- [チュートリアル : My.Application.Log による情報の書き込み先の確認](walkthrough-determining-where-my-application-log-writes-information.md)
