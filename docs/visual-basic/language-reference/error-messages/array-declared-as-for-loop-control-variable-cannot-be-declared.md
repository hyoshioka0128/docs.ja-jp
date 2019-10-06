---
title: ループ コントロール変数として宣言された配列を初期サイズで宣言することはできません
ms.date: 07/20/2015
f1_keywords:
- vbc32039
- bc32039
helpviewer_keywords:
- BC32039
ms.assetid: 1d8b6560-c9eb-4b71-a038-24c6f5a5ce46
ms.openlocfilehash: 9e8bb7b79b5a770c3c92e47d8e7c01c5b83d6061
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/01/2019
ms.locfileid: "71701208"
---
# <a name="array-declared-as-for-loop-control-variable-cannot-be-declared-with-an-initial-size"></a>ループ コントロール変数として宣言された配列を初期サイズで宣言することはできません
@No__t-0 ループは、配列を*要素*反復変数として使用しますが、その配列を初期化します。  
  
 次のステートメントは、このエラーを生成する方法を示しています。  
  
```vb  
Dim arrayList As New List(Of Integer())  
For Each listElement() As Integer In arrayList  
For Each listElement(1) As Integer In arrayList  
```  
  
 最初の `For Each` ステートメントは、`arrayList` の要素にアクセスするための正しい方法です。 2番目の `For Each` ステートメントでは、このエラーが生成されます。  
  
 **エラー ID:** BC32039  
  
## <a name="to-correct-this-error"></a>このエラーを解決するには  
  
- *要素*反復変数の宣言から初期化を削除します。  
  
## <a name="see-also"></a>関連項目

- [For...Next ステートメント](../../../visual-basic/language-reference/statements/for-next-statement.md)
- [配列](../../../visual-basic/programming-guide/language-features/arrays/index.md)
- [コレクション](../../../standard/collections/index.md)
