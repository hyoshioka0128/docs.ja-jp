---
title: '方法: 境界ブロッキング機能をコレクションに追加する'
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- thread-safe collections, custom blocking collections
ms.assetid: 4c2492de-3876-4873-b5a1-000bb404d770
ms.openlocfilehash: 57a01726e897f4ddbf8df5ede53609c198012d80
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84287875"
---
# <a name="how-to-add-bounding-and-blocking-functionality-to-a-collection"></a>方法: 境界ブロッキング機能をコレクションに追加する
この例では、<xref:System.Collections.Concurrent.IProducerConsumerCollection%601?displayProperty=nameWithType> インターフェイスをクラスに実装し、クラスのインスタンスを <xref:System.Collections.Concurrent.BlockingCollection%601?displayProperty=nameWithType> の内部ストレージ メカニズムとして使用することによって、カスタム コレクション クラスに境界ブロッキング機能を追加する方法を示します。 境界ブロッキングの詳細については、「[BlockingCollection の概要](blockingcollection-overview.md)」を参照してください。  
  
## <a name="example"></a>例  
 カスタム コレクション クラスは基本優先度キューであり、優先度レベルは <xref:System.Collections.Concurrent.ConcurrentQueue%601?displayProperty=nameWithType> オブジェクトの配列として表されます。 各キュー内で他の順序付けは行われません。  
  
 クライアント コードでは、3 つのタスクが開始されます。 1 番目のタスクはキーボード入力のポーリングだけを行い、実行中にいつでもキャンセルできるようにします。 2 番目のタスクはプロデューサー スレッドであり、ブロッキング コレクションに新しい項目を追加し、ランダムな値に基づく優先度を各項目に割り当てます。 3 番目のタスクは、利用可能になった項目をコレクションから削除します。  
  
 1 つのスレッドが他より速く実行されるようにすることで、アプリケーションの動作を調整できます。 プロデューサーが高速に実行されると、コンストラクターで指定されている数の項目がコレクションに既に含まれる場合はブロッキング コレクションが項目の追加を防ぐので、境界機能が目立つようになります。 コンシューマーが高速に実行されると、コンシューマーは新しい項目が追加されるのを待機するので、ブロッキング機能が目立つようになります。  
  
 [!code-csharp[CDS_BlockingCollection#06](../../../../samples/snippets/csharp/VS_Snippets_Misc/cds_blockingcollection/cs/prodcon.cs#06)]  
  
 既定では、<xref:System.Collections.Concurrent.BlockingCollection%601?displayProperty=nameWithType> の記憶域は <xref:System.Collections.Concurrent.ConcurrentQueue%601?displayProperty=nameWithType> です。  
  
## <a name="see-also"></a>参照

- [スレッドセーフなコレクション](index.md)
