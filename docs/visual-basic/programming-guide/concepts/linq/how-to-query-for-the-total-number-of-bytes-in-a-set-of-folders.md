---
title: '方法: 一連のフォルダーの合計バイト数を照会する (LINQ)'
ms.date: 07/20/2015
ms.assetid: bfe85ed2-44dc-4ef1-aac7-241622b80a69
ms.openlocfilehash: c6490c8863b5762b0b487c6f3f3b2809e16d6519
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84397935"
---
# <a name="how-to-query-for-the-total-number-of-bytes-in-a-set-of-folders-linq-visual-basic"></a>方法: 一連のフォルダーの合計バイト数を照会する (LINQ) (Visual Basic)
この例では、指定したフォルダーとそのすべてのサブフォルダーに格納されている全ファイルの合計バイト数を取得する方法について説明します。  
  
## <a name="example"></a>例  
 <xref:System.Linq.Enumerable.Sum%2A> は、`select` 句で選択されたすべての項目の値を加算するメソッドです。 このクエリに少し変更を加え、<xref:System.Linq.Enumerable.Sum%2A> の代わりに <xref:System.Linq.Enumerable.Min%2A> メソッドまたは <xref:System.Linq.Enumerable.Max%2A> メソッドを呼び出せば、指定したディレクトリ ツリーの最大ファイルまたは最小ファイルを取得することができます。  
  
```vb  
Module QueryTotalBytes  
    Sub Main()  
  
        ' Change the drive\path if necessary.  
        Dim root As String = "C:\Program Files\Microsoft Visual Studio 9.0\VB"  
  
        'Take a snapshot of the folder contents.  
        ' This method assumes that the application has discovery permissions  
        ' for all folders under the specified path.  
        Dim fileList = My.Computer.FileSystem.GetFiles _  
                  (root, FileIO.SearchOption.SearchAllSubDirectories, "*.*")  
  
        Dim fileQuery = From file In fileList _  
                        Select GetFileLength(file)  
  
        ' Force execution and cache the results to avoid multiple trips to the file system.  
        Dim fileLengths = fileQuery.ToArray()  
  
        ' Find the largest file  
        Dim maxSize = Aggregate aFile In fileLengths Into Max()  
  
        ' Find the total number of bytes  
        Dim totalBytes = Aggregate aFile In fileLengths Into Sum()  
  
        Console.WriteLine("The largest file is " & maxSize & " bytes")  
        Console.WriteLine("There are " & totalBytes & " total bytes in " & _  
                          fileList.Count & " files under " & root)  
  
        ' Keep the console window open in debug mode  
        Console.WriteLine("Press any key to exit.")  
        Console.ReadKey()  
    End Sub  
  
    ' This method is used to catch the possible exception  
    ' that can be raised when accessing the FileInfo.Length property.  
    Function GetFileLength(ByVal filename As String) As Long  
        Dim retval As Long  
        Try  
            Dim fi As New System.IO.FileInfo(filename)  
            retval = fi.Length  
        Catch ex As System.IO.FileNotFoundException  
            ' If a file is no longer present,  
            ' just return zero bytes.
            retval = 0  
        End Try  
  
        Return retval  
    End Function  
End Module  
```  
  
 指定したディレクトリ ツリー内のバイト数をカウントするだけならば、LINQ クエリを作成せずに行う方が効率的です。LINQ クエリでは、データ ソースとしてリスト コレクションを作成する際のオーバーヘッドが発生します。 LINQ を使ったアプローチは、クエリが複雑化するか、同じデータ ソースに対して複数のクエリを実行する必要があるときに利便性が増します。  
  
 このクエリは、ファイルの長さを取得するために別のメソッドを呼び出しています。 その理由は、`GetFiles` の呼び出しで <xref:System.IO.FileInfo> オブジェクトが作成された後に別のスレッドでファイルが削除された場合に発生する可能性のある例外を処理するためです。 <xref:System.IO.FileInfo> オブジェクトの作成後であっても、例外は発生する可能性があります。<xref:System.IO.FileInfo> オブジェクトは、<xref:System.IO.FileInfo.Length%2A> プロパティが最初にアクセスされたときに最新の長さに基づいてそのプロパティを更新しようと試みるためです。 この操作をクエリの外側の try-catch ブロックに置くことで、"副作用の原因となりうるような操作はクエリ内では行わない" という原則に従っているのです。 一般に、アプリケーションが不明な状態に陥ることのないよう、例外を処理する際には十分な注意が必要です。  
  
## <a name="compile-the-code"></a>コードのコンパイル  
System.Linq 名前空間の `Imports` ステートメントを使用して、Visual Basic コンソール アプリケーション プロジェクトを作成します。
  
## <a name="see-also"></a>関連項目

- [LINQ to Objects (Visual Basic)](linq-to-objects.md)
- [LINQ とファイル ディレクトリ (Visual Basic)](linq-and-file-directories.md)
