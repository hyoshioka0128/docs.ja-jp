---
title: '方法: 文字列での単語の出現回数をカウントする (LINQ)'
ms.date: 07/20/2015
ms.assetid: bc367e46-f7cc-45f9-936f-754e661b7bb9
ms.openlocfilehash: c6894359e5785419ccf8f283f976c0a897288a5d
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84405327"
---
# <a name="how-to-count-occurrences-of-a-word-in-a-string-linq-visual-basic"></a>方法: 文字列での単語の出現回数をカウントする (LINQ) (Visual Basic)

この例では、LINQ クエリを使用して、指定された単語が文字列内に出現する回数をカウントする方法を示します。 カウントを実行するには、まず <xref:System.String.Split%2A> メソッドを呼び出して単語の配列を作成します。 <xref:System.String.Split%2A> メソッドを呼び出すと、パフォーマンスが低下します。 文字列に対する操作が単語のカウントのみである場合は、<xref:System.Text.RegularExpressions.Regex.Matches%2A> または <xref:System.String.IndexOf%2A> メソッドの使用を検討してください。 ただし、パフォーマンスが重要でない場合や、他の種類のクエリを実行する目的で事前に文章を分割している場合は、LINQ を使用して単語や語句をカウントすることにも意味があります。

## <a name="example"></a>例

```vb
Class CountWords

    Shared Sub Main()

        Dim text As String = "Historically, the world of data and the world of objects" &
                  " have not been well integrated. Programmers work in C# or Visual Basic" &
                  " and also in SQL or XQuery. On the one side are concepts such as classes," &
                  " objects, fields, inheritance, and .NET Framework APIs. On the other side" &
                  " are tables, columns, rows, nodes, and separate languages for dealing with" &
                  " them. Data types often require translation between the two worlds; there are" &
                  " different standard functions. Because the object world has no notion of query, a" &
                  " query can only be represented as a string without compile-time type checking or" &
                  " IntelliSense support in the IDE. Transferring data from SQL tables or XML trees to" &
                  " objects in memory is often tedious and error-prone."

        Dim searchTerm As String = "data"

        ' Convert the string into an array of words.
        Dim dataSource As String() = text.Split(New Char() {" ", ",", ".", ";", ":"},
                                                 StringSplitOptions.RemoveEmptyEntries)

        ' Create and execute the query. It executes immediately
        ' because a singleton value is produced.
        ' Use ToLower to match "data" and "Data"
        Dim matchQuery = From word In dataSource
                      Where word.ToLowerInvariant() = searchTerm.ToLowerInvariant()
                      Select word

        ' Count the matches.
        Dim count As Integer = matchQuery.Count()
        Console.WriteLine(count & " occurrence(s) of the search term """ &
                          searchTerm & """ were found.")

        ' Keep console window open in debug mode.
        Console.WriteLine("Press any key to exit.")
        Console.ReadKey()
    End Sub
End Class
' Output:
' 3 occurrence(s) of the search term "data" were found.
```

## <a name="compile-the-code"></a>コードのコンパイル

System.Linq 名前空間の `Imports` ステートメントを使用して、Visual Basic コンソール アプリケーション プロジェクトを作成します。

## <a name="see-also"></a>関連項目

- [LINQ と文字列 (Visual Basic)](linq-and-strings.md)
