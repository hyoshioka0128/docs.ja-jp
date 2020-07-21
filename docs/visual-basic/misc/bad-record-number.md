---
title: レコード番号が正しくありません
ms.date: 07/20/2015
f1_keywords:
- vbrID63
ms.assetid: 1fcc33f8-822a-4de9-a6e3-228ddb5824a6
ms.openlocfilehash: 44a11d95d33041de9d637684f41cb003dcc36b97
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84367543"
---
# <a name="bad-record-number"></a>レコード番号が正しくありません
`a FileGet`、 `FilePut`、 `FileGetObject`、または `FilePutObject` ステートメント内のレコード番号が 0 以下です。  
  
## <a name="to-correct-this-error"></a>このエラーを解決するには  
  
1. レコード番号の生成で使用される計算を確認します。 レコード番号が含まれている変数、またはレコード番号の計算で使用される変数のスペルを確認します。 モジュールで `Option Explicit On` を使用しない限り、スペル ミスの変数名は暗黙的に宣言され、0 に初期化されます。  
  
## <a name="see-also"></a>関連項目

- [Option Explicit ステートメント](../language-reference/statements/option-explicit-statement.md)
