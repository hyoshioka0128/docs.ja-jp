---
title: '方法: 特定のパターンに一致するファイルを検索する'
ms.date: 07/20/2015
helpviewer_keywords:
- files [Visual Basic], finding
- pattern matching
- patterns, matching
ms.assetid: 25e3b71d-b844-4293-9e4e-f06c5836b5cc
ms.openlocfilehash: 71073672ed14cb2d5df5b5365266b718c59cb18f
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84401642"
---
# <a name="how-to-find-files-with-a-specific-pattern-in-visual-basic"></a>方法: 特定のパターンに一致するファイルを検索する (Visual Basic)

<xref:Microsoft.VisualBasic.MyServices.FileSystemProxy.GetFiles%2A> メソッドは、ファイルのパス名を表す文字列の読み取り専用のコレクションを返します。 `wildCards` パラメーターを使用して、特定のパターンを指定できます。 サブディレクトリを検索対象に含めるには、`searchType` パラメーターを `SearchOption.SearchAllSubDirectories` に設定します。  
  
 指定したパターンに一致するファイルがない場合は、空のコレクションが返されます。  
  
> [!NOTE]
> `System.IO` 名前空間の `DirectoryInfo` クラスを使用してファイルの一覧を返す方法については、「<xref:System.IO.DirectoryInfo.GetFiles%2A>」を参照してください。  
  
### <a name="to-find-files-with-a-specified-pattern"></a>特定のパターンに一致するファイルを検索するには  
  
- 検索するディレクトリの名前とパス、およびパターンを指定して、`GetFiles` メソッドを使用します。 次の例では、ディレクトリ内にある拡張子が `.dll` のファイルがすべて返され、`ListBox1` に追加されます。  
  
     [!code-vb[VbFileIOMisc#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbFileIOMisc/VB/Class1.vb#4)]  
  
## <a name="net-framework-security"></a>.NET Framework のセキュリティ  

 次の条件を満たす場合は、例外が発生する可能性があります。  
  
- パスが正しくない。長さが 0 の文字列である、空白だけが含まれている、使用できない文字が含まれている、デバイス パスである (先頭が \\\\.\\)、のいずれかの理由が考えられる (<xref:System.ArgumentException>)。  
  
- パスが `Nothing` であるため、有効でない (<xref:System.ArgumentNullException>)  
  
- `directory` が存在しない (<xref:System.IO.DirectoryNotFoundException>)。  
  
- `directory` が既存のファイルを指している (<xref:System.IO.IOException>)。  
  
- パスがシステムで定義されている最大長を超えている (<xref:System.IO.PathTooLongException>)。  
  
- パス内のファイル名またはフォルダー名にコロン (:) が含まれている、または形式が無効である (<xref:System.NotSupportedException>)。  
  
- ユーザーがパスを参照するのに必要なアクセス許可がない (<xref:System.Security.SecurityException>)  
  
- ユーザーに必要な権限がない (<xref:System.UnauthorizedAccessException>)。  
  
## <a name="see-also"></a>参照

- <xref:Microsoft.VisualBasic.MyServices.FileSystemProxy.GetFiles%2A>
- [方法: 特定のパターンに一致するサブディレクトリを検索する](how-to-find-subdirectories-with-a-specific-pattern.md)
- [トラブルシューティング : テキスト ファイルの読み取りと書き込み](troubleshooting-reading-from-and-writing-to-text-files.md)
- [方法: ディレクトリにあるファイルのコレクションを取得する](how-to-get-the-collection-of-files-in-a-directory.md)
