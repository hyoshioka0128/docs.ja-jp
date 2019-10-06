---
title: クラスの明示的なインスタンスを指定しないで、共有メソッドまたは共有メンバー初期化子内からクラスのインスタンス メンバーへ参照することはできません。
ms.date: 07/20/2015
f1_keywords:
- vbc30369
- bc30369
helpviewer_keywords:
- Shared
- BC30369
ms.assetid: 39d9466b-c1f3-4406-91a5-3d6c52d23a3d
ms.openlocfilehash: a2a5ab99ff68e6dce783a2fd986ee6e8c15ae858
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/01/2019
ms.locfileid: "71701174"
---
# <a name="cannot-refer-to-an-instance-member-of-a-class-from-within-a-shared-method-or-shared-member-initializer-without-an-explicit-instance-of-the-class"></a>クラスの明示的なインスタンスを指定しないで、共有メソッドまたは共有メンバー初期化子内からクラスのインスタンス メンバーへ参照することはできません。
共有プロシージャ内から、クラスの共有されていないメンバーを参照しようとしました。 このような状況の例を次に示します。  
  
```vb  
Class sample  
    Public x as Integer  
    Public Shared Sub setX()  
        x = 10  
    End Sub  
End Class  
```  
  
 前の例では、代入ステートメント `x = 10` によって、このエラーメッセージが生成されます。 これは、共有プロシージャがインスタンス変数にアクセスしようとしているためです。  
  
 変数 `x` は[Shared](../../../visual-basic/language-reference/modifiers/shared.md)として宣言されていないため、インスタンスメンバーです。 クラス `sample` の各インスタンスには、独自の個別の変数 `x` が含まれています。 1つのインスタンスが `x` の値を設定または変更した場合、他のインスタンスの `x` の値には影響しません。  
  
 ただし、`setX` というプロシージャは、クラス `sample` のすべてのインスタンスの間で `Shared` です。 これは、クラスの1つのインスタンスに関連付けられておらず、個別のインスタンスとは独立して動作することを意味します。 特定のインスタンスとの接続がないため、`setX` はインスタンス変数にアクセスできません。 @No__t 0 の変数でのみ動作する必要があります。 @No__t-0 の場合、共有変数の値を設定または変更すると、その新しい値はクラスのすべてのインスタンスで使用できるようになります。  
  
 **エラー ID:** BC30369  
  
## <a name="to-correct-this-error"></a>このエラーを解決するには  
  
1. メンバーをクラスのすべてのインスタンス間で共有するか、インスタンスごとに個別に保持するかを決定します。  
  
2. メンバーの1つのコピーをすべてのインスタンス間で共有する場合は、メンバー宣言に `Shared` キーワードを追加します。 プロシージャ宣言で @no__t 0 キーワードを保持します。  
  
3. 各インスタンスがメンバーの個別のコピーを持つようにする場合は、メンバー宣言に `Shared` を指定しないでください。 プロシージャ宣言から @no__t 0 キーワードを削除します。  
  
## <a name="see-also"></a>関連項目

- [Shared](../../../visual-basic/language-reference/modifiers/shared.md)
