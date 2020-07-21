---
title: foreach を使用して BlockingCollection 内の項目を削除する
ms.date: 05/04/2020
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- thread-safe collections, how to enumerate blocking collection
ms.assetid: 2096103c-22f7-420d-b631-f102bc33a6dd
ms.openlocfilehash: 46638d2cd8078fefebc0eacc4b8f7798ffe178ff
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84288902"
---
# <a name="use-foreach-to-remove-items-in-a-blockingcollection"></a>foreach を使用して BlockingCollection 内の項目を削除する

<xref:System.Collections.Concurrent.BlockingCollection%601.Take%2A> と <xref:System.Collections.Concurrent.BlockingCollection%601.TryTake%2A> メソッドを使用して <xref:System.Collections.Concurrent.BlockingCollection%601> から項目を取得するだけでなく、<xref:System.Collections.Concurrent.BlockingCollection%601.GetConsumingEnumerable%2A?displayProperty=nameWithType> の [foreach](../../../csharp/language-reference/keywords/foreach-in.md) (Visual Basic では [For Each](../../../visual-basic/language-reference/statements/for-each-next-statement.md)) を使用して、追加が完了してコレクションが空になるまで項目を削除することもできます。 これは、通常の `foreach` (`For Each`) ループとは異なり、この列挙子が項目を削除することでソース コレクションを変更するので、*変更列挙*または*消費列挙*と呼ばれます。

## <a name="example"></a>例

次の例は、`foreach` (`For Each`) ループを使用して、<xref:System.Collections.Concurrent.BlockingCollection%601> 内のすべての項目を削除する方法を示しています。

[!code-csharp[CDS_BlockingCollection#03](../../../../samples/snippets/csharp/VS_Snippets_Misc/cds_blockingcollection/cs/example03.cs#03)]
[!code-vb[CDS_BlockingCollection#03](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/cds_blockingcollection/vb/enumeratebc.vb#03)]

この例では、消費スレッドの <xref:System.Collections.Concurrent.BlockingCollection%601.GetConsumingEnumerable%2A?displayProperty=nameWithType> メソッドで `foreach` ループを使用します。各項目は列挙されるとコレクションから削除されます。 <xref:System.Collections.Concurrent.BlockingCollection%601?displayProperty=nameWithType> はコレクション内の項目の最大数を制限します。 この方法でコレクションを列挙すると、使用できる項目がない場合、またはコレクションが空の場合は、コンシューマー スレッドがブロックされます。 この例では、プロデューサー スレッドによる項目の追加の方が項目の消費より高速なので、ブロックは問題になりません。

<xref:System.Collections.Concurrent.BlockingCollection%601.GetConsumingEnumerable%2A?displayProperty=nameWithType> は `IEnumerable<T>` を返します。そのため、順序を保証することはできません。 ただし、内部的には、<xref:System.Collections.Concurrent.ConcurrentQueue%601?displayProperty=nameWithType> が基になるコレクション型として使用されます。オブジェクトは、先入れ先出し (FIFO) 順序に従ってデキューされます。 <xref:System.Collections.Concurrent.BlockingCollection%601.GetConsumingEnumerable%2A?displayProperty=nameWithType> の同時呼び出しが行われると、競合が発生します。 1 つの列挙で使用 (デキュー) された 1 つの項目をもう一方で見ることはできません。

コレクションを変更せずに列挙するには、<xref:System.Collections.Concurrent.BlockingCollection%601.GetConsumingEnumerable%2A> メソッドを使用せずに `foreach` (`For Each`) のみを使用します。 ただし、この種の列挙は特定時点のコレクションのスナップショットを表すことを理解しておくことが重要です。 ループの実行中に同時に他のスレッドが項目を追加または削除する場合、ループはコレクションの実際の状態を表さない可能性があります。

## <a name="see-also"></a>関連項目

- <xref:System.Collections.Concurrent?displayProperty=nameWithType>
- [並列プログラミング](../../parallel-programming/index.md)
