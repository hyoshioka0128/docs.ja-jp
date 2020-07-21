---
title: "'Custom' 修飾子は、明示的なデリゲート型なしで宣言されたイベントでは無効です。"
ms.date: 07/20/2015
f1_keywords:
- vbc31122
- bc31122
helpviewer_keywords:
- BC31122
ms.assetid: 6911f0d1-641a-473b-906d-8ee5681194be
ms.openlocfilehash: 0c5a4188fedf9685afdd1cde4c1de93a0b43b919
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84409785"
---
# <a name="custom-modifier-is-not-valid-on-events-declared-without-explicit-delegate-types"></a>'Custom' 修飾子は、明示的なデリゲート型なしで宣言されたイベントでは無効です。
非カスタム イベントと異なり、`Custom Event` 宣言では、イベント名の後に、イベントのデリゲート型を明示的に指定する `As` 句が必要です。  
  
 非カスタム イベントを定義するには、`As` 句と明示的なデリゲート型を使用するか、またはイベント名の直後にパラメーター リストを指定します。  
  
 **エラー ID:** BC31122  
  
## <a name="to-correct-this-error"></a>このエラーを解決するには  
  
1. カスタム イベントと同じパラメーター リストでデリゲートを定義します。  
  
     たとえば、`Custom Event` が `Custom Event Test(ByVal sender As Object, ByVal i As Integer)` によって定義されている場合、対応するデリゲートは次のようになります。  
  
     [!code-vb[VbVbalrEventError#18](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrEventError/VB/VbVbalrEventError.vb#18)]  
  
2. カスタム イベントのパラメーター リストを、デリゲート型を指定する `As` 句に置き換えます。  
  
     この例を続行すると、`Custom Event` 宣言は次のように書き換えられます。  
  
     [!code-vb[VbVbalrEventError#19](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrEventError/VB/VbVbalrEventError.vb#19)]  
  
## <a name="example"></a>例  
 この例では、`Custom Event` を宣言し、デリゲート型で必要な `As` 句を指定しています。  
  
 [!code-vb[VbVbalrEventError#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrEventError/VB/VbVbalrEventError.vb#2)]  
  
## <a name="see-also"></a>関連項目

- [Event ステートメント](../statements/event-statement.md)
- [Delegate ステートメント](../statements/delegate-statement.md)
- [イベント](../../programming-guide/language-features/events/index.md)
