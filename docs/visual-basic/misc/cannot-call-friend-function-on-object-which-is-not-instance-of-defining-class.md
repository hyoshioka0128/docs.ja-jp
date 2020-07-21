---
title: 定義クラスのインスタンスではないオブジェクトのフレンド関数は呼び出せません
ms.date: 07/20/2015
f1_keywords:
- vbrID97
ms.assetid: b9d821f0-8565-4f15-bb35-184789c69662
ms.openlocfilehash: c18c04470c4c49113e8195b92185326c5c4197c1
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84400849"
---
# <a name="cannot-call-friend-function-on-object-which-is-not-an-instance-of-defining-class"></a>定義クラスのインスタンスではないオブジェクトのフレンド関数は呼び出せません
クラスの `Friend` プロシージャを呼び出そうとするか、プロセス間またはスレッド間で `Friend` プロパティまたはメソッドにアクセスしようとしました。 `Friend` 手順はクラスの外部のモジュールから呼び出せますが、クラスが定義されているプロジェクトの一部です。  
  
## <a name="to-correct-this-error"></a>このエラーを解決するには  
  
- クラスが定義されているプロジェクトの一部であるモジュールからプロシージャを呼び出しているか、またはアクセスしていることを確認します。  
  
## <a name="see-also"></a>関連項目

- [Friend](../language-reference/modifiers/friend.md)
