---
title: '方法: 並列および順次の LINQ クエリを連結する'
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- parallel queries, combine parallel and sequential
ms.assetid: 1167cfe6-c8aa-4096-94ba-c66c3a4edf4c
ms.openlocfilehash: 2bdf074bc2977dc501e0726a52e825c89828565f
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84289539"
---
# <a name="how-to-combine-parallel-and-sequential-linq-queries"></a>方法: 並列および順次の LINQ クエリを連結する

この例では、PLINQ にクエリ内の後続のすべての演算子を順次処理するように指示する <xref:System.Linq.ParallelEnumerable.AsSequential%2A> メソッドの使用方法を示します。 順次処理はしばしば並列処理よりも遅いですが、正しい結果を出すためにこれが必要な場合もあります。  
  
> [!NOTE]
> この例は、使用方法を示すことを意図したものであるため、同等の順次的な LINQ to Objects クエリほど高速ではない可能性があります。 高速化の詳細については、「[PLINQ での高速化について](understanding-speedup-in-plinq.md)」を参照してください。  
  
## <a name="example"></a>例  
 次の例は、クエリの前の句で確立された順序を保持する <xref:System.Linq.ParallelEnumerable.AsSequential%2A> が必要な 1 つのシナリオを示します。  
  
 [!code-csharp[PLINQ#24](../../../samples/snippets/csharp/VS_Snippets_Misc/plinq/cs/plinqsamples.cs#24)]
 [!code-vb[PLINQ#24](../../../samples/snippets/visualbasic/VS_Snippets_Misc/plinq/vb/plinqsnippets1.vb#24)]  
  
## <a name="compiling-the-code"></a>コードのコンパイル  
 このコードをコンパイルして実行するには、これを [PLINQ データのサンプル](plinq-data-sample.md) プロジェクトに貼り付けて、`Main` からメソッドを呼び出す行を追加し、**F5** キーを押します。  
  
## <a name="see-also"></a>関連項目

- [Parallel LINQ (PLINQ)](introduction-to-plinq.md)
