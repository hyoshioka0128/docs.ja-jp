---
title: Expression は値であるため、代入式のターゲットにすることはできません。
ms.date: 07/20/2015
f1_keywords:
- bc30068
- vbc30068
helpviewer_keywords:
- BC30068
ms.assetid: d65141e1-f31e-4ac5-a3b8-0b2e02a71ebf
ms.openlocfilehash: 9e4dbaf2f2800454c673cd58ddec4cf0f6e5c6b9
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84409508"
---
# <a name="expression-is-a-value-and-therefore-cannot-be-the-target-of-an-assignment"></a>Expression は値であるため、代入式のターゲットにすることはできません。

ステートメントで式に値を代入しようとしています。 実行時に値を代入できるのは、書き込み可能な変数、プロパティ、または配列要素だけです。 次の例では、このエラーがどのように発生する可能性があるかを示しています。

```vb
Dim yesterday As Integer
ReadOnly maximum As Integer = 45
yesterday + 1 = DatePart(DateInterval.Day, Now)
' The preceding line is an ERROR because of an expression on the left.
maximum = 50
' The preceding line is an ERROR because maximum is declared ReadOnly.
```

同様の例は、プロパティや配列要素にも当てはまる可能性があります。

**間接アクセス。** 値の型による間接アクセスによって、このエラーが発生することもあります。 次のコード例を考えてみます。ここでは、<xref:System.Windows.Forms.Control.Location%2A> 経由で間接的にアクセスすることによって、<xref:System.Drawing.Point> の値を設定しようとしています。

```vb
' Assume this code runs inside Form1.
Dim exitButton As New System.Windows.Forms.Button()
exitButton.Text = "Exit this form"
exitButton.Location.X = 140
' The preceding line is an ERROR because of no storage for Location.
```

前の例の最後のステートメントは、<xref:System.Windows.Forms.Control.Location%2A> プロパティによって返される <xref:System.Drawing.Point> 構造体の一時的な割り当てのみを作成しているため、失敗します。 構造体は値の型であり、一時的な構造体は、ステートメントの実行後に保持されません。 この問題を解決するには、<xref:System.Windows.Forms.Control.Location%2A> の変数を宣言して使用します。これにより、<xref:System.Drawing.Point> 構造体のより永続的な割り当てが作成されます。 次の例に、前の例の最後のステートメントを置き換えることができるコードを示しています。

```vb
Dim exitLocation as New System.Drawing.Point(140, exitButton.Location.Y)
exitButton.Location = exitLocation
```

**エラー ID:** BC30068

## <a name="to-correct-this-error"></a>このエラーを解決するには

- ステートメントで式に値を代入している場合は、式を 1 つの書き込み可能な変数、プロパティ、または配列要素に置き換えます。

- ステートメントで値の型 (通常は構造体) を介して間接的にアクセスしている場合は、値の型を保持する変数を作成します。

- 変数に適切な構造体 (またはその他の値の型) を割り当てます。

- 変数を使用してプロパティにアクセスし、それに値を代入します。

## <a name="see-also"></a>関連項目

- [演算子および式](../../programming-guide/language-features/operators-and-expressions/index.md)
- [ステートメント](../../programming-guide/language-features/statements.md)
- [プロシージャのトラブルシューティング](../../programming-guide/language-features/procedures/troubleshooting-procedures.md)
