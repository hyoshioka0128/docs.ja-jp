---
title: '方法: 並列タスクでバイナリ ツリーを走査する'
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- tasks, how to traverse a tree
ms.assetid: 4265d169-6c69-4f36-b10d-b7ae7f72f4df
ms.openlocfilehash: 5ac81a61691ec20daafc9e18978ba5814a150383
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84288070"
---
# <a name="how-to-traverse-a-binary-tree-with-parallel-tasks"></a>方法: 並列タスクでバイナリ ツリーを走査する
次の例では、ツリー データ構造を走査する並列タスクを使用する 2 つの方法を示します。 ツリー自体の作成は、演習として残しておきます。  
  
## <a name="example"></a>例  
 [!code-csharp[TPL#16](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl/cs/tpl.cs#16)]
 [!code-vb[TPL#16](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl/vb/treewalk.vb#16)]  
  
 示した 2 つのメソッドは、機能的に同等です。 タスクを作成して実行するために、<xref:System.Threading.Tasks.TaskFactory.StartNew%2A> メソッドを使用すると、タスクで待機し、例外を処理するために使用するタスクからハンドルを戻すことができます。  
  
## <a name="see-also"></a>参照

- [タスク並列ライブラリ (TPL)](task-parallel-library-tpl.md)
