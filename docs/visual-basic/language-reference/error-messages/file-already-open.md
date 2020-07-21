---
title: ファイルは既に開かれています。
ms.date: 07/20/2015
f1_keywords:
- vbrID55
ms.assetid: d674a0fb-ef16-4cc2-9da7-709a8a07dbea
ms.openlocfilehash: 8ec878e04b0128c997c5be51d2c714d55abcde8c
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2019
ms.locfileid: "64665116"
---
# <a name="file-already-open"></a>ファイルは既に開かれています。
別の `FileOpen` またはその他の操作を実行する前に、ファイルを閉じる必要がある場合があります。 このエラーでは以下の原因が考えられます。  
  
- 既に開いているファイルに対して順次出力モードの `FileOpen` 操作が実行されました  
  
- ステートメントが開いているファイルを参照しています。  
  
## <a name="to-correct-this-error"></a>このエラーを解決するには  
  
1. ステートメントを実行する前に、ファイルを閉じます。  
  
## <a name="see-also"></a>関連項目

- <xref:Microsoft.VisualBasic.FileSystem.FileOpen%2A>
