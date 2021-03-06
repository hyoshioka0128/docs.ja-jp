---
title: スレッド処理オブジェクトと機能
ms.date: 10/01/2018
ms.technology: dotnet-standard
helpviewer_keywords:
- threading [.NET Framework], features
- managed threading
ms.assetid: 239b2e8d-581b-4ca3-992b-0e8525b9321c
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 9a355c2e996ddb00dad804dfeb22987923d91aa6
ms.sourcegitcommit: ccd8c36b0d74d99291d41aceb14cf98d74dc9d2b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/10/2018
ms.locfileid: "53144521"
---
# <a name="threading-objects-and-features"></a>スレッド処理オブジェクトと機能

.NET では、<xref:System.Threading.Thread?displayProperty=nameWithType> クラスの他に、マルチ スレッド アプリケーションを開発するのに役立つ複数のクラスが提供されます。 次の記事では、それらのクラスの概要を説明します。

|Title|説明|  
|-----------|-----------------|  
|[マネージド スレッド プール](the-managed-thread-pool.md)|.NET によって管理されるワーカー スレッドのプールを提供する <xref:System.Threading.ThreadPool?displayProperty=nameWithType> について説明します。|  
|[タイマー](timers.md)|マルチスレッド環境で使用できる .NET タイマーについて説明します。|
|[同期プリミティブの概要](overview-of-synchronization-primitives.md)|共有リソースへのアクセスを同期化する場合や、スレッドの相互作用を制御する場合に使用できる型について説明します。|
|[EventWaitHandle、AutoResetEvent、CountdownEvent、ManualResetEvent](eventwaithandle-autoresetevent-countdownevent-manualresetevent.md)|通知を行ったり通知を待機したりすることによりスレッドの活動を同期するために使用するマネージド イベント待機ハンドルについて説明します。|
|[ミューテックス](mutexes.md)|共有リソースへの排他アクセスを付与する <xref:System.Threading.Mutex?displayProperty=nameWithType> について説明します。|
|[Semaphore と SemaphoreSlim](semaphore-and-semaphoreslim.md)|共有リソースまたはリソースのプールに同時にアクセスできるスレッドの数を制限する <xref:System.Threading.Semaphore?displayProperty=nameWithType> について説明します。|
|[バリア](barrier.md)|段階的な操作におけるスレッドの調整のためのバリア パターンを実装する <xref:System.Threading.Barrier?displayProperty=nameWithType> クラスについて説明します。|
|[SpinLock](spinlock.md)|特定の下位レベルのシナリオで <xref:System.Threading.Monitor?displayProperty=nameWithType> ロックの代わりに軽量クラスとして使用できる <xref:System.Threading.SpinLock?displayProperty=nameWithType> 構造体について説明します。|
|[SpinWait](spinwait.md)|スピンベースの待機のサポートを提供する <xref:System.Threading.SpinWait?displayProperty=nameWithType> 構造体について説明します。|

## <a name="see-also"></a>関連項目

- <xref:System.Threading.Monitor?displayProperty=nameWithType>
- <xref:System.Threading.WaitHandle?displayProperty=nameWithType>
- <xref:System.ComponentModel.BackgroundWorker?displayProperty=nameWithType>
- <xref:System.Threading.Tasks.Parallel?displayProperty=nameWithType>
- <xref:System.Threading.Tasks.Task?displayProperty=nameWithType>
- [スレッドの使用とスレッド処理](using-threads-and-threading.md)
- [Asynchronous File I/O](../io/asynchronous-file-i-o.md)
- [並列プログラミング](../parallel-programming/index.md)
- [タスク並列ライブラリ (TPL)](../parallel-programming/task-parallel-library-tpl.md)
