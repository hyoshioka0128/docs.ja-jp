---
title: '方法: 空のクエリ結果セットをデバッグする'
ms.date: 07/20/2015
ms.assetid: b242c90a-d2b8-4309-8a1e-e4e70736c727
ms.openlocfilehash: b2059ccd4638d2fb77c524773cb4bd50f721b5b9
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84398039"
---
# <a name="how-to-debug-empty-query-results-sets-visual-basic"></a>方法: 空のクエリ結果セットをデバッグする (Visual Basic)

XML ツリーのクエリにおける最も一般的な問題の 1 つは、XML ツリーに既定の名前空間がある場合に、XML が名前空間に含まれていないものとして開発者がクエリを記述してしまうことです。

このトピックの最初に示す一連の例では、既定の名前空間内の XML が読み込まれ、クエリが不適切に実行される典型的な例を示しています。

2 番目に示す一連の例では、名前空間内の XML に対してクエリを実行できるようにするために必要な修正を示しています。

詳細については、「[名前空間の概要 (LINQ to XML) (Visual Basic)](namespaces-overview-linq-to-xml.md)」を参照してください。

## <a name="example"></a>例

この例では、名前空間内にある XML の作成、および空の結果セットを返すクエリを示します。

```vb
Dim root As XElement = _
    <Root xmlns='http://www.adventure-works.com'>
        <Child>1</Child>
        <Child>2</Child>
        <Child>3</Child>
        <AnotherChild>4</AnotherChild>
        <AnotherChild>5</AnotherChild>
        <AnotherChild>6</AnotherChild>
    </Root>
Dim c1 As IEnumerable(Of XElement) = _
        From el In root.<Child> _
        Select el
Console.WriteLine("Result set follows:")
For Each el As XElement In c1
    Console.WriteLine(el.Value)
Next
Console.WriteLine("End of result set")
```

この例を実行すると、次の結果が得られます。

```console
Result set follows:
End of result set
```

## <a name="example"></a>例

この例では、名前空間内にある XML の作成と、適切に記述されたクエリを示します。

グローバルな既定の名前空間を宣言して初期化することで問題を解決できます。 これにより、すべての XML プロパティが既定の名前空間に配置されます。 この例を正しく動作させるために必要な変更はこれだけです。

```vb
Imports <xmlns="http://www.adventure-works.com">

Module Module1
    Sub Main()
        Dim root As XElement = _
            <Root xmlns='http://www.adventure-works.com'>
                <Child>1</Child>
                <Child>2</Child>
                <Child>3</Child>
                <AnotherChild>4</AnotherChild>
                <AnotherChild>5</AnotherChild>
                <AnotherChild>6</AnotherChild>
            </Root>
        Dim c1 As IEnumerable(Of XElement) = _
                From el In root.<Child> _
                Select el
        Console.WriteLine("Result set follows:")
        For Each el As XElement In c1
            Console.WriteLine(CInt(el))
        Next
        Console.WriteLine("End of result set")
    End Sub
End Module
```

この例を実行すると、次の結果が得られます。

```console
Result set follows:
1
2
3
End of result set
```

## <a name="see-also"></a>関連項目

- [基本的なクエリ (LINQ to XML) (Visual Basic)](basic-queries-linq-to-xml.md)
