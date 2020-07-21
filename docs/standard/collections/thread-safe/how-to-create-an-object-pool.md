---
title: ConcurrentBag を使用してオブジェクト プールを作成する
ms.date: 05/01/2020
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- object pool, in .NET Framework
ms.assetid: 0480e7ff-b6f9-480e-a889-2ed4264d8372
ms.openlocfilehash: 64d91162b27eba80fba63761d0a926e441b63440
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84287862"
---
# <a name="create-an-object-pool-by-using-a-concurrentbag"></a>ConcurrentBag を使用してオブジェクト プールを作成する

この例では、<xref:System.Collections.Concurrent.ConcurrentBag%601> を使用してオブジェクト プールを実装する方法を示します。 オブジェクト プールは、クラスの複数のインスタンスが必要であり、クラスの作成または破棄に大きなコストがかかる状況で、アプリケーションのパフォーマンスを向上させることができます。 クライアント プログラムが新しいオブジェクトを要求すると、オブジェクト プールは最初に既に作成されてプールに返されているオブジェクトを提供しようとします。 使用できるオブジェクトがない場合にのみ、新しいオブジェクトが作成されます。

<xref:System.Collections.Concurrent.ConcurrentBag%601> は、高速での挿入と削除をサポートしており、同じスレッドが項目の追加と削除の両方を行うときは特に高速であるため、オブジェクトの格納に使用されます。 この例は、<xref:System.Collections.Concurrent.IProducerConsumerCollection%601> を中心に構築するようにさらに拡張できます。これは、<xref:System.Collections.Concurrent.ConcurrentQueue%601> や <xref:System.Collections.Concurrent.ConcurrentStack%601> と同じようにバッグ データの構造を実装します。

> [!TIP]
> この記事では、オブジェクトを再利用できるよう格納しておくために、基になる同時実行型と共に、独自の実装のオブジェクト プールのを作成する方法を定義します。 ただし、<xref:Microsoft.Extensions.ObjectPool.ObjectPool%601?displayProperty=nameWithType> 型は <xref:Microsoft.Extensions.ObjectPool?displayProperty=fullName> 名前空間に既に存在します。 実装をご自分で作成する前に、多くの追加機能がある、利用可能な型を使用することを検討してください。

## <a name="example"></a>例

[!code-csharp[CDS#04](../../../../samples/snippets/csharp/VS_Snippets_Misc/cds/cs/objectpool.cs#04)]
[!code-vb[CDS#04](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/cds/vb/objectpool04.vb#04)]

## <a name="see-also"></a>関連項目

- [スレッドセーフなコレクション](index.md)
