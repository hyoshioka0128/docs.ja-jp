---
title: If ステートメント行の外側でステートメント ブロックを終了することはできません。
ms.date: 07/20/2015
f1_keywords:
- vbc32005
- bc32005
helpviewer_keywords:
- BC32005
ms.assetid: 4039f51b-e0ee-4789-a89b-45d06de06b5d
ms.openlocfilehash: 3fe3faaa3637446bb6ab443ba1d6e1d1004b4d48
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84400319"
---
# <a name="statement-cannot-end-a-block-outside-of-a-line-if-statement"></a>If ステートメント行の外側でステートメント ブロックを終了することはできません。
単一行の `If` ステートメントにコロン (:) で区切られた複数のステートメントが含まれていて、そのうちの 1 つが、単一行の `If` の外側にある制御ブロックの `End` ステートメントです。 単一行の `If` ステートメントで、`End If` ステートメントが使用されません。  
  
 **エラー ID:** BC32005  
  
## <a name="to-correct-this-error"></a>このエラーを解決するには  
  
- 単一行の `If` ステートメントを、`End If` ステートメントが含まれている制御ブロックの外側に移動します。  
  
## <a name="see-also"></a>関連項目

- [If...Then...Else ステートメント](../statements/if-then-else-statement.md)
