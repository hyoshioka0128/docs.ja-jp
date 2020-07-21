---
title: "'typename' は Null 許容型であるため、'typename' 型の 'IsNot' オペランドは 'Nothing' とのみ比較できます"
ms.date: 07/20/2015
f1_keywords:
- bc32128
- vbc32128
helpviewer_keywords:
- BC32128
ms.assetid: 1155b23a-ad75-4bab-b9da-73f35c767a36
ms.openlocfilehash: fb61b04021bd844fade94413b4f3b28b82f6411b
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84402799"
---
# <a name="isnot-operand-of-type-typename-can-only-be-compared-to-nothing-because-typename-is-a-nullable-type"></a>'typename' は Null 許容型であるため、'typename' 型の 'IsNot' オペランドは 'Nothing' とのみ比較できます

Null 許容値型として宣言された変数が、`Nothing` 演算子を使用して、`IsNot` 以外の式と比較されました。

**エラー ID:** BC32128

## <a name="to-correct-this-error"></a>このエラーを解決するには

`Nothing` 演算子を使用して、Null 許容型を `IsNot` 以外の式と比較するには、次の例に示すように、Null 許容型に対して `GetType` メソッドを呼び出し、その結果を式と比較します。

```vb
Dim number? As Integer = 5

If number IsNot Nothing Then
  If number.GetType() IsNot Type.GetType("System.Int32") Then

  End If
End If
```

## <a name="see-also"></a>関連項目

- [null 許容値型](../../programming-guide/language-features/data-types/nullable-value-types.md)
- [IsNot 演算子](../operators/isnot-operator.md)
