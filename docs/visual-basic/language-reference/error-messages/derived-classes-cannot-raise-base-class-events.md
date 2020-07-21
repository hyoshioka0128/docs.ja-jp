---
title: 派生クラスで基本クラスのイベントを発生させることはできません。
ms.date: 07/20/2015
f1_keywords:
- vbc30029
- bc30029
helpviewer_keywords:
- BC30029
ms.assetid: 63afa1c6-2f93-4512-a2f0-372455979771
ms.openlocfilehash: c59212a28ba27123a7db9163ff7437c159a3d310
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84409700"
---
# <a name="derived-classes-cannot-raise-base-class-events"></a>派生クラスで基本クラスのイベントを発生させることはできません。
イベントを発生させることができるのは、それが宣言されている宣言領域からのみです。 そのため、クラスは、派生元のクラスであっても、他のクラスからイベントを発生させることはできません。  
  
 **エラー ID:** BC30029  
  
## <a name="to-correct-this-error"></a>このエラーを解決するには  
  
- `Event` ステートメントまたは `RaiseEvent` ステートメントが同じクラス内になるように移動します。  
  
## <a name="see-also"></a>関連項目

- [Event ステートメント](../statements/event-statement.md)
- [RaiseEvent ステートメント](../statements/raiseevent-statement.md)
