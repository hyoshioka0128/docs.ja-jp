---
title: '方法: タスクから値を返す'
description: .NET で System.Threading.Tasks.Task<TResult> 型を使用して Result プロパティから値を返す方法について参照します。
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- tasks, how to return a value
ms.assetid: c4bc0f44-eba2-4e96-9e03-1cc787461e61
ms.openlocfilehash: 051cef7cac654e4369ec1486884876004370ba0b
ms.sourcegitcommit: 5fd4696a3e5791b2a8c449ccffda87f2cc2d4894
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2020
ms.locfileid: "84767976"
---
# <a name="how-to-return-a-value-from-a-task"></a>方法: タスクから値を返す
この例では、<xref:System.Threading.Tasks.Task%601?displayProperty=nameWithType> の型を使用して <xref:System.Threading.Tasks.Task%601.Result%2A> プロパティから値を返す方法を示します。 C:\Users\Public\Pictures\Sample Pictures\ ディレクトリが存在している必要があり、それがファイルを含んでいる必要があります。  
  
## <a name="example"></a>例  
 [!code-csharp[TPL#10](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl/cs/returnavalue10.cs#10)]
 [!code-vb[TPL#10](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl/vb/10_returnavalue.vb#10)]  
  
 <xref:System.Threading.Tasks.Task%601.Result%2A> プロパティは、タスクが終了するまで呼び出し元のスレッドをブロックします。  
  
 1 つの <xref:System.Threading.Tasks.Task%601?displayProperty=nameWithType> の結果を継続タスクに渡す方法を確認するには、「[継続タスクを使用したタスクの連結](chaining-tasks-by-using-continuation-tasks.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- [タスク ベースの非同期プログラミング](task-based-asynchronous-programming.md)
- [PLINQ および TPL のラムダ式](lambda-expressions-in-plinq-and-tpl.md)
