---
title: '方法: カスタムの PLINQ 集約関数を記述する'
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- PLINQ queries, how to create aggregate function
ms.assetid: 5a70dd49-ab2a-4798-b551-196ee7042b1a
ms.openlocfilehash: 644d6b6f929e040a0fe688c18c774de6f434c4b3
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84290773"
---
# <a name="how-to-write-a-custom-plinq-aggregate-function"></a>方法: カスタムの PLINQ 集約関数を記述する
この例は、<xref:System.Linq.ParallelEnumerable.Aggregate%2A> メソッドを使用して、カスタム集計関数をソース シーケンスに適用する方法を示しています。  
  
> [!WARNING]
> この例は、使用方法を示すことを意図したものであるため、同等の順次的な LINQ to Objects クエリほど高速ではない可能性があります。 高速化の詳細については、「[PLINQ での高速化について](understanding-speedup-in-plinq.md)」を参照してください。  
  
## <a name="example"></a>例  
 次の例では、整数シーケンスの標準偏差を計算します。  
  
 [!code-csharp[PLINQ#31](../../../samples/snippets/csharp/VS_Snippets_Misc/plinq/cs/plinqsamples.cs#31)]
 [!code-vb[PLINQ#31](../../../samples/snippets/visualbasic/VS_Snippets_Misc/plinq/vb/plinqsnippets1.vb#31)]  
  
 この例では、PLINQ に固有の Aggregate 標準クエリ演算子のオーバーロードを使用します。 このオーバーロードでは、3 番目の入力パラメーターとして、追加の <xref:System.Func%603?displayProperty=nameWithType> を受け取ります。 このデリゲートは、集計結果で最終計算を実行する前に、すべてのスレッドからの結果を結合します。 この例では、すべてのスレッドからの合計をまとめます。  
  
 ラムダ式の本体が単一の式で構成されている場合、<xref:System.Func%602?displayProperty=nameWithType> デリゲートの戻り値は式の値になることに注意してください。  
  
## <a name="see-also"></a>参照

- <xref:System.Linq.ParallelEnumerable>
- [Parallel LINQ (PLINQ)](introduction-to-plinq.md)
