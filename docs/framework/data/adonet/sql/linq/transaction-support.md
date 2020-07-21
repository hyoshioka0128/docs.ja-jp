---
title: トランザクションのサポート
ms.date: 03/30/2017
ms.assetid: 8cceb26e-8d36-4365-8967-58e2e89e0187
ms.openlocfilehash: 9c7128ef432fa609b8d628bc74caebe790058ede
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2019
ms.locfileid: "70792280"
---
# <a name="transaction-support"></a>トランザクションのサポート
[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] では、3 種類のトランザクション モデルがサポートされています。 チェックが行われる順に、これらのモデルを以下に示します。  
  
## <a name="explicit-local-transaction"></a>明示的なローカル トランザクション  
 <xref:System.Data.Linq.DataContext.SubmitChanges%2A> が呼び出されたときに <xref:System.Data.Linq.DataContext.Transaction%2A> プロパティが (`IDbTransaction`) トランザクションに設定されている場合、同じトランザクションのコンテキストで <xref:System.Data.Linq.DataContext.SubmitChanges%2A> 呼び出しが実行されます。  
  
 トランザクションの実行が終了したら、ユーザーがトランザクションをコミットまたはロールバックする必要があります。 トランザクションに対応する接続は、<xref:System.Data.Linq.DataContext> を構築するのに使用した接続に一致する必要があります。 異なる接続が使用されると、例外がスローされます。  
  
## <a name="explicit-distributable-transaction"></a>明示的な分散トランザクション  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] API (<xref:System.Data.Linq.DataContext.SubmitChanges%2A> など) は、アクティブな <xref:System.Transactions.Transaction> のスコープ内で呼び出すことができます。 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] によって呼び出しがトランザクションのスコープ内であることが検出されて、新しいトランザクションは作成されません。 この場合、[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] では接続の終了も回避されます。 このようなトランザクションのコンテキストで、クエリと <xref:System.Data.Linq.DataContext.SubmitChanges%2A> の実行が可能です。  
  
## <a name="implicit-transaction"></a>暗黙のトランザクション  
 <xref:System.Data.Linq.DataContext.SubmitChanges%2A> を呼び出すと、[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] によって、呼び出しが <xref:System.Transactions.Transaction> のスコープにあるかどうか、または `Transaction` プロパティ (`IDbTransaction`) がユーザーによって開始されたローカル トランザクションに設定されているかどうかがチェックされます。 どちらのトランザクションも見つからない場合、[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] によってローカル トランザクション (`IDbTransaction`) が開始され、それを使用して、生成された SQL コマンドが実行されます。 すべての SQL コマンドが終了すると、ローカル トランザクションがコミットされて [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] から戻ります。  
  
## <a name="see-also"></a>関連項目

- [背景情報](background-information.md)
- [方法: データ送信をトランザクションで囲む](how-to-bracket-data-submissions-by-using-transactions.md)
