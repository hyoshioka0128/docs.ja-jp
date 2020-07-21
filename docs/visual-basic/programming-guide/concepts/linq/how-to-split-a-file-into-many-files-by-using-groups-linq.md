---
title: '方法: グループを使用して 1 つのファイルを複数のファイルに分割する (LINQ)'
ms.date: 07/20/2015
ms.assetid: 5e8b2a2b-0b1d-4933-8a2b-03e91dfaf77f
ms.openlocfilehash: f6b11ab4b4fe11dbf1cb4cf07654b5ef3f6785ad
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84397714"
---
# <a name="how-to-split-a-file-into-many-files-by-using-groups-linq-visual-basic"></a>方法: グループを使用してファイルを複数のファイルに分割する (LINQ) (Visual Basic)

この例では、2 つのファイルの内容をマージし、新しい方法でデータを整理する一連の新しいファイルを作成するための、1 つの方法を示します。

### <a name="to-create-the-data-files"></a>データ ファイルを作成するには

1. 次の名前を names1.txt という名前のテキスト ファイルにコピーし、プロジェクト フォルダーに保存します。

    ```text
    Bankov, Peter
    Holm, Michael
    Garcia, Hugo
    Potra, Cristina
    Noriega, Fabricio
    Aw, Kam Foo
    Beebe, Ann
    Toyoshima, Tim
    Guy, Wey Yuan
    Garcia, Debra
    ```

2. 次の名前を names2.txt という名前のテキスト ファイルにコピーし、プロジェクト フォルダーに保存します。2 つのファイルには、共通の名前がいくつか含まれていることに注意してください。

    ```text
    Liu, Jinghao
    Bankov, Peter
    Holm, Michael
    Garcia, Hugo
    Beebe, Ann
    Gilchrist, Beth
    Myrcha, Jacek
    Giakoumakis, Leo
    McLin, Nkenge
    El Yassir, Mehdi
    ```

## <a name="example"></a>例

```vb
Class SplitWithGroups

    Shared Sub Main()

        Dim fileA As String() = System.IO.File.ReadAllLines("../../../names1.txt")
        Dim fileB As String() = System.IO.File.ReadAllLines("../../../names2.txt")

        ' Concatenate and remove duplicate names based on
        Dim mergeQuery As IEnumerable(Of String) = fileA.Union(fileB)

        ' Group the names by the first letter in the last name
        Dim groupQuery = From name In mergeQuery
                     Let n = name.Split(New Char() {","})
                     Order By n(0)
                     Group By groupKey = n(0)(0)
                     Into groupName = Group

        ' Create a new file for each group that was created
        ' Note that nested foreach loops are required to access
        ' individual items with each group.
        For Each gGroup In groupQuery
            Dim fileName As String = "..'..'..'testFile_" & gGroup.groupKey & ".txt"
            Dim sw As New System.IO.StreamWriter(fileName)
            Console.WriteLine(gGroup.groupKey)
            For Each item In gGroup.groupName
                Console.WriteLine("   " & item.name)
                sw.WriteLine(item.name)
            Next
            sw.Close()
        Next

        ' Keep console window open in debug mode.
        Console.WriteLine("Files have been written. Press any key to exit.")
        Console.ReadKey()

    End Sub
End Class
' Console Output:
' A
'    Aw, Kam Foo
' B
'    Bankov, Peter
'    Beebe, Ann
' E
'    El Yassir, Mehdi
' G
'    Garcia, Hugo
'    Garcia, Debra
'    Giakoumakis, Leo
'    Gilchrist, Beth
'    Guy, Wey Yuan
' H
'    Holm, Michael
' L
'    Liu, Jinghao
' M
'    McLin, Nkenge
'    Myrcha, Jacek
' N
'    Noriega, Fabricio
' P
'    Potra, Cristina
' T
'    Toyoshima, Tim
```

このプログラムは、データ ファイルとしてグループごとに異なるファイルを同じフォルダーに書き込みます。

## <a name="compile-the-code"></a>コードのコンパイル

System.Linq 名前空間の `Imports` ステートメントを使用して、Visual Basic コンソール アプリケーション プロジェクトを作成します。

## <a name="see-also"></a>関連項目

- [LINQ と文字列 (Visual Basic)](linq-and-strings.md)
- [LINQ とファイル ディレクトリ (Visual Basic)](linq-and-file-directories.md)
