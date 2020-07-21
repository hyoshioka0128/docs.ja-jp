---
title: 引数 'Period' は 'Life' 引数以下でなければなりません
ms.date: 07/20/2015
f1_keywords:
- vbrFinancial_PeriodLELife
ms.assetid: dc575d41-b376-4b05-bbbe-6de1e98385f1
ms.openlocfilehash: 0b20bb1fd1c0954e30262dd3a3b43d145226b7cc
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84367725"
---
# <a name="argument-period-must-be-less-than-or-equal-to-argument-life"></a>引数 'Period' は 'Life' 引数以下でなければなりません
資産の減価償却費計算の対象期間を指定する `Period` 引数の値が `Life` 引数の値より大きくなっています。  
  
## <a name="to-correct-this-error"></a>このエラーを解決するには  
  
- `Life` 引数と `Period` 引数の両方が同じ単位で指定されていることを確認します。 たとえば、 `Life` を月単位で指定する場合は、 `Period` も月単位で指定します。  
  
## <a name="see-also"></a>関連項目

- [引数の値渡しと参照渡し](../programming-guide/language-features/procedures/passing-arguments-by-value-and-by-reference.md)
