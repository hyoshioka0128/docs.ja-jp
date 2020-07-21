---
title: マネージド スレッド処理の基本
description: 例外、データの同期、フォアグラウンド スレッドとバックグラウンド スレッド、ローカル ストレージなど、マネージド スレッド処理に関する他の記事へのリンクを示します。
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- multiple threads
- threading [.NET Framework], multiple threads
- threading [.NET Framework], about threading
- managed threading
ms.assetid: b2944911-0e8f-427d-a8bb-077550618935
ms.openlocfilehash: d4a4ceabf29bd0f6f537e59ba477f9da686b1ef5
ms.sourcegitcommit: 5fd4696a3e5791b2a8c449ccffda87f2cc2d4894
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2020
ms.locfileid: "84769094"
---
# <a name="managed-threading-basics"></a>マネージド スレッド処理の基本

このセクションの最初の 5 つのトピックは、マネージド スレッド処理を使用するタイミングを判断するのに役立つように設計されており、また、いくつかの基本的な機能について説明するためのものです。 その他の機能を提供するクラスについては、「[スレッド処理オブジェクトと機能](threading-objects-and-features.md)」と「[同期プリミティブの概要](overview-of-synchronization-primitives.md)」を参照してください。  
  
 このセクションの残りのトピックには、マネージド スレッド処理と Windows オペレーティング システムとの相互作用など、高度なトピックが含まれます。  
  
> [!NOTE]
> .NET Framework 4 では、タスク並列ライブラリと PLINQ によって、マルチスレッド プログラムでのタスクとデータの並列処理のための API が提供されます。 詳細については、[並列プログラミング](../parallel-programming/index.md)に関するページをご覧ください。  
  
## <a name="in-this-section"></a>このセクションの内容

 [スレッドおよびスレッド処理](threads-and-threading.md)  
 複数のスレッドの利点と欠点について説明し、スレッドを作成またはスレッド プール スレッドを使用する可能性のあるシナリオの概要を示します。  
  
 [マネージド スレッドの例外](exceptions-in-managed-threads.md)  
 さまざまなバージョンの .NET Framework のスレッドでのハンドルされていない例外の動作、特に、アプリケーションの終了の原因となる状況について説明します。  
  
 [マルチスレッド処理のためのデータの同期](synchronizing-data-for-multithreading.md)  
 複数のスレッドで使用されるクラスのデータを同期する方法について説明します。  
  
 [フォアグラウンド スレッドとバックグラウンド スレッド](foreground-and-background-threads.md)  
 フォアグラウンド スレッドとバック グラウンド スレッドの違いについて説明します。  
  
 [Windows でのマネージド スレッド処理とアンマネージド スレッド処理](managed-and-unmanaged-threading-in-windows.md)  
 マネージド スレッド処理とアンマネージド スレッド処理の関係について説明し、Windows のスレッド処理 API に相当するマネージド API をリストし、COM アパートメントとマネージド スレッドの相互作用について説明します。  
  
 [スレッド ローカル ストレージ:スレッド相対静的フィールドとデータ スロット](thread-local-storage-thread-relative-static-fields-and-data-slots.md)  
 スレッド相対ストレージ メカニズムについて説明します。  
  
## <a name="reference"></a>関連項目

 <xref:System.Threading.Thread>  
 **Thread** クラスのリファレンス ドキュメントです。このクラスは、アンマネージド コードから作成されたか、マネージド アプリケーションで作成されたかにかかわらず、マネージド スレッドを表します。  
  
 <xref:System.ComponentModel.BackgroundWorker>  
 ユーザー インターフェイス オブジェクトと共にマルチスレッドを実装するための安全な方法を提供します。  
  
## <a name="related-sections"></a>関連項目

 [同期プリミティブの概要](overview-of-synchronization-primitives.md)  
 複数のスレッドのアクティビティを同期するために使用されるマネージド クラスについて説明します。  
  
 [マネージド スレッド処理の実施](managed-threading-best-practices.md)  
 マルチスレッドに関する一般的な問題と、問題を回避するための方法について説明します。  
  
 [並列プログラミング](../parallel-programming/index.md)  
 非同期およびマルチスレッドの .NET Framework アプリケーションを作成する作業を大幅に簡素化する、タスク並列ライブラリと PLINQ について説明します。
