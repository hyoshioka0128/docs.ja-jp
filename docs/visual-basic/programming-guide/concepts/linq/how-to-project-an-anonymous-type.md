---
title: '方法: 匿名型を射影する'
ms.date: 07/20/2015
ms.assetid: 30b42987-0e0e-4b2b-adb1-5255ddfbcd7b
ms.openlocfilehash: 459602eb7ede0bd055e00d3c7620cb95ec5408ff
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84396481"
---
# <a name="how-to-project-an-anonymous-type-visual-basic"></a>方法: 匿名型を射影する (Visual Basic)
短期間しか使用しないことがわかっている新しい型にクエリを射影することが必要になる場合があります。 単に射影で使用するために新しい型を作成するのは大きな負担です。 この場合は、匿名型に射影する方法が効率的です。 匿名型を使用すると、クラス名を指定することなくクラスを定義し、そのクラスのオブジェクトを宣言して初期化できます。  
  
 匿名型とは、*タプル*の数学的概念を C# で実装したものです。 タプルという数学用語は、1 タプル、2 タプル、3 タプル、4 タプル、5 タプル、n タプルという数列に基づいています。 組とは、それぞれが特定の型を持つオブジェクトの有限のシーケンスを意味します。 名前と値のペアの一覧と呼ばれることもあります。 たとえば、[サンプル XML ファイル: 一般的な購買発注書 (LINQ to XML)](sample-xml-file-typical-purchase-order-linq-to-xml.md) の XML ドキュメントのアドレス コンテンツは次のように表されます。  
  
```  
Name: Ellen Adams  
Street: 123 Maple Street  
City: Mill Valley  
State: CA  
Zip: 90952  
Country: USA  
```  
  
 匿名型のインスタンスを作成するときは、注文 n のタプルを作成すると考えると簡単です。 `Select` 句でタプルを作成するクエリを記述すると、そのクエリからタプルの `IEnumerable` が返されます。  
  
## <a name="example"></a>例  
 この例では、`Select` 句で匿名型を射影しています。 さらに、`Dim` を使用して `IEnumerable` オブジェクトを作成しています。 `For Each` ループ内では、繰り返し変数が、クエリ式で作成された匿名型のインスタンスになります。  
  
 この例では、次の XML ドキュメントを使用します: 「[サンプル XML ファイル:顧客と注文 (LINQ to XML)](sample-xml-file-customers-and-orders-linq-to-xml.md)」。  
  
```vb  
Dim custOrd As XElement = XElement.Load("CustomersOrders.xml")  
Dim custList = _  
    From el In custOrd.<Customers>.<Customer> _  
    Select New With { _  
        .CustomerID = el.@<CustomerID>, _  
        .CompanyName = el.<CompanyName>.Value, _  
        .ContactName = el.<ContactName>.Value _  
    }  
For Each cust In custList  
    Console.WriteLine("{0}:{1}:{2}", cust.CustomerID, cust.CompanyName, cust.ContactName)  
Next  
```  
  
 このコードを実行すると、次の出力が生成されます。  
  
```console  
GREAL:Great Lakes Food Market:Howard Snyder  
HUNGC:Hungry Coyote Import Store:Yoshi Latimer  
LAZYK:Lazy K Kountry Store:John Steel  
LETSS:Let's Stop N Shop:Jaime Yorres  
```  
  
## <a name="see-also"></a>関連項目

- [プロジェクションと変換 (LINQ to XML) (Visual Basic)](projections-and-transformations-linq-to-xml.md)
