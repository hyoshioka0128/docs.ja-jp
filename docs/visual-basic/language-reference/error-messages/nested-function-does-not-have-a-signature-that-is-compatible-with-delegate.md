---
title: 入れ子になった関数に、デリゲート '<delegatename>' と互換性のあるシグネチャがありません。
ms.date: 07/20/2015
f1_keywords:
- vbc36532
- bc36532
helpviewer_keywords:
- BC36532
ms.assetid: 493f292c-d81e-40ef-8b47-61f020571829
ms.openlocfilehash: 28d07f01c0fd467cb68d73749988273eee95edf4
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84409427"
---
# <a name="nested-function-does-not-have-a-signature-that-is-compatible-with-delegate-delegatename"></a>入れ子になった関数に、デリゲート '\<delegatename>' と互換性のあるシグネチャがありません。

ラムダ式が、互換性のないシグネチャを含むデリゲートに割り当てられています。 たとえば、次のコードでは、デリゲート `Del` に 2 つの整数パラメーターがあります。

```vb
Delegate Function Del(ByVal p As Integer, ByVal q As Integer) As Integer
```

このエラーは、1 つの引数を含むラムダ式が `Del` 型として宣言されている場合に発生します。

```vb
' Neither of these is valid.
' Dim lambda1 As Del = Function(n As Integer) n + 1
' Dim lambda2 As Del = Function(n) n + 1
```

**エラー ID:** BC36532

## <a name="to-correct-this-error"></a>このエラーを解決するには

デリゲート定義または割り当てられているラムダ式を調整して、シグネチャに互換性を持たせるようにします。

## <a name="see-also"></a>関連項目

- [厳密でないデリゲート変換](../../programming-guide/language-features/delegates/relaxed-delegate-conversion.md)
- [ラムダ式](../../programming-guide/language-features/procedures/lambda-expressions.md)
