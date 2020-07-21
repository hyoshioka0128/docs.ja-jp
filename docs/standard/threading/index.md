---
title: マネージド スレッド処理
description: 基本、ベスト プラクティス、スレッド オブジェクトと機能、リファレンス ページなどについては、.NET でのマネージ スレッド処理に関する記事へのリンクをご覧ください。
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- threading [.NET Framework], about threading
- managed threading
ms.assetid: 7b46a7d9-c6f1-46d1-a947-ae97471bba87
ms.openlocfilehash: 570db45138c85c4252967404da4404d434660d69
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84599751"
---
# <a name="managed-threading"></a>マネージド スレッド処理
アプリケーションを開発する場合、対象のコンピューターがプロセッサがシングルまたはマルチのいずれの場合でも、アプリケーションにユーザーとの迅速な対話を提供する必要があります。これはアプリケーションがほかの処理の実行中であっても同じことです。 アプリケーションによるユーザーへの迅速な応答を維持すると同時に、ユーザー イベントの合間やその処理中にプロセッサを使用する最も強力な方法は、複数の実行スレッドを使用することです。 ここでは、スレッド処理の基本概念について、マネージド スレッド処理の概念と使用方法を中心に説明します。  
  
> [!NOTE]
> .NET Framework 4 以降では、<xref:System.Threading.Tasks.Parallel?displayProperty=nameWithType> クラスおよび <xref:System.Threading.Tasks.Task?displayProperty=nameWithType> クラス、[Parallel LINQ (PLINQ)](../parallel-programming/introduction-to-plinq.md)、<xref:System.Collections.Concurrent?displayProperty=nameWithType> 名前空間の新しい同時実行コレクション クラス、スレッドではなくタスクの概念を基にした新しいプログラミング モデルにより、マルチスレッド プログラミングが大幅に簡略化されています。 詳細については、[並列プログラミング](../parallel-programming/index.md)に関するページをご覧ください。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [マネージド スレッド処理の基本](managed-threading-basics.md)  
 マネージド スレッド処理の概要と、マルチ スレッドをどのようなときに使用するかについて説明します。  
  
 [スレッドの使用とスレッド処理](using-threads-and-threading.md)  
 スレッドの作成、開始、一時停止、再開、および中止について説明します。  
  
 [マネージド スレッド処理の実施](managed-threading-best-practices.md)  
 同期のレベル、デッドロックと競合状態の回避方法、およびその他のスレッド処理に関する問題について説明します。  
  
 [スレッド処理オブジェクトと機能](threading-objects-and-features.md)  
 スレッドの動作や、別のスレッドによってアクセスされるオブジェクトのデータを同期するために使用するマネージド クラスについて説明し、スレッド プールのスレッドの概要を示します。  
  
## <a name="reference"></a>関連項目  
 <xref:System.Threading>  
 マネージド スレッドを使用したり同期したりするためのクラスを含みます。  
  
 <xref:System.Collections.Concurrent>  
 複数のスレッドで使用する安全なコレクション クラスを含みます。  
  
 <xref:System.Threading.Tasks>  
 同時処理タスクを作成およびスケジュールするためのクラスを含みます。  
  
## <a name="related-sections"></a>関連項目  
 [アプリケーション ドメイン](../../framework/app-domains/application-domains.md)  
 アプリケーション ドメインと、その共通言語インフラストラクチャでの使用に関する概要を示します。  
  
 [非同期ファイル I/O](../io/asynchronous-file-i-o.md)  
 非同期 I/O のパフォーマンス上の利点と基本的な操作について説明します。  
  
 [タスク ベースの非同期パターン (TAP)](../asynchronous-programming-patterns/task-based-asynchronous-pattern-tap.md)  
 .NET での非同期プログラミングの推奨パターンの概要を示します。  
  
 [同期メソッドの非同期呼び出し](../asynchronous-programming-patterns/calling-synchronous-methods-asynchronously.md)  
 デリゲートの組み込み機能を使用してスレッド プールのスレッドでメソッドを呼び出す方法を示します。  
  
 [並列プログラミング](../parallel-programming/index.md)  
 アプリケーションで複数のスレッドを簡単に使用できるようにする並列プログラミング ライブラリについて説明します。  
  
 [Parallel LINQ (PLINQ)](../parallel-programming/introduction-to-plinq.md)  
 複数のプロセッサを利用するために、クエリを並列で実行するシステムについて説明します。
