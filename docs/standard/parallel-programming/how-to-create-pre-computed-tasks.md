---
title: '方法: 事前計算済みのタスクを作成する'
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- tasks, creating pre-computed
ms.assetid: a73eafa2-1f49-4106-a19e-997186029b58
ms.openlocfilehash: 88f0782380d21858bc5dd0fc0fbf63bbf85403b8
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84289994"
---
# <a name="how-to-create-pre-computed-tasks"></a>方法: 事前計算済みのタスクを作成する
このドキュメントでは、キャッシュに保持されている非同期ダウンロード操作の結果を取得する <xref:System.Threading.Tasks.Task.FromResult%2A?displayProperty=nameWithType> メソッドの使用方法について説明します。 <xref:System.Threading.Tasks.Task.FromResult%2A> メソッドは、<xref:System.Threading.Tasks.Task%601.Result%2A> プロパティとして指定された値を保持する、完成した <xref:System.Threading.Tasks.Task%601> オブジェクトを返します。 このメソッドは <xref:System.Threading.Tasks.Task%601> オブジェクトの結果があらかじめ計算されている <xref:System.Threading.Tasks.Task%601> オブジェクトを返す、非同期操作を実行する場合に便利です。  
  
## <a name="example"></a>例  
 次の例では、Web から文字列をダウンロードします。 これは `DownloadStringAsync` を定義します。 このメソッドでは、Web から非同期的に文字列をダウンロードします。 また、この例では <xref:System.Collections.Concurrent.ConcurrentDictionary%602> オブジェクトを使用して、前の操作の結果をキャッチします。 入力アドレスがこのキャッシュに保持されている場合、`DownloadStringAsync` では <xref:System.Threading.Tasks.Task.FromResult%2A> メソッドを使用して、そのアドレスでコンテンツを保持する <xref:System.Threading.Tasks.Task%601> オブジェクトを生成します。 それ以外の場合、`DownloadStringAsync` では Web からファイルをダウンロードし、結果をキャッシュに追加します。  
  
 [!code-csharp[TPL_CachedDownloads#1](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_cacheddownloads/cs/cacheddownloads.cs#1)]
 [!code-vb[TPL_CachedDownloads#1](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_cacheddownloads/vb/cacheddownloads.vb#1)]  
  
 この例では、複数の文字列を 2 回ダウンロードするために必要な時間を計算します。 結果がキャッシュに保持されているため、ダウンロード操作の 2 番目のセットにかかる時間は最初のセットより短くなります。 <xref:System.Threading.Tasks.Task.FromResult%2A> メソッドを使用することで、`DownloadStringAsync` メソッドでこれらの事前計算済みの結果を保持する <xref:System.Threading.Tasks.Task%601> オブジェクトを作成することができます。  
  
## <a name="see-also"></a>参照

- [タスク ベースの非同期プログラミング](task-based-asynchronous-programming.md)
