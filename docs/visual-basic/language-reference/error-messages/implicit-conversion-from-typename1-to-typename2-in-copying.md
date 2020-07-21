---
title: "'ByRef' パラメーター '<typename1>' の値を、一致する引数に戻してコピーする際の、'<typename2>' から '<parametername>' への暗黙的な変換です。"
ms.date: 07/20/2015
f1_keywords:
- vbc41999
- bc41999
helpviewer_keywords:
- BC41999
ms.assetid: ae48c738-dff8-4c0f-8931-bbb70b2c8b03
ms.openlocfilehash: 4d0f9aac795f683cf58210ea38b3783e451ccfc3
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84402863"
---
# <a name="implicit-conversion-from-typename1-to-typename2-in-copying-the-value-of-byref-parameter-parametername-back-to-the-matching-argument"></a>'ByRef' パラメーター '\<typename1>' の値を、一致する引数に戻してコピーする際の、'\<typename2>' から '\<parametername>' への暗黙的な変換です。
プロシージャが、対応するパラメーターとは異なる型の [ByRef](../modifiers/byref.md) 引数を指定して呼び出されました。  
  
 引数 `ByRef` を渡した場合、Visual Basic は参照を渡す代わりに、引数の値をプロシージャのローカル変数にコピーすることがあります。 このような場合は、プロシージャから戻るときに、Visual Basic で呼び出し元のコードの引数にローカル変数の値をコピーする必要があります。  
  
 `ByRef` 引数の値がプロシージャにコピーされ、引数とパラメーターが同じ型である場合、変換は必要ありません。 型が異なる場合、Visual Basic では双方向で変換する必要があります。 プロシージャの引数またはパラメーターで `CType` または他の変換キーワードを使用することはできないため、このような変換は常に暗黙的です。  
  
 既定では、このメッセージは警告です。 警告を非表示にする方法や、警告をエラーとして扱う方法の詳細については、「 [Configuring Warnings in Visual Basic](/visualstudio/ide/configuring-warnings-in-visual-basic)」をご覧ください。  
  
 **エラー ID:** BC41999  
  
## <a name="to-correct-this-error"></a>このエラーを解決するには  
  
- 可能な場合は、プロシージャのパラメーターと同じ型の呼び出し元の引数を使用して、Visual Basic で変換する必要がないようにします。  
  
- パラメーター型とは異なる引数型を使用してプロシージャを呼び出す必要があり、呼び出し元の引数に値を返す必要がない場合は、 [ByRef](../modifiers/byval.md) ではなく `ByRef`になるようにパラメーターを定義します。  
  
## <a name="see-also"></a>関連項目

- [手順](../../programming-guide/language-features/procedures/index.md)
- [プロシージャのパラメーターと引数](../../programming-guide/language-features/procedures/procedure-parameters-and-arguments.md)
- [引数の値渡しと参照渡し](../../programming-guide/language-features/procedures/passing-arguments-by-value-and-by-reference.md)
- [暗黙の型変換と明示的な型変換](../../programming-guide/language-features/data-types/implicit-and-explicit-conversions.md)
