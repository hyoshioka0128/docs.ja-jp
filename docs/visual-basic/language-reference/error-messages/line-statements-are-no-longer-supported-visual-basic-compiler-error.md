---
title: "'Line' ステートメントはサポートされていません (Visual Basic コンパイラ エラー)"
ms.date: 07/20/2015
f1_keywords:
- bc30830
- vbc30830
helpviewer_keywords:
- BC30830
ms.assetid: 4734bc1d-882e-4555-b498-1f1ec0399d16
ms.openlocfilehash: a3d243f39f3fc45ca6b1ba0d26892d4c3db56f59
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84397299"
---
# <a name="line-statements-are-no-longer-supported-visual-basic-compiler-error"></a>'Line' ステートメントはサポートされていません (Visual Basic コンパイラ エラー)
Line ステートメントは現在サポートされていません。 ファイル I/O 機能は `Microsoft.VisualBasic.FileSystem.LineInput` として使用でき、グラフィックス機能は `System.Drawing.Graphics.DrawLine` として使用できます。  
  
 **エラー ID:** BC30830  
  
## <a name="to-correct-this-error"></a>このエラーを解決するには  
  
1. ファイル アクセスを実行する場合は、`Microsoft.VisualBasic.FileSystem.LineInput` を使用します。  
  
2. グラフィックス処理を行っている場合は、 `System.Drawing.Graphics.Drawline`を使用します。  
  
## <a name="see-also"></a>関連項目

- <xref:System.IO>
- <xref:System.Drawing>
- [Visual Basic におけるファイル アクセス](../../developing-apps/programming/drives-directories-files/file-access.md)
