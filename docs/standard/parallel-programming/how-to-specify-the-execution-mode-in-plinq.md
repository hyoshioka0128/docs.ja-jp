---
title: '方法: PLINQ の実行モードを指定する'
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- PLINQ queries, how to use execution mode
ms.assetid: e52ff26c-c5d3-4fab-9fec-c937fb387963
ms.openlocfilehash: 39ccde003b60ac9cbcff7ab824103a9cf37cc453
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84288096"
---
# <a name="how-to-specify-the-execution-mode-in-plinq"></a>方法: PLINQ の実行モードを指定する

この例では、PLINQ に既定のヒューリスティックをバイパスさせ、クエリのシェイプに関係なくクエリを並列化する方法を示します。  
  
> [!NOTE]
> この例は、使用方法を示すことを意図したものであるため、同等の順次的な LINQ to Objects クエリほど高速ではない可能性があります。 高速化の詳細については、「[PLINQ での高速化について](understanding-speedup-in-plinq.md)」を参照してください。  
  
## <a name="example"></a>例  
 [!code-csharp[PLINQ#22](../../../samples/snippets/csharp/VS_Snippets_Misc/plinq/cs/plinqsamples.cs#22)]
 [!code-vb[PLINQ#22](../../../samples/snippets/visualbasic/VS_Snippets_Misc/plinq/vb/plinqsnippets1.vb#22)]  
  
 PLINQ は、並列化を利用しやすくするために設計されています。 ただし、すべてのクエリが並列実行の利点を活用できるわけではありません。 たとえば、大きなことを実行しない単一のユーザー デリゲートがクエリに含まれる場合、順次実行の方が速度が速くなります。 順次実行の方が速度が速いのは、並列実行を有効にするために必要なオーバーヘッドが、得られる高速化の負荷より大きいためです。 このため、PLINQ はすべてのクエリを自動的に並列化するわけではありません。 最初に、クエリのシェイプとクエリを構成しているさまざまな演算子を調べます。 この分析に基づいて、既定の実行モードの PLINQ によって、クエリの一部またはすべてを順次実行するかどうかが決定されます。 ただし、PLINQ が分析から判断するよりも、ユーザーの方がクエリをより詳しく理解している場合があります。 たとえば、デリゲートの負荷が大きいため、クエリで並列化を使用する方がよいとわかっているとします。 このような場合は、<xref:System.Linq.ParallelEnumerable.WithExecutionMode%2A> メソッドを使用し、<xref:System.Linq.ParallelExecutionMode.ForceParallelism> 値を指定することで、クエリを常に並列実行するよう PLINQ に指示できます。  
  
## <a name="compiling-the-code"></a>コードのコンパイル  
 このコードをコピーして [PLINQ データのサンプル](plinq-data-sample.md) に貼り付けて、`Main` からメソッドを呼び出します。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Linq.ParallelEnumerable.AsSequential%2A>
- [Parallel LINQ (PLINQ)](introduction-to-plinq.md)
