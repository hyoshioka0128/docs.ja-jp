---
title: '方法 : 分離ストレージでファイルおよびディレクトリを削除する'
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- data storage using isolated storage, deleting files and directories
- directories [.NET Framework], isolated storage
- files [.NET Framework], isolated storage
- isolated storage, deleting files and directories
- data stores, deleting files and directories
- stores, creating files and directories
- deleting files within isolated stage file
- storing data using isolated storage, deleting files and directories
- deleting directories within isolated stage file
ms.assetid: 8fcc0dea-435b-4d40-ba4d-ba056265c202
ms.openlocfilehash: dc84fefbde1177993b17e9ec687a1ef759b74735
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84291904"
---
# <a name="how-to-delete-files-and-directories-in-isolated-storage"></a>方法 : 分離ストレージでファイルおよびディレクトリを削除する
分離ストレージ ファイル内のディレクトリとファイルを削除することができます。 ストア内では、ファイル名とディレクトリ名はオペレーティング システムに依存し、仮想ファイル システムのルートに対して相対的に指定されます。 Windows オペレーティング システムでは大文字小文字は区別されません。  
  
 <xref:System.IO.IsolatedStorage.IsolatedStorageFile?displayProperty=nameWithType> クラスには、<xref:System.IO.IsolatedStorage.IsolatedStorageFile.DeleteDirectory%2A> と <xref:System.IO.IsolatedStorage.IsolatedStorageFile.DeleteFile%2A> のディレクトリおよびファイルを削除するメソッドが 2 つあります。 存在しないファイルまたはディレクトリを削除しようとする場合、<xref:System.IO.IsolatedStorage.IsolatedStorageException> の例外がスローされます。 名前にワイルドカード文字を含める場合、<xref:System.IO.IsolatedStorage.IsolatedStorageFile.DeleteDirectory%2A> は <xref:System.IO.IsolatedStorage.IsolatedStorageException> の例外をスローし、<xref:System.IO.IsolatedStorage.IsolatedStorageFile.DeleteFile%2A> は <xref:System.ArgumentException> の例外をスローします。  
  
 ディレクトリにファイルまたはサブディレクトリが含まれている場合、<xref:System.IO.IsolatedStorage.IsolatedStorageFile.DeleteDirectory%2A> メソッドは失敗します。 <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetFileNames%2A> と <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetDirectoryNames%2A> のメソッドを使用すると、既存のファイルとディレクトリを取得することができます。 ストアの仮想ファイル システムを検索する方法の詳細については、「[方法 : 分離ストレージ内でファイルおよびディレクトリを検索する](how-to-find-existing-files-and-directories-in-isolated-storage.md)」を参照してください。  
  
## <a name="example"></a>例  
 次のコード例は、いくつかのディレクトリとファイルを作成して削除します。  
  
 [!code-cpp[Conceptual.IsolatedStorage#4](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.isolatedstorage/cpp/source4.cpp#4)]
 [!code-csharp[Conceptual.IsolatedStorage#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.isolatedstorage/cs/source4.cs#4)]
 [!code-vb[Conceptual.IsolatedStorage#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.isolatedstorage/vb/source4.vb#4)]  
  
## <a name="see-also"></a>参照

- <xref:System.IO.IsolatedStorage.IsolatedStorageFile?displayProperty=nameWithType>
- [分離ストレージ](isolated-storage.md)
