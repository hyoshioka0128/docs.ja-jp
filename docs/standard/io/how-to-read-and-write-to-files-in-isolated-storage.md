---
title: '方法 : 分離ストレージ内でファイルの読み取りと書き込みを行う'
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- files, isolated storage
- reading data
- storing data using isolated storage, reading and writing to files
- writing to files within store
- data storage using isolated storage, reading and writing to files
- reading files within store
- isolated storage, reading and writing to files
- data stores, reading and writing to files
- stores, reading and writing to files
ms.assetid: f977ebdc-1b55-475a-bc3d-3376470b08ae
ms.openlocfilehash: d0c95f418ff85654dceed296b7a891c025ab2e62
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84291800"
---
# <a name="how-to-read-and-write-to-files-in-isolated-storage"></a>方法 : 分離ストレージ内でファイルの読み取りと書き込みを行う
分離ストアのファイルを読み取ったり、それに書き込んだりするには、ストリーム リーダー (<xref:System.IO.StreamReader> オブジェクト) またはストリーム ライター (<xref:System.IO.StreamWriter> オブジェクト) で <xref:System.IO.IsolatedStorage.IsolatedStorageFileStream> オブジェクトを使用します。  
  
## <a name="example"></a>例  
 次のコード例では、分離ストアを取得し、ストア内に TestStore.txt をという名前のファイルが存在するかどうかが確認されます。 存在しない場合、ファイルが作成され、"Hello Isolated Storage" とファイルに書き込まれます。 TestStore.txt が既に存在する場合、コード例は、ファイルから読み取られます。  
  
 [!code-csharp[Conceptual.IsolatedStorage#5](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.isolatedstorage/cs/source5.cs#5)]
 [!code-vb[Conceptual.IsolatedStorage#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.isolatedstorage/vb/source5.vb#5)]  
  
## <a name="see-also"></a>参照

- <xref:System.IO.IsolatedStorage.IsolatedStorageFile>
- <xref:System.IO.IsolatedStorage.IsolatedStorageFileStream>
- <xref:System.IO.FileMode?displayProperty=nameWithType>
- <xref:System.IO.FileAccess?displayProperty=nameWithType>
- <xref:System.IO.StreamReader?displayProperty=nameWithType>
- <xref:System.IO.StreamWriter?displayProperty=nameWithType>
- [ファイルおよびストリーム入出力](index.md)
- [分離ストレージ](isolated-storage.md)
