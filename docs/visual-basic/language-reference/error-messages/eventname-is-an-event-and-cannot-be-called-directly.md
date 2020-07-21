---
title: "'<eventname>' はイベントであるため、直接呼び出すことはできません。"
ms.date: 07/20/2015
f1_keywords:
- bc32022
- vbc32022
helpviewer_keywords:
- BC32022
ms.assetid: 4dcfcb8d-a9fa-46a7-a034-29d9ff3a59b3
ms.openlocfilehash: 510fff5370e63a31ee271421c0ab6f154518899f
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84409596"
---
# <a name="eventname-is-an-event-and-cannot-be-called-directly"></a>'\<eventname>' はイベントであるため、直接呼び出すことはできません。
'<`eventname`>' はイベントであるため、直接呼び出すことはできません。 `RaiseEvent` ステートメントを使用して、イベントを発生させます。  
  
 プロシージャ呼び出しは、プロシージャ名のイベントを指定します。 イベント ハンドラーはプロシージャですが、イベント自体はシグナル通知デバイスであり、これを発生させて処理する必要があります。  
  
 **エラー ID:** BC32022  
  
## <a name="to-correct-this-error"></a>このエラーを解決するには  
  
1. `RaiseEvent` ステートメントを使用して、イベントを通知し、それを処理するプロシージャを呼び出します。  
  
## <a name="see-also"></a>関連項目

- [RaiseEvent ステートメント](../statements/raiseevent-statement.md)
