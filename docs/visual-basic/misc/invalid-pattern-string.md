---
title: 正しくないパターン文字列
ms.date: 07/20/2015
ms.assetid: ec1aecdb-5339-4a93-be71-eec56b1d7438
ms.openlocfilehash: aa408f4cecc2a2774cb98cba96cd04a67afcc546
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84402214"
---
# <a name="invalid-pattern-string"></a>正しくないパターン文字列
検索の `Like` 演算で指定されているパターン文字列が正しくありません。  
  
## <a name="to-correct-this-error"></a>このエラーを解決するには  
  
1. リスト式に使用できる文字を確認します。  
  
2. パターン範囲の指定で、 `[a-z]`のように、範囲の開始文字が終了文字より小さいことを確認します。  
  
3. パターン範囲の指定で、 `[a--z]`のように、複数のハイフンが続けて指定されていないことを確認します。  
  
4. パターン範囲を右角かっこで終了します。  
  
## <a name="see-also"></a>関連項目

- [Like 演算子](../language-reference/operators/like-operator.md)
