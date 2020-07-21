---
title: ディレクトリを作成する方法
ms.date: 07/20/2015
helpviewer_keywords:
- directories [Visual Basic], creating
- folders [Visual Basic], creating
ms.assetid: 0351a2ca-24d8-43b5-bb39-9b99e6401cff
ms.openlocfilehash: 0da915054a2e38c778f15bc0b472fe9b02521189
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84401668"
---
# <a name="how-to-create-a-directory-in-visual-basic"></a>方法 : Visual Basic でディレクトリを作成する

ディレクトリを作成するには、`My.Computer.FileSystem` オブジェクトの `CreateDirectory` メソッドを使用します。  
  
 ディレクトリが既にある場合、例外はスローされません。  
  
### <a name="to-create-a-directory"></a>ディレクトリを作成するには  
  
- ディレクトリを作成する場所を完全にパスに指定して、`CreateDirectory` メソッドを使用します。 この例では、`C:\Documents and Settings\All Users\Documents` に `NewDirectory` ディレクトリを作成します。  
  
     [!code-vb[VbVbcnMyFileSystem#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnMyFileSystem/VB/Class1.vb#2)]  
  
## <a name="robust-programming"></a>信頼性の高いプログラミング  

 次の条件を満たす場合は、例外が発生する可能性があります。  
  
- ディレクトリ名が不正な場合。 たとえば、不正な文字が含まれている場合や、空白だけの場合などです (<xref:System.ArgumentException>)。  
  
- 作成するディレクトリの親ディレクトリが読み取り専用である場合 (<xref:System.IO.IOException>)。  
  
- ディレクトリ名が `Nothing` の場合 (<xref:System.ArgumentNullException>)｡  
  
- ディレクトリ名が長すぎる場合 (<xref:System.IO.PathTooLongException>)｡  
  
- ディレクトリ名がコロン ":" の場合 (<xref:System.NotSupportedException>)｡  
  
- ユーザーがディレクトリを作成するアクセス許可を持っていない場合 (<xref:System.UnauthorizedAccessException>)。  
  
- 部分的に信頼されている状況でユーザーにアクセス許可がない場合 (<xref:System.Security.SecurityException>)。  
  
## <a name="see-also"></a>参照

- <xref:Microsoft.VisualBasic.FileIO.FileSystem.CreateDirectory%2A>
- [ファイルおよびディレクトリの作成、削除、および移動](creating-deleting-and-moving-files-and-directories.md)
