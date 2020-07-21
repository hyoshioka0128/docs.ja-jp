---
title: ファイルにこれ以上データがありません。
ms.date: 07/20/2015
f1_keywords:
- vbrID62
ms.assetid: 65292704-6e7d-4622-9f50-eb655a59b016
ms.openlocfilehash: 5da14c7a28ecdcd023fc6439cb6ed64444c1183b
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62013791"
---
# <a name="input-past-end-of-file"></a>ファイルにこれ以上データがありません。
`Input` ステートメントが空のファイル、またはすべてのデータが使用されているファイルから読み取っているか、またはバイナリ アクセス用に開かれたファイルで `EOF` 関数を使用しました。  
  
## <a name="to-correct-this-error"></a>このエラーを解決するには  
  
1. `Input` ステートメントの直前で `EOF` 関数を使用して、ファイルの末尾を検出します。  
  
2. ファイルがバイナリ アクセス用に開かれている場合は、`Seek` と `Loc` を使用します。  
  
## <a name="see-also"></a>関連項目

- <xref:Microsoft.VisualBasic.FileSystem.Input%2A>
- <xref:Microsoft.VisualBasic.FileSystem.EOF%2A>
- <xref:Microsoft.VisualBasic.FileSystem.Seek%2A>
- <xref:Microsoft.VisualBasic.FileSystem.Loc%2A>
