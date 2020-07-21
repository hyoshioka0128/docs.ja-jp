---
title: '方法: 並列ループの例外を処理する'
description: .NET で並列ループの例外を処理する方法について説明します。 System.AggregateException のループからすべての例外をラップする方法の例を参照します。
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- parallel loops, how to handle exceptions
ms.assetid: 512f0d5a-4636-4875-b766-88f20044f143
ms.openlocfilehash: 61c22d6e82282f8aeb54818c813d4489e3bc9641
ms.sourcegitcommit: 5fd4696a3e5791b2a8c449ccffda87f2cc2d4894
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2020
ms.locfileid: "84768977"
---
# <a name="how-to-handle-exceptions-in-parallel-loops"></a>方法: 並列ループの例外を処理する
<xref:System.Threading.Tasks.Parallel.For%2A?displayProperty=nameWithType> および <xref:System.Threading.Tasks.Parallel.ForEach%2A?displayProperty=nameWithType> のオーバーロード には、スローされる可能性のある例外を処理する特別な仕組みはありません。 この点では、標準の `for` ループおよび `foreach` ループ (Visual Basic では `For` と `For Each`) と似ており、現在実行中のイテレーションがすべて終了すると、処理されない例外によってループはただちに終了します。
  
 独自の例外処理のロジックを並列ループに追加する場合は、同様の例外が複数のスレッドに同時にスローされるケース、および特定のスレッドにスローされる例外が、別のスレッドに別の例外をスローするケースを処理してください。 <xref:System.AggregateException?displayProperty=nameWithType>  のループからすべての例外をラップすることで、両方のケースを処理できます。 考えられる方法の 1 つの例を次に示します。  
  
> [!NOTE]
> [マイ コードのみ] が有効になっている場合、Visual Studio では、例外をスローする行で処理が中断され、"ユーザー コードで処理されない例外" に関するエラー メッセージが表示されることがあります。 このエラーは問題にはなりません。 F5 キーを押して、処理が中断された箇所から続行し、以下の例に示す例外処理動作を確認できます。 Visual Studio による処理が最初のエラーで中断しないようにするには、 **[ツール] メニューの [オプション]、[デバッグ] 、[全般]** の順にクリックし、[マイ コードのみ] チェック ボックスをオフにします。  
  
## <a name="example"></a>例  
 この例では、すべての例外がキャッチされた後に <xref:System.AggregateException?displayProperty=nameWithType> にラップされ、スローされます。 呼び出し元は、どの例外を処理するかを決定できます。  
  
 [!code-csharp[TPL_Exceptions#08](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_exceptions/cs/exceptions.cs#08)]
 [!code-vb[TPL_Exceptions#08](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_exceptions/vb/exceptionsinloops.vb#08)]  
  
## <a name="see-also"></a>関連項目

- [データの並列化](data-parallelism-task-parallel-library.md)
- [PLINQ および TPL のラムダ式](lambda-expressions-in-plinq-and-tpl.md)
