---
title: Delegate クラス '<classname>' には Invoke メソッドが含まれていないため、この型の式をメソッド呼び出しのターゲットに設定することはできません。
ms.date: 07/20/2015
f1_keywords:
- vbc30220
- bc30220
helpviewer_keywords:
- BC30220
ms.assetid: 6be0d61c-f2f9-4f9b-ab90-8871a0d7206d
ms.openlocfilehash: 27be97ba2930791bcb9012c824bc418a0089b037
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84409713"
---
# <a name="delegate-class-classname-has-no-invoke-method-so-an-expression-of-this-type-cannot-be-the-target-of-a-method-call"></a>Delegate クラス '\<classname>' には Invoke メソッドが含まれていないため、この型の式をメソッド呼び出しのターゲットに設定することはできません。
デリゲート クラスに `Invoke` が実装されていないため、デリゲートを使用して `Invoke` を呼び出すことができませんでした。  
  
 **エラー ID:** BC30220  
  
## <a name="to-correct-this-error"></a>このエラーを解決するには  
  
1. デリゲート クラスのインスタンスが `Dim` ステートメントを使用して作成されていること、およびプロシージャが `AddressOf` 演算子を使用してデリゲート インスタンスに割り当てられていることを確認してください。  
  
2. デリゲート クラスを実装するコードを見つけ、それによって `Invoke` プロシージャが実装されることを確認します。  
  
## <a name="see-also"></a>関連項目

- [デリゲート](../../programming-guide/language-features/delegates/index.md)
- [Delegate ステートメント](../statements/delegate-statement.md)
- [AddressOf 演算子](../operators/addressof-operator.md)
- [Dim ステートメント](../statements/dim-statement.md)
