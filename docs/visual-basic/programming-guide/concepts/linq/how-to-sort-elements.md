---
title: '方法: 要素を並べ替える'
ms.date: 07/20/2015
ms.assetid: c2c09279-6c8a-482e-8e71-b1453a815052
ms.openlocfilehash: 1204fb4dc190d68956d01ffce225ce40e11538a4
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84397753"
---
# <a name="how-to-sort-elements-visual-basic"></a>方法: 要素を並べ替える (Visual Basic)
この例では、結果を並べ替えるクエリの作成方法を示します。  
  
## <a name="example"></a>例  
 この例では、次の XML ドキュメントを使用します: 「[サンプル XML ファイル:数値データ (LINQ to XML)](sample-xml-file-numerical-data-linq-to-xml.md) を使用します。  
  
```vb  
Dim root As XElement = XElement.Load("Data.xml")  
Dim prices As IEnumerable(Of Decimal) = _  
    From el In root.<Data> _  
    Let price = Convert.ToDecimal(el.<Price>.Value) _  
    Order By (price) _  
    Select price  
For Each el As Decimal In prices  
    Console.WriteLine(el)  
Next  
```  
  
 このコードを実行すると、次の出力が生成されます。  
  
```console  
0.99  
4.95  
6.99  
24.50  
29.00  
66.00  
89.99  
```  
  
## <a name="example"></a>例  
 次の例は名前空間に含まれている XML 用のクエリです。これらのクエリは上の例と同じ機能を表しています。 詳細については、「[名前空間の概要 (LINQ to XML) (Visual Basic)](namespaces-overview-linq-to-xml.md)」を参照してください。  
  
 この例では、次の XML ドキュメントを使用します: 「[サンプル XML ファイル:名前空間内の数値データ](sample-xml-file-numerical-data-in-a-namespace.md)を使用します。  
  
```vb  
Imports <xmlns='http://www.adatum.com'>  
  
Module Module1  
    Sub Main()  
        Dim root As XElement = XElement.Load("DataInNamespace.xml")  
        Dim prices As IEnumerable(Of Decimal) = _  
            From el In root.<Data> _  
            Let price = Convert.ToDecimal(el.<Price>.Value) _  
            Order By (price) _  
            Select price  
        For Each el As Decimal In prices  
            Console.WriteLine(el)  
        Next  
    End Sub  
End Module  
```  
  
 このコードを実行すると、次の出力が生成されます。  
  
```console  
0.99  
4.95  
6.99  
24.50  
29.00  
66.00  
89.99  
```  
  
## <a name="see-also"></a>関連項目

- [データの並べ替え](sorting-data.md)
- [基本的なクエリ (LINQ to XML) (Visual Basic)](basic-queries-linq-to-xml.md)
