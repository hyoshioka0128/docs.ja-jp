---
title: メソッドや複数行のラムダの内部では有効でないステートメントです。
ms.date: 07/20/2015
f1_keywords:
- vbc30024
- bc30024
helpviewer_keywords:
- BC30024
ms.assetid: 758e7a8f-429b-42c1-9a78-778e5b480e04
ms.openlocfilehash: f3c43d640259d5e1af545e2610088aab5d70453d
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84396247"
---
# <a name="statement-is-not-valid-inside-a-methodmultiline-lambda"></a>メソッドや複数行のラムダの内部では有効でないステートメントです。
ステートメントは、`Sub`、`Function`、プロパティ `Get`、またはプロパティ `Set` プロシージャ内で無効です。 一部のステートメントは、モジュール レベルまたはクラス レベルで配置できます。 `Option Strict` などの他のものは、名前空間レベルで、他のすべての宣言の前に配置する必要があります。  
  
 **エラー ID:** BC30024  
  
## <a name="to-correct-this-error"></a>このエラーを解決するには  
  
- プロシージャからステートメントを削除します。  
  
## <a name="see-also"></a>関連項目

- [Sub ステートメント](../statements/sub-statement.md)
- [Function ステートメント](../statements/function-statement.md)
- [Get ステートメント](../statements/get-statement.md)
- [Set ステートメント](../statements/set-statement.md)
