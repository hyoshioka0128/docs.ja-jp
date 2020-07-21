---
title: '方法: ディレクトリをコピーする'
description: 別の場所にディレクトリの内容を同期的にコピーする I/O クラスを使用してディレクトリをコピーする方法を参照します。
ms.date: 12/27/2018
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- directory copying
- I/O [.NET Framework], copying directories
- subdirectory copying
- copying directories
- directories [.NET Framework], copying
ms.assetid: 5a969765-e5f8-4b4e-977e-90e2b0a1fe3c
ms.openlocfilehash: 65fe28c90a6cd6f0b3c8c32da19c1d9603900670
ms.sourcegitcommit: 7137e12f54c4e83a94ae43ec320f8cf59c1772ea
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/10/2020
ms.locfileid: "84662590"
---
# <a name="how-to-copy-directories"></a>方法: ディレクトリをコピーする
このトピックでは、I/O クラスを使用して、別の場所にディレクトリの内容を同期的にコピーする方法について説明します。

ファイルを非同期的にコピーする例については、「[非同期ファイル I/O](asynchronous-file-i-o.md)」を参照してください。

この例では、`DirectoryCopy` メソッドの `copySubDirs` を `true` に設定することでサブディレクトリをコピーします。 `DirectoryCopy` メソッドは各サブディレクトリでそれ自体を呼び出すことで、コピーするサブディレクトリがなくなるまでサブディレクトリを再帰的にコピーします。  
  
## <a name="example"></a>例  
 [!code-csharp[System.IO.Directory_Copy#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.IO.Directory_Copy/cs/program.cs#1)]
 [!code-vb[System.IO.Directory_Copy#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.IO.Directory_Copy/vb/Program.vb#1)]  
  
[!INCLUDE [localized code comments](../../../includes/code-comments-loc.md)]

## <a name="see-also"></a>関連項目

- <xref:System.IO.FileInfo>
- <xref:System.IO.DirectoryInfo>
- <xref:System.IO.FileStream>
- [ファイルおよびストリーム入出力](index.md)
- [共通 I/O タスク](common-i-o-tasks.md)
- [非同期ファイル I/O](asynchronous-file-i-o.md)
