---
title: 連結クエリのパフォーマンス (LINQ to XML)
ms.date: 07/20/2015
ms.assetid: 589f2adc-69f9-404d-b9d6-4c28dabea7f7
ms.openlocfilehash: 6b87f2744f663ebd45dceb036dcaac71b80765fc
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84396390"
---
# <a name="performance-of-chained-queries-linq-to-xml-visual-basic"></a>連結クエリのパフォーマンス (LINQ to XML) (Visual Basic)

LINQ (および LINQ to XML) の重要な利点の 1 つは、連結クエリが、大きい複雑な単一クエリと同様のパフォーマンスを発揮できるという点です。

連結クエリとは、別のクエリをソースとして使用するクエリです。 たとえば、次の単純なコードでは、`query2` のソースとして `query1` があります。

```vb
Dim root As New XElement("Root", New XElement("Child", 1), New XElement("Child", 2), New XElement("Child", 3), New XElement("Child", 4))

Dim query1 = From x In root.Elements("Child") Where CInt(x) >= 3x

Dim query2 = From e In query1 Where CInt(e) Mod 2 = 0e

For Each i As var In query2
    Console.WriteLine("{0}", CInt(i))
Next
```

この例を実行すると、次の出力が生成されます。

```console
4
```

この連結クエリは、リンク リストの反復と同じパフォーマンス プロファイルを提供します。

- <xref:System.Xml.Linq.XContainer.Elements%2A> 軸のパフォーマンスは、基本的にリンク リストの反復と同じです。 <xref:System.Xml.Linq.XContainer.Elements%2A> は、遅延実行のある反復子として実装されます。 つまり、リンク リストの反復の他に、反復子オブジェクトの割り当てや実行状態の追跡などの作業をします。 この作業は、反復子の設定時に行われる作業と、各反復中に行われる作業の 2 つのカテゴリに分けることができます。 設定作業は一定量の小さい作業であり、各反復中に行われる作業はソース コレクションの項目数に比例します。

- `query1` では、`Where` 句によってクエリは <xref:System.Linq.Enumerable.Where%2A> メソッドを呼び出します。 このメソッドも反復子として実装されています。 設定作業は、ラムダ式を参照するデリゲートのインスタンス化と、反復子の通常の設定から成ります。 反復ごとに、デリゲートが呼び出されて述語を実行します。 設定作業と、各反復中に行われる作業は、軸の反復中に行われる作業に似ています。

- `query1` では、SELECT 句によってクエリが <xref:System.Linq.Enumerable.Select%2A> メソッドを呼び出します。 このメソッドには <xref:System.Linq.Enumerable.Where%2A> メソッドと同じパフォーマンス プロファイルがあります。

- `query2` では、`Where` 句と `Select` 句の両方に `query1` と同じパフォーマンス プロファイルがあります。

 したがって、`query2` の反復は最初のクエリのソースにある項目数に直接比例します。つまり線形時間となります。

## <a name="see-also"></a>関連項目

- [パフォーマンス (LINQ to XML) (Visual Basic)](performance-linq-to-xml.md)
