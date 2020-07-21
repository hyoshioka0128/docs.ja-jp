---
title: '方法: 複数のキャンセル要求を待機する'
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- cancellation tokens, joining
- LinkedTokenSource, how to
ms.assetid: 6f4f3804-2ed7-41b4-a97a-6e32b93f6e05
ms.openlocfilehash: 3f92d1d9e8fec91475886e8bd7bffbc97bb632a0
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84279396"
---
# <a name="how-to-listen-for-multiple-cancellation-requests"></a>方法: 複数のキャンセル要求を待機する
この例では、2 つのキャンセル トークンを同時にリッスンして、いずれかのトークンからキャンセルが要求された場合に操作を取り消す方法を示します。  
  
> [!NOTE]
> [マイ コードのみ] が有効になっている場合、Visual Studio では、例外をスローする行で処理が中断され、"ユーザー コードで処理されない例外" に関するエラー メッセージが表示されることがあります。 このエラーは問題にはなりません。 F5 キーを押して、処理が中断された箇所から続行し、以下の例に示す例外処理動作を確認できます。 Visual Studio による処理が最初のエラーで中断しないようにするには、 **[ツール] メニューの [オプション]、[デバッグ] 、[全般]** の順にクリックし、[マイ コードのみ] チェック ボックスをオフにします。  
  
## <a name="example"></a>例  
 次の例では、<xref:System.Threading.CancellationTokenSource.CreateLinkedTokenSource%2A> メソッドを使用して 2 つのトークンを 1 つのトークンに結合します。 これで、1 つのキャンセル トークンのみを引数として受け取るメソッドにトークンを渡すことができます。 この例では、クラスの外部から渡されたトークンと、クラス内部で生成されたトークンの両方をメソッドで観察する必要がある一般的なシナリオを示します。  
  
 [!code-csharp[Cancellation#13](../../../samples/snippets/csharp/VS_Snippets_Misc/cancellation/cs/cancellationex13.cs#13)]
 [!code-vb[Cancellation#13](../../../samples/snippets/visualbasic/VS_Snippets_Misc/cancellation/vb/cancellationex13.vb#13)]  
  
 リンクされたトークンから <xref:System.OperationCanceledException> がスローされる場合、例外に渡されるトークンは先行トークンではなくリンクされたトークンです。 取り消されたトークンを特定するには、先行トークンの状態を直接確認します。  
  
 この例で <xref:System.AggregateException> がスローされることはまずありませんが、実際のシナリオでは、タスクのデリゲートからスローされた <xref:System.OperationCanceledException> 以外の例外はすべて <xref:System.AggregateException> にラップされるので、ここでキャッチされます。  
  
## <a name="see-also"></a>参照

- [マネージド スレッドのキャンセル](cancellation-in-managed-threads.md)
