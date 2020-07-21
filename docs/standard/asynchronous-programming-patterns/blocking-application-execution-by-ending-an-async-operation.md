---
title: 非同期操作の終了によるアプリケーション実行のブロック
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- blocks, asynchronous operations
- AsyncWaitHandle property
- asynchronous programming, blocking applications
- blocking application execution
ms.assetid: cc5e2834-a65b-4df8-b750-7bdb79997fee
dev_langs:
- csharp
- vb
ms.openlocfilehash: 74976176acc0fbb948c514358b7bd323cc20c134
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84289955"
---
# <a name="blocking-application-execution-by-ending-an-async-operation"></a>非同期操作の終了によるアプリケーション実行のブロック
非同期操作の結果の待機中に、他の作業を継続できないアプリケーションは、操作が完了するまでブロックする必要があります。 次のオプションのいずれかを使用して、非同期操作が完了するまでの待機中に、アプリケーションのメイン スレッドをブロックします。  
  
- 非同期操作の **End**_OperationName_ メソッドを呼び出します。 このトピックでは、この方法のデモが実行されます。  
  
- 非同期操作の **Begin**_OperationName_ メソッドによって返される <xref:System.IAsyncResult> の <xref:System.IAsyncResult.AsyncWaitHandle%2A> プロパティを使用します。 この方法をデモの例については、「[AsyncWaitHandle の使用によるアプリケーション実行のブロック](blocking-application-execution-using-an-asyncwaithandle.md)」を参照してください。  
  
 非同期操作が完了するまでブロックするために **End**_OperationName_ メソッドを使用するアプリケーションは、通常は **Begin**_OperationName_ メソッドを呼び出し、操作の結果なしで実行できる任意の作業を実行して、**End**_OperationName_ を呼び出します。  
  
## <a name="example"></a>例  
 次のコード例は、ユーザー指定のコンピューターのドメイン ネーム システム情報を取得するために、<xref:System.Net.Dns> クラスの非同期メソッドを使用してデモを実行します。 この方法を使用する場合はこれらの引数は必要ないため、`null` (Visual Basic の場合は `Nothing`) は、<xref:System.Net.Dns.BeginGetHostByName%2A>`requestCallback` と `stateObject` パラメーターに渡されることに注意してください。  
  
 [!code-csharp[AsyncDesignPattern#1](../../../samples/snippets/csharp/VS_Snippets_CLR/AsyncDesignPattern/CS/Async_EndBlock.cs#1)]
 [!code-vb[AsyncDesignPattern#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/AsyncDesignPattern/VB/Async_EndBlock.vb#1)]  
  
## <a name="see-also"></a>参照

- [イベント ベースの非同期パターン (EAP)](event-based-asynchronous-pattern-eap.md)
- [イベントベースの非同期パターンの概要](event-based-asynchronous-pattern-overview.md)
