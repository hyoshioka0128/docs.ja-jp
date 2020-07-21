---
title: 内部エラーのために完全な運用システム名を取得できませんでした
ms.date: 07/20/2015
f1_keywords:
- vbrDiagnosticInfo_FullOSName
ms.assetid: f69da02b-eb9a-4284-bb9e-3025517ae6c1
ms.openlocfilehash: 67e8fb5e906800d28bf15714463b7ff6ae585693
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84402279"
---
# <a name="could-not-obtain-full-operation-system-name-due-to-internal-error"></a>内部エラーのために完全な運用システム名を取得できませんでした
内部エラーのために完全な運用システム名を取得できませんでした。 これは、現在のコンピューターに WMI が存在しないことが原因である場合があります。  
  
 `My.Computer.Info.OSFullName` プロパティの呼び出しに失敗しました。 このエラーの考えられる原因は、Windows Management Instrumentation (WMI) が、現在のコンピューターにインストールされていないことです。  
  
## <a name="to-correct-this-error"></a>このエラーを解決するには  
  
1. `Try...Catch` プロパティの呼び出しの周囲に `My.Computer.Info.OSFullName` ブロックを追加します。  
  
2. WMI とそのインストール方法の詳細については、「」にアクセスし、「Windows Management Instrumentation Core」を検索してください。  
  
## <a name="see-also"></a>関連項目

- [マイ. Computer. Info. OSFullName](xref:Microsoft.VisualBasic.Devices.ComputerInfo.OSFullName)
- [.NET での例外の処理とスロー](../../standard/exceptions/index.md)
- [Try...Catch...Finally ステートメント](../language-reference/statements/try-catch-finally-statement.md)
