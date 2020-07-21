---
title: "'Class' ステートメントの終わりには、対応する 'End Class' を指定しなければなりません。"
ms.date: 07/20/2015
f1_keywords:
- vbc30481
- bc30481
helpviewer_keywords:
- BC30481
ms.assetid: 583f3029-bc3a-4e06-866f-92dbecc46f19
ms.openlocfilehash: 01c231f577d21028e9ef92f37c7ac5f7f1fe2aa3
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84415389"
---
# <a name="class-statement-must-end-with-a-matching-end-class"></a>'Class' ステートメントの終わりには、対応する 'End Class' を指定しなければなりません。
`Class` は `Class` ブロックを開始するために使用します。ブロックの先頭にのみ指定でき、対応する`End Class` ステートメントでブロックを終えます。 `Class` ステートメントが重複しているか、`Class` ブロックの最後に `End Class` が使用されませんでした。  
  
 **エラー ID:** BC30481  
  
## <a name="to-correct-this-error"></a>このエラーを解決するには  
  
- 不要な `Class` ステートメントを見つけて削除します。  
  
- 一致する `End Class` で `Class` ブロックを終了します。  
  
## <a name="see-also"></a>関連項目

- [End \<keyword> ステートメント](../statements/end-keyword-statement.md)
- [Class ステートメント](../statements/class-statement.md)
