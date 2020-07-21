---
title: ループの境界とステップの句が同じ型に変換されないため、'<variablename>' の型を推論できません
ms.date: 07/20/2015
f1_keywords:
- bc30982
- vbc30982
helpviewer_keywords:
- BC30982
ms.assetid: 741e85d9-a747-42ad-a1e1-a3f1928aaff5
ms.openlocfilehash: 74b690ce3dee87e481c629a254e629be4b40f8cd
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84387011"
---
# <a name="type-of-variablename-cannot-be-inferred-because-the-loop-bounds-and-the-step-variable-do-not-widen-to-the-same-type"></a>ループの境界とステップの句が同じ型に変換されないため、'\<variablename>' の型を推論できません

`For...Next` ループを記述していますが、次の条件が当てはまるため、コンパイラがそのループの中でループ制御変数のデータ型を推論できません。

- ループ コントロール変数のデータ型が `As` 句で指定されていません。

- ループ境界とステップ変数に少なくとも 2 つのデータ型が含まれています。

- データ型の間に標準変換が存在しません。

 そのため、コンパイラが、ループの制御変数のデータ型を推論できません。

 次の例で、ステップ変数は文字で、ループの境界はどちらも整数です。 文字と整数の間に標準変換がないため、このエラーが報告されます。

```vb
Dim stepVar = "1"c
Dim m = 0
Dim n = 20

' Not valid.
' For i = 1 To 10 Step stepVar
    ' Loop processing
' Next
```

**エラー ID:** BC30982

## <a name="to-correct-this-error"></a>このエラーを解決するには

- 必要に応じて、ループの境界とステップ変数の型を変更して、それらのうち少なくとも 1 つが、他の型の拡大変換先の型になるようにします。 前の例では、`stepVar` の型を `Integer` に変更します。

  ```vb
  Dim stepVar = 1
  ```

  \- または -

  ```vb
  Dim stepVar As Integer = 1
  ```

- 明示的な変換関数を使用して、ループの境界とステップ変数を適切な型に変換します。 前の例では、`Val` 関数を `stepVar` に適用します。

  ```vb
  For i = 1 To 10 Step Val(stepVar)
      ' Loop processing
  Next
  ```

## <a name="see-also"></a>関連項目

- <xref:Microsoft.VisualBasic.Conversion.Val%2A>
- [For...Next ステートメント](../statements/for-next-statement.md)
- [暗黙の型変換と明示的な型変換](../../programming-guide/language-features/data-types/implicit-and-explicit-conversions.md)
- [ローカル型の推論](../../programming-guide/language-features/variables/local-type-inference.md)
- [Option Infer ステートメント](../statements/option-infer-statement.md)
- [データ型変換関数](../functions/type-conversion-functions.md)
- [拡大変換と縮小変換](../../programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)
