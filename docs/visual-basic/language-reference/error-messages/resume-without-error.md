---
title: エラーが発生していないときに Resume を実行することはできません。
ms.date: 07/20/2015
f1_keywords:
- vbrID20
ms.assetid: f9631804-fd36-4443-b36c-30db827e6176
ms.openlocfilehash: b6b565c88acadca048ade22ab00ac68539725f78
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84400371"
---
# <a name="resume-without-error"></a>エラーが発生していないときに Resume を実行することはできません。
`Resume` ステートメントがエラー処理コードの外側に記述されていたか、エラーが発生していない場合でもコードがエラー ハンドラーにジャンプしました。  
  
## <a name="to-correct-this-error"></a>このエラーを解決するには  
  
1. `Resume` ステートメントをエラー ハンドラー内に移動するか、または削除します。  
  
2. プロシージャ間でラベルにジャンプすることはできないため、プロシージャでエラー ハンドラーを識別するラベルを検索します。 `On Error GoTo` ステートメントではない `GoTo` ステートメントのターゲットとして重複するラベルが指定されている場合は、その目的のターゲットと一致するように行ラベルを変更します。  
  
## <a name="see-also"></a>関連項目

- [Resume ステートメント](../statements/resume-statement.md)
- [On Error ステートメント](../statements/on-error-statement.md)
