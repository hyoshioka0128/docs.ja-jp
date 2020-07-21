---
title: '方法 : テキスト ファイルに追記する'
ms.date: 07/20/2015
helpviewer_keywords:
- I/O [Visual Basic], appending to files
- I/O [Visual Basic], My.Computer.FileSystem.WriteAllText method
- I/O [Visual Basic], WriteAllText method
ms.assetid: bbbd7fb5-f169-41a9-b53f-520ea9613913
ms.openlocfilehash: 53b2e4c9030e9d1dd81a4121ad3f92aad796e3e1
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84359956"
---
# <a name="how-to-append-to-text-files-in-visual-basic"></a>方法 : Visual Basic でテキスト ファイルに追記する

`append` パラメーターが `True` に設定されるように指定して、<xref:Microsoft.VisualBasic.FileIO.FileSystem.WriteAllText%2A> メソッドを使いテキスト ファイルに追加できます。  
  
### <a name="to-append-to-a-text-file"></a>テキスト ファイルに追加するには  
  
- `WriteAllText` メソッドを使って、ターゲット ファイルと追加する文字列を指定し、`append` パラメーターを `True` に設定します。  
  
     この例では、文字列 `"This is a test string."` を `Testfile.txt` という名前のファイルに書き込みます。  
  
     [!code-vb[VbFileIOWrite#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbFileIOWrite/VB/Class1.vb#6)]  
  
## <a name="robust-programming"></a>信頼性の高いプログラミング  

 次の条件を満たす場合は、例外が発生する可能性があります。  
  
- パスが正しくない。長さが 0 の文字列である、空白だけが含まれている、使用できない文字が含まれている、デバイス パスである (先頭が \\\\.\\)、のいずれかの理由が考えられる (<xref:System.ArgumentException>)。  
  
- パスが `Nothing` であるため、有効でない (<xref:System.ArgumentNullException>)  
  
- `File` が、存在しないパスを指している (<xref:System.IO.FileNotFoundException> または <xref:System.IO.DirectoryNotFoundException>)。  
  
- 他のプロセスがファイルを使用しているか、または I/O エラーが発生した (<xref:System.IO.IOException>)。  
  
- パスがシステムで定義されている最大長を超えている (<xref:System.IO.PathTooLongException>)。  
  
- パス内のファイル名またはディレクトリ名にコロン (:) が含まれているか、または形式が無効である (<xref:System.NotSupportedException>)  
  
- ユーザーがパスを参照するのに必要なアクセス許可がない (<xref:System.Security.SecurityException>)  
  
## <a name="see-also"></a>参照

- <xref:Microsoft.VisualBasic.FileIO.FileSystem.WriteAllText%2A>
- <xref:Microsoft.VisualBasic.FileIO.FileSystem>
- [ファイルへの書き込み](writing-to-files.md)
