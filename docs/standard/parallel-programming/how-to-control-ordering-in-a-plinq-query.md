---
title: '方法: PLINQ クエリの順序を制御する'
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- PLINQ queries, how to control ordering
ms.assetid: c67eccc7-004d-4b2f-987e-919cbbd62ef7
ms.openlocfilehash: 80e199d75471eba219f1f3da12d307b6cd1d90cf
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84285457"
---
# <a name="how-to-control-ordering-in-a-plinq-query"></a>方法: PLINQ クエリの順序を制御する
以下の例では、<xref:System.Linq.ParallelEnumerable.AsOrdered%2A> 拡張メソッドを使用して PLINQ クエリの順序を制御する方法を示します。  
  
> [!WARNING]
> これらの例は使用法を示すことを主な目的としており、同等の LINQ to Objects 順次クエリよりも実行速度が速い場合もあれば遅い場合もあります。  
  
## <a name="example"></a>例  
 次の例では、ソース シーケンスの順序を維持します。 この操作が必要になるのは、たとえば、正確な結果を生成するためにクエリ演算子で順序ありのソース シーケンスが求められる場合です。  
  
 [!code-csharp[PLINQ#12](../../../samples/snippets/csharp/VS_Snippets_Misc/plinq/cs/plinqsamples.cs#12)]
 [!code-vb[PLINQ#12](../../../samples/snippets/visualbasic/VS_Snippets_Misc/plinq/vb/plinqsnippets1.vb#12)]  
  
## <a name="example"></a>例  
 次の例は、ソース シーケンスで順序付けが求められるクエリ演算子を示しています。 これらの演算子は、順序なしのシーケンスで動作しますが、予測できない結果を生成する場合があります。  
  
 [!code-csharp[PLINQ#14](../../../samples/snippets/csharp/VS_Snippets_Misc/plinq/cs/plinqsamples.cs#14)]
 [!code-vb[PLINQ#14](../../../samples/snippets/visualbasic/VS_Snippets_Misc/plinq/vb/plinqsnippets1.vb#14)]  
  
 このメソッドを実行するには、[PLINQ データのサンプル](plinq-data-sample.md) プロジェクトの PLINQDataSample クラスに貼り付け、F5 キーを押します。  
  
## <a name="example"></a>例  
 次の例は、クエリの最初の部分で順序を維持した後に、join 句のパフォーマンスを向上させるために順序を削除し、最終的な結果に順序を再適用する方法を示しています。  
  
 [!code-csharp[PLINQ#15](../../../samples/snippets/csharp/VS_Snippets_Misc/plinq/cs/plinqsamples.cs#15)]
 [!code-vb[PLINQ#15](../../../samples/snippets/visualbasic/VS_Snippets_Misc/plinq/vb/plinqsnippets1.vb#15)]  
  
 このメソッドを実行するには、[PLINQ データのサンプル](plinq-data-sample.md) プロジェクトの PLINQDataSample クラスに貼り付け、F5 キーを押します。  
  
## <a name="see-also"></a>参照

- <xref:System.Linq.ParallelEnumerable>
- [Parallel LINQ (PLINQ)](introduction-to-plinq.md)
