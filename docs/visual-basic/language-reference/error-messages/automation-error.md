---
title: オートメーション エラーです。
ms.date: 07/20/2015
f1_keywords:
- vbrID440
ms.assetid: 2c4be5c5-2f0d-4a2b-96fe-d1b24f08fc4c
ms.openlocfilehash: d62ba57db8bffefb2cfebed705251d87fe285602
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84409895"
---
# <a name="automation-error"></a>オートメーション エラーです。

メソッドの実行中、またはオブジェクト変数のプロパティの取得中または設定中にエラーが発生しました。 エラーは、オブジェクトを作成したアプリケーションによって報告されました。  
  
## <a name="to-correct-this-error"></a>このエラーを解決するには  
  
1. `Err` オブジェクトのプロパティをチェックし、エラーの原因と性質を確認します。  
  
2. アクセス ステートメントの直前で `On Error Resume Next` ステートメントを使用し、アクセス ステートメントの直後のエラーを確認します。  
  
## <a name="see-also"></a>関連項目

- [エラーの種類](../../programming-guide/language-features/error-types.md)
- [ご意見](/visualstudio/ide/feedback-options)
