---
title: '方法: 単純な PLINQ クエリを作成して実行する'
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- PLINQ queries, how to create
ms.assetid: 983b4213-bddd-4a44-9262-cbe59186df4c
ms.openlocfilehash: a9c044254423d0f9d266539c728a6604f562e97d
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84290007"
---
# <a name="how-to-create-and-execute-a-simple-plinq-query"></a>方法: 単純な PLINQ クエリを作成して実行する

この記事の例では、ソース シーケンスに対する <xref:System.Linq.ParallelEnumerable.AsParallel%2A?displayProperty=nameWithType> 拡張メソッドを使用して単純な並列統合言語クエリ (LINQ) クエリを作成し、<xref:System.Linq.ParallelEnumerable.ForAll%2A?displayProperty=nameWithTyp> メソッドを使用して、そのクエリを実行する方法を示します。  
  
> [!NOTE]
> ここでは、ラムダ式を使用して PLINQ でデリゲートを定義します。 C# または Visual Basic のラムダ式についての情報が必要な場合は、「[Lambda Expressions in PLINQ and TPL (PLINQ および TPL のラムダ式)](lambda-expressions-in-plinq-and-tpl.md)」を参照してください。  
  
## <a name="example"></a>例  
 [!code-csharp[PLINQ#11](../../../samples/snippets/csharp/VS_Snippets_Misc/plinq/cs/create1.cs#11)]
 [!code-vb[PLINQ#11](../../../samples/snippets/visualbasic/VS_Snippets_Misc/plinq/vb/create1.vb#11)]  
  
 この例では、結果シーケンスの順序付けが重要ではない場合に、並列 LINQ クエリを作成して実行する基本的なパターンを示しています。 通常、順序なしのクエリは、順序ありのクエリより高速です。 このクエリはソースを、複数のスレッドで非同期的に実行した複数のタスクにパーティション分割します。 各タスクが完了する順序は、その特定のパーティションに含まれる要素を処理するために必要な作業量だけでなく、オペレーティング システムが各スレッドをどのようにスケジュールするかといった外部要因にも依存します。 この例は、使用方法を示すことを意図したものであるため、同等の順次的な LINQ to Objects クエリほど高速ではない可能性があります。 高速化の詳細については、「[PLINQ での高速化について](understanding-speedup-in-plinq.md)」を参照してください。 クエリに含まれる要素の順序を保持する方法の詳細については、「[方法: PLINQ クエリの順序を制御する](how-to-control-ordering-in-a-plinq-query.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- [Parallel LINQ (PLINQ)](introduction-to-plinq.md)
