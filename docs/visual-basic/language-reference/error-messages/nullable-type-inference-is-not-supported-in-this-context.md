---
title: Null 許容型の推論はこのコンテキストではサポートされていません
ms.date: 07/20/2015
f1_keywords:
- vbc36629
- bc36629
helpviewer_keywords:
- BC36629
ms.assetid: 0a1e2dbc-d9a4-433d-9306-c5540782b81d
ms.openlocfilehash: 52e5391fbcf30a4dada4d64a0e810c900ea85806
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84409388"
---
# <a name="nullable-type-inference-is-not-supported-in-this-context"></a>Null 許容型の推論はこのコンテキストではサポートされていません
値の型と構造体は、Null 許容と宣言できます。  
  
```vb  
Dim a? As Integer  
Dim b As Integer?  
```  
  
 ただし、Null 許容の宣言を型の推定と組み合わせて使用することはできません。 次の例では、このエラーが発生します。  
  
```vb  
' Not valid.  
' Dim c? = 10  
' Dim d? = a  
```  
  
 **エラー ID:** BC36629  
  
## <a name="to-correct-this-error"></a>このエラーを解決するには  
  
- `As` 句を使用して、変数を null 許容値型として宣言します。  
  
## <a name="see-also"></a>関連項目

- [null 許容値型](../../programming-guide/language-features/data-types/nullable-value-types.md)
- [ローカル型の推論](../../programming-guide/language-features/variables/local-type-inference.md)
