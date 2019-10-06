---
title: 匿名型メンバーの名前は、引数なしの簡易名または修飾名からのみ推論できます
ms.date: 07/20/2015
f1_keywords:
- vbc36556
- bc36556
helpviewer_keywords:
- BC36556
ms.assetid: e3ba1f33-3a71-4f03-9b04-ed5ec17de17c
ms.openlocfilehash: 38f669fe183ac79ebed6e5a122bc70aedc9bb753
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/01/2019
ms.locfileid: "71701226"
---
# <a name="anonymous-type-member-name-can-be-inferred-only-from-a-simple-or-qualified-name-with-no-arguments"></a>匿名型メンバーの名前は、引数なしの簡易名または修飾名からのみ推論できます
複合式から匿名型のメンバー名を推論することはできません。  
  
```vb  
Dim numbers() As Integer = {1, 2, 3, 4, 5}  
' Not valid.  
' Dim instanceName1 = New With {numbers(3)}  
```  
  
 匿名型がメンバーの名前および型を推定できるソースと、メンバーの名前および型を推論できないソースの詳細については、「[How to:匿名型の宣言でプロパティ名と型を推論する @ no__t-0。  
  
 **エラー ID:** BC36556  
  
## <a name="to-correct-this-error"></a>このエラーを解決するには  
  
- 次のコードに示すように、式をメンバー名に割り当てます。  
  
    ```vb  
    Dim instanceName2 = New With {.number = numbers(3)}  
    ```  
  
## <a name="see-also"></a>関連項目

- [匿名型](../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)
- [2 つのオブジェクトが等しいかどうかをテストする方法匿名型の宣言でプロパティ名と型を推論する @ no__t-0
