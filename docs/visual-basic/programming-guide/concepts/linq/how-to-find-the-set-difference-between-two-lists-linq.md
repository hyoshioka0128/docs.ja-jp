---
title: '方法: 2 つのリストの差集合を見つける (LINQ)'
ms.date: 07/20/2015
ms.assetid: b5b25474-10a8-4df6-aab5-75621bb6b68e
ms.openlocfilehash: f533b63b40325b34c5881c1e2f14aa4e576191c7
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84396598"
---
# <a name="how-to-find-the-set-difference-between-two-lists-linq-visual-basic"></a>方法: 2 つのリストの差集合を見つける (LINQ) (Visual Basic)
この例では、LINQ を使用して、2 つの文字列リストを比較し、names2.txt ではなく names1.txt でそれらの行を出力する方法を示します。  
  
### <a name="to-create-the-data-files"></a>データ ファイルを作成するには  
  
1. 「[方法:文字列コレクションを結合および比較する (LINQ) (Visual Basic)](how-to-combine-and-compare-string-collections-linq.md)」に示されているように、ソリューション フォルダーに names1.txt と names2.txt をコピーします。  
  
## <a name="example"></a>例  
  
```vb  
Class CompareLists  
  
    Shared Sub Main()  
  
        ' Create the IEnumerable data sources.  
        Dim names1 As String() = System.IO.File.ReadAllLines("../../../names1.txt")  
        Dim names2 As String() = System.IO.File.ReadAllLines("../../../names2.txt")  
  
        ' Create the query. Note that method syntax must be used here.  
        Dim differenceQuery = names1.Except(names2)  
        Console.WriteLine("The following lines are in names1.txt but not names2.txt")  
  
        ' Execute the query.  
        For Each name As String In differenceQuery  
            Console.WriteLine(name)  
        Next  
  
        ' Keep console window open in debug mode.  
        Console.WriteLine("Press any key to exit.")  
        Console.ReadKey()  
    End Sub  
End Class  
' Output:  
' The following lines are in names1.txt but not names2.txt  
' Potra, Cristina  
' Noriega, Fabricio  
' Aw, Kam Foo  
' Toyoshima, Tim  
' Guy, Wey Yuan  
' Garcia, Debra  
```  
  
 <xref:System.Linq.Enumerable.Except%2A>、<xref:System.Linq.Enumerable.Distinct%2A>、<xref:System.Linq.Enumerable.Union%2A>、および <xref:System.Linq.Enumerable.Concat%2A> など、Visual Basic のいくつかの種類のクエリ操作は、メソッドベースの構文でのみ表すことができます。  
  
## <a name="compile-the-code"></a>コードのコンパイル  
System.Linq 名前空間の `Imports` ステートメントを使用して、Visual Basic コンソール アプリケーション プロジェクトを作成します。
  
## <a name="see-also"></a>関連項目

- [LINQ と文字列 (Visual Basic)](linq-and-strings.md)
