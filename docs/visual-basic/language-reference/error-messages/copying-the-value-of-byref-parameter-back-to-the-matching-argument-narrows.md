---
title: "'ByRef' パラメーター '<parametername>' の値を一致する引数へ戻してコピーすると、型 '<typename1>' から型 '<typename2>' に下位変換します"
ms.date: 07/20/2015
f1_keywords:
- bc32053
- vbc32053
helpviewer_keywords:
- BC32053
ms.assetid: 281564b7-99f7-451f-b10d-f985e831bb25
ms.openlocfilehash: bac5f9a88df719bc64a8b0541f65e5912275866e
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84409752"
---
# <a name="copying-the-value-of-byref-parameter-parametername-back-to-the-matching-argument-narrows-from-type-typename1-to-type-typename2"></a>'ByRef' パラメーター '\<parametername>' の値を一致する引数へ戻してコピーすると、型 '\<typename1>' から型 '\<typename2>' に下位変換します
対応するパラメーターの型に拡大変換する引数でプロシージャが呼び出され、パラメーターから引数への変換が縮小されます。  
  
 クラスまたは構造体を定義するときは、そのクラスまたは構造体の型を他の型に変換する 1 つまたは複数の変換演算子を定義できます。 その他の型をクラスまたは構造体の型に変換する逆の変換演算子を定義することもできます。 プロシージャ呼び出しでクラスまたは構造体の型を使用すると、Visual Basic ではこれらの変換演算子を使用して、引数の型を、対応するパラメーターの型に変換できます。  
  
 引数 [ByRef](../modifiers/byref.md) を渡した場合、Visual Basic では参照を渡す代わりに、引数の値をプロシージャのローカル変数にコピーすることがあります。 このような場合は、プロシージャから戻るときに、Visual Basic で呼び出し元のコードの引数にローカル変数の値をコピーする必要があります。  
  
 `ByRef` 引数の値がプロシージャにコピーされ、引数とパラメーターが同じ型である場合、変換は必要ありません。 型が異なる場合、Visual Basic では双方向で変換する必要があります。 型のいずれかがクラスまたは構造体の型の場合、Visual Basic ではその型を他の型との間で変換する必要があります。 これらの変換のいずれかが拡大変換している場合、逆変換では縮小変換される可能性があります。  
  
 **エラー ID:** BC32053  
  
## <a name="to-correct-this-error"></a>このエラーを解決するには  
  
- 可能な場合は、プロシージャのパラメーターと同じ型の呼び出し元の引数を使用して、Visual Basic で変換する必要がないようにします。  
  
- パラメーター型とは異なる引数型を使用してプロシージャを呼び出す必要があり、呼び出し元の引数に値を返す必要がない場合は、 [ByRef](../modifiers/byval.md) ではなく `ByRef`になるようにパラメーターを定義します。  
  
- 呼び出し元の引数に値を返す必要がある場合は、可能であれば[拡大変換](../modifiers/widening.md)として、逆変換演算子を定義します。  
  
## <a name="see-also"></a>関連項目

- [手順](../../programming-guide/language-features/procedures/index.md)
- [プロシージャのパラメーターと引数](../../programming-guide/language-features/procedures/procedure-parameters-and-arguments.md)
- [引数の値渡しと参照渡し](../../programming-guide/language-features/procedures/passing-arguments-by-value-and-by-reference.md)
- [演算子プロシージャ](../../programming-guide/language-features/procedures/operator-procedures.md)
- [Operator ステートメント](../statements/operator-statement.md)
- [方法: 演算子を定義する](../../programming-guide/language-features/procedures/how-to-define-an-operator.md)
- [方法: 変換演算子を定義する](../../programming-guide/language-features/procedures/how-to-define-a-conversion-operator.md)
- [Visual Basic における型変換](../../programming-guide/language-features/data-types/type-conversions.md)
- [拡大変換と縮小変換](../../programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)
