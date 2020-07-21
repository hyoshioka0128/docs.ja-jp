---
title: Null 条件演算子
ms.date: 10/19/2018
helpviewer_keywords:
- null-conditional operators [Visual Basic]
- ?. operator [Visual Basic]
- ?[] operator [C#]
- ?[] operator [Visual Basic]
ms.openlocfilehash: bffbba859968e0a050397cd9e685c142f801798a
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84401473"
---
# <a name="-and--null-conditional-operators-visual-basic"></a>?. および ?() Null 条件演算子 (Visual Basic)

メンバー アクセス (`?.`) またはインデックス (`?()`) 演算を実行する前に、左の演算子の値で null (`Nothing`) のテストを行います。左側のオペランドが `Nothing` に評価されると、`Nothing` が返されます。 通常、値の型を返す式では、Null 条件演算子は <xref:System.Nullable%601> を返します。

これらの演算子を使用すると、少ないコードで null チェックを処理することができます (特に、データ構造を下っていく場合)。 次に例を示します。

```vb
' Nothing if customers is Nothing
Dim length As Integer? = customers?.Length

' Nothing if customers is Nothing
Dim first As Customer = customers?(0)

' Nothing if customers, the first customer, or Orders is Nothing
Dim count As Integer? = customers?(0)?.Orders?.Count()
```

比較のために、Null 条件演算子を使用しない最初の式の代替コードは次のとおりです。

```vb
Dim length As Integer
If customers IsNot Nothing Then
   length = customers.Length
End If
```

(次の例のブール型プロパティ `IsAllowedFreeShipping` のように、) オブジェクトのブール型メンバーの値に基づいて、null の可能性があるオブジェクトに対してアクションを実行する必要がある場合があります。

```vb
Dim customer = FindCustomerByID(123) 'customer will be Nothing if not found.

If customer IsNot Nothing AndAlso customer.IsAllowedFreeShipping Then
  ApplyFreeShippingToOrders(customer)
End If
```

次のように Null 条件演算子を使用することで、コードを短縮し、手動での null のチェックを回避できます。

```vb
Dim customer = FindCustomerByID(123) 'customer will be Nothing if not found.

If customer?.IsAllowedFreeShipping Then ApplyFreeShippingToOrders(customer)
```

Null 条件演算子はショートサーキットです。  条件付きメンバー アクセスとインデックス演算のチェーンにある 1 つの演算で `Nothing` が返されると、チェーンの実行の残りの部分は停止します。  次の例で、`A`、`B`、または `C` が `Nothing` に評価されると、`C(E)` は評価されません。

```vb
A?.B?.C?(E)
```

Null 条件メンバー アクセスのもう 1 つの用途は、はるかに少ないコードを使ってスレッドセーフな方法でデリゲートを呼び出すことです。  次の例では、`NewsBroadcaster` と `NewsReceiver` の 2 つの型を定義しています。 ニュース項目は、`NewsBroadcaster.SendNews` デリゲートによって受信者に送信されます。

```vb
Public Module NewsBroadcaster
   Dim SendNews As Action(Of String)

   Public Sub Main()
      Dim rec As New NewsReceiver()
      Dim rec2 As New NewsReceiver()
      SendNews?.Invoke("Just in: A newsworthy item...")
   End Sub

   Public Sub Register(client As Action(Of String))
      SendNews = SendNews.Combine({SendNews, client})
   End Sub
End Module

Public Class NewsReceiver
   Public Sub New()
      NewsBroadcaster.Register(AddressOf Me.DisplayNews)
   End Sub

   Public Sub DisplayNews(newsItem As String)
      Console.WriteLine(newsItem)
   End Sub
End Class
```

`SendNews` 呼び出しリストに要素がない場合、`SendNews` デリゲートは <xref:System.NullReferenceException> をスローします。 Null 条件演算子の前は、次のようなコードによって、デリゲート呼び出しリストが `Nothing` でないことが確認されました。

```vb
SendNews = SendNews.Combine({SendNews, client})
If SendNews IsNot Nothing Then
   SendNews("Just in...")
End If
```

新しい方法は格段に単純です。

```vb
SendNews = SendNews.Combine({SendNews, client})
SendNews?.Invoke("Just in...")
```

コンパイラが `SendNews` を評価するためのコードを一度しか生成せず、一時変数に結果が保持されるため、新しい方法はスレッド セーフです。 null 条件デリゲート呼び出し構文 `SendNews?(String)` がないため、`Invoke` メソッドを明示的に呼び出す必要があります。

## <a name="see-also"></a>関連項目

- [演算子 (Visual Basic)](index.md)
- [Visual Basic プログラミング ガイド](../../programming-guide/index.md)
- [Visual Basic の言語リファレンス](../index.md)
