---
title: クリップボードの形式が有効ではありません。
ms.date: 07/20/2015
f1_keywords:
- vbrID460
ms.assetid: 71a4a045-65bb-417d-b3bd-99a9fa3c53f6
ms.openlocfilehash: 15bc530d1030a8c4d720321ea249fdd7fb6cd8b6
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2019
ms.locfileid: "64623094"
---
# <a name="clipboard-format-is-not-valid"></a>クリップボードの形式が有効ではありません。
指定されたクリップボードの形式が、実行されるメソッドと互換性がありません。 このエラーでは以下の原因が考えられます。  
  
- クリップボードの `GetText` または `SetText` メソッドに `vbCFText` または `vbCFLink` 以外のクリップボードの形式を使用している。  
  
- クリップボードの `GetData` または `SetData` メソッドに `vbCFBitmap`、`vbCFDIB`、または `vbCFMetafile` 以外のクリップボードの形式を使用している。  
  
- クリップボードの形式が Microsoft Windows に登録されていないときに、登録されている形式 (&HC000-& HFFFF) に対して Microsoft Windows によって予約されている範囲内のクリップボードの形式を使用して、`DataObject` の `GetData` または `SetData` メソッドを使用している。  
  
## <a name="to-correct-this-error"></a>このエラーを解決するには  
  
- 無効な形式を削除して、有効な形式を指定してください。  
  
## <a name="see-also"></a>関連項目

- [クリップボード: その他の形式の追加](/cpp/mfc/clipboard-adding-other-formats)
