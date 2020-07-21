---
title: .NET ガベージ コレクション
description: .NET のガベージ コレクションについて説明します。 .NET のガベージ コレクターは、アプリケーションのメモリの割り当てと解放を管理します。
ms.date: 04/21/2020
ms.technology: dotnet-standard
helpviewer_keywords:
- memory, garbage collection
- garbage collection, automatic memory management
- GC [.NET Framework]
- memory, allocating
- common language runtime, garbage collection
- garbage collector
- cleanup operations
- garbage collection
- memory, releasing
- common language runtime, automatic memory management
- automatic memory management
- runtime, automatic memory management
- runtime, garbage collection
- garbage collection, about
ms.assetid: 22b6cb97-0c80-4eeb-a2cf-5ed7655e37f9
ms.openlocfilehash: dde0012ff7233eb7ee13efab1931f129b0eae276
ms.sourcegitcommit: 7137e12f54c4e83a94ae43ec320f8cf59c1772ea
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/10/2020
ms.locfileid: "84662486"
---
# <a name="garbage-collection"></a>ガベージ コレクション

.NET のガベージ コレクターは、アプリケーションのメモリの割り当てと解放を管理します。 新しいオブジェクトを生成するたびに、共通言語ランタイムは、マネージド ヒープからオブジェクトにメモリを割り当てます。 マネージド ヒープに使用可能なアドレス空間がある限り、ランタイムは新しいオブジェクト用に領域の割り当てを続けます。 しかし、メモリの大きさは無限ではありません。 最終的には、ガベージ コレクターが、一部のメモリを解放するためにガベージ コレクションを実行する必要があります。 コレクションの実行に最適な時期は、ガベージ コレクターの最適化エンジンが、割り当てられるオブジェクトの状況に応じて決定します。 コレクションを実行する場合、ガベージ コレクターは、アプリケーションによって使用されなくなったオブジェクトがマネージド ヒープにあるかどうかをチェックし、使われていないオブジェクトのメモリを再利用するために必要な操作を実行します。  
  
## <a name="in-this-section"></a>このセクションの内容
  
|Title|説明|  
|-----------|-----------------|  
|[ガベージ コレクションの基礎](fundamentals.md)|ガベージ コレクションの動作、マネージド ヒープに対するオブジェクトの割り当て方法、およびその他の主要な概念について説明します。|  
|[ワークステーションとサーバーのガベージ コレクション](workstation-server-gc.md)|ワークステーションのクライアント アプリ用ガベージ コレクションと、サーバーのサーバー アプリ用ガベージ コレクションの違いについて説明します。|
|[バックグラウンド ガベージ コレクション](background-gc.md)|バックグラウンド ガベージ コレクションについて説明します。これは、第 2 世代のコレクションを処理中の、第 0 世代と第 1 世代のオブジェクトのコレクションです。|
|[大きなオブジェクト ヒープ](large-object-heap.md)|大きなオブジェクト ヒープ (LOH) について、および大きなオブジェクトをガベージ コレクションする方法について説明します。|
|[ガベージ コレクションとパフォーマンス](performance.md)|ガベージ コレクションとパフォーマンスの問題を診断するために使用できるパフォーマンス チェックについて説明します。|  
|[発生したコレクション](induced.md)|ガベージ コレクションがどのように行われるかについて説明します。|  
|[待機モード](latency.md)|ガベージ コレクションの割り込みの動作を決定するモードについて説明します。|  
|[共有 Web ホストの最適化](optimization-for-shared-web-hosting.md)|複数の小規模な Web サイトで共有されているサーバーで、ガベージ コレクションを最適化する方法について説明します。|  
|[ガベージ コレクションの通知](notifications.md)|フル ガベージ コレクションが近づいたときと完了したときを検出する方法について説明します。|  
|[アプリケーション ドメインのリソース監視](app-domain-resource-monitoring.md)|アプリケーション ドメインによる CPU とメモリの使用状況を監視する方法について説明します。|  
|[弱い参照](weak-references.md)|アプリケーションからオブジェクトへのアクセスを許容したまま、そのオブジェクトをガベージ コレクターが収集できるようにする機能について説明します。|  
  
## <a name="reference"></a>関連項目

- <xref:System.GC?displayProperty=nameWithType>  
- <xref:System.GCCollectionMode?displayProperty=nameWithType>  
- <xref:System.GCNotificationStatus?displayProperty=nameWithType>  
- <xref:System.Runtime.GCLatencyMode?displayProperty=nameWithType>  
- <xref:System.Runtime.GCSettings?displayProperty=nameWithType>  
- <xref:System.Runtime.GCSettings.LargeObjectHeapCompactionMode%2A?displayProperty=nameWithType>  
- <xref:System.Object.Finalize%2A?displayProperty=nameWithType>  
- <xref:System.IDisposable?displayProperty=nameWithType>  
  
## <a name="see-also"></a>関連項目

- [アンマネージド リソースのクリーンアップ](unmanaged.md)
