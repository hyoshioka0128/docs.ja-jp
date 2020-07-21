---
title: 省略可能な引数には、既定値を指定する必要があります。
ms.date: 07/20/2015
f1_keywords:
- vbc30812
- bc30812
helpviewer_keywords:
- BC30812
ms.assetid: 5091a250-be66-413b-98a3-2a9974c4d600
ms.openlocfilehash: eb782b2fa1fb73c7407b57a0942e5eebb30474ff
ms.sourcegitcommit: ad800f019ac976cb669e635fb0ea49db740e6890
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/29/2019
ms.locfileid: "73040937"
---
# <a name="optional-parameters-must-specify-a-default-value"></a>省略可能な引数には、既定値を指定する必要があります。

省略可能なパラメーターには、呼び出し元のプロシージャによってパラメーターが指定されていない場合に使用できる既定値を指定する必要があります。

**エラー ID:** BC30812

## <a name="example"></a>例

次の例では BC30812 が生成されます。

```vb
Sub Proc1(x As Integer, Optional y As String)
    Console.WriteLine("Default argument is: " & y)
End Sub
```

## <a name="to-correct-this-error"></a>このエラーを解決するには

省略可能なパラメーターの既定値を指定します。

```vb
Sub Proc1(x As Integer, Optional y As String = "Default Value")
    Console.WriteLine("Default argument is: " & y)
End Sub
```

## <a name="see-also"></a>関連項目

- [Optional](../modifiers/optional.md)
