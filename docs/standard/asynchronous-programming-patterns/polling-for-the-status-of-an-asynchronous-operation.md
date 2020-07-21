---
title: 非同期操作のステータスのポーリング
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- asynchronous programming, status polling
- polling asynchronous operation status
- status information [.NET Framework], asynchronous operations
ms.assetid: b541af31-dacb-4e20-8847-1b1ff7c35363
ms.openlocfilehash: f10b4ae5617edc8cf8a38a6cbac999e10a935dc2
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84291384"
---
# <a name="polling-for-the-status-of-an-asynchronous-operation"></a>非同期操作のステータスのポーリング
非同期操作の結果の待機中に、他の作業を実行できるアプリケーションは、操作が完了するまで待機をブロックする必要はありません。 次のオプションのいずれかを使用して、非同期操作が完了するまでの待機中に、手順の実行を継続します。  
  
- 非同期操作の **Begin**_OperationName_ メソッドによって返される <xref:System.IAsyncResult> の <xref:System.IAsyncResult.IsCompleted%2A> プロパティを使用して、その操作が完了したかどうかを判断します。 この方法はポーリングと呼ばれ、このトピックでデモが実行されます。  
  
- <xref:System.AsyncCallback> デリゲートを使用し、個別のスレッドで非同期操作の結果を処理します。 この方法のデモを実行する例については、「[AsyncCallback デリゲートの使用による非同期操作の終了](using-an-asynccallback-delegate-to-end-an-asynchronous-operation.md)」を参照してください。  
  
## <a name="example"></a>例  
 次のコード例は、ユーザー指定のコンピューターのドメイン ネーム システム情報を取得するために、<xref:System.Net.Dns> クラスの非同期メソッドを使用してデモを実行します。 この例では、非同期操作が開始され、操作が完了するまでコンソールにピリオド (".") が出力されます。 この方法を使用する場合はこれらの引数は必要ないため、**null** (Visual Basic の場合は **Nothing**) は、<xref:System.Net.Dns.BeginGetHostByName%2A><xref:System.AsyncCallback> と <xref:System.Object> パラメーターに渡されることに注意してください。  
  
 [!code-csharp[AsyncDesignPattern#3](../../../samples/snippets/csharp/VS_Snippets_CLR/AsyncDesignPattern/CS/Async_Poll.cs#3)]
 [!code-vb[AsyncDesignPattern#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/AsyncDesignPattern/VB/Async_Poll.vb#3)]  
  
## <a name="see-also"></a>参照

- [イベント ベースの非同期パターン (EAP)](event-based-asynchronous-pattern-eap.md)
- [イベントベースの非同期パターンの概要](event-based-asynchronous-pattern-overview.md)
