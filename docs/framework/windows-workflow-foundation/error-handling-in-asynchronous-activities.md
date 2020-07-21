---
title: 非同期アクティビティ内のエラー処理
ms.date: 03/30/2017
ms.assetid: e8f8ce2b-50c9-4e44-b187-030e0cf30a5d
ms.openlocfilehash: c63ce231687b03bdba57edd38c32270eabeff834
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79182947"
---
# <a name="error-handling-in-asynchronous-activities"></a>非同期アクティビティ内のエラー処理
<xref:System.Activities.AsyncCodeActivity> でのエラー処理には、アクティビティのコールバック システムを使用したエラーの送信が含まれています。 このトピックでは、SendMail アクティビティのサンプルを使用してホストへ非同期操作でスローされるエラーを取得する方法について説明します。  
  
## <a name="returning-an-error-thrown-in-an-asynchronous-activity-back-to-the-host"></a>非同期アクティビティでスローされたエラーをホストへ返す  
 SendMail アクティビティ サンプルでの、ホストに返される非同期操作でのエラーのルーティングの手順は次のとおりです。  
  
- Exception プロパティを `SendMailAsyncResult` クラスに追加します。  
  
- スローされたエラーを `SendCompleted` イベント ハンドラー内でそのプロパティにコピーします。  
  
- `EndExecute` イベント ハンドラー内で例外をスローします。  
  
 結果として得られるコードは次のようになります。  
  
```csharp  
class SendMailAsyncResult : IAsyncResult  
        {  
            …  
            public Exception Error { get; set; }
            …  
            void SendCompleted(object sender, AsyncCompletedEventArgs e)  
            {  
                Error = e.Error;  
                this.asyncWaitHandle.Set();  
                callback(this);  
            }  
         }  
  
    public sealed class SendMail: AsyncCodeActivity  
    {  
         …  
        protected override void EndExecute(AsyncCodeActivityContext context, IAsyncResult result)  
        {  
            SendMailAsyncResult sendMailResult = result as SendMailAsyncResult;  
            if (sendMailResult != null && sendMailResult.Error != null)  
                throw sendMailResult.Error;
        }  
    }  
```
