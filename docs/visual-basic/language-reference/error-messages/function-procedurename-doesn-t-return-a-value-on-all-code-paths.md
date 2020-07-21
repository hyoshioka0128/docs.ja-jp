---
title: 関数 '<procedurename>' すべてのコード パス上では値を返しません。
ms.date: 07/20/2015
f1_keywords:
- bc42105
- vbc42105
helpviewer_keywords:
- BC42105
ms.assetid: b6929bf4-a365-4a70-8dc9-6b0fc09e1468
ms.openlocfilehash: edb2195f4e83c2315aa929936aff8af88ca8556c
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84374136"
---
# <a name="function-procedurename-doesnt-return-a-value-on-all-code-paths"></a>関数 '\<procedurename>' すべてのコード パス上では値を返しません。
関数 '\<procedurename>' がすべてのコード パス上では値を返しません。 'return' ステートメントが不足していませんか。  
  
 `Function` プロシージャに、値を返さないコードのパスが少なくとも 1 つ含まれています。  
  
 次のいずれかの方法で、`Function` プロシージャから値を返すことができます。  
  
- [return ステートメント](../statements/return-statement.md)に値を含めます。  
  
- `Function` プロシージャ名に値を代入して、`Exit Function` ステートメントを実行します。  
  
- `Function` プロシージャ名に値を代入して、`End Function` ステートメントを実行します。  
  
 制御が `Exit Function` または `End Function` に渡され、プロシージャ名に何も値を代入していない場合、プロシージャでは、戻り値のデータ型の既定値が返されます。 詳細については、「[Function ステートメント](../statements/function-statement.md)」の "動作" に関する記述を参照してください。  
  
 既定では、このメッセージは警告です。 警告を非表示にする方法や、警告をエラーとして扱う方法の詳細については、「 [Configuring Warnings in Visual Basic](/visualstudio/ide/configuring-warnings-in-visual-basic)」を参照してください。  
  
 **エラー ID:** BC42105  
  
## <a name="to-correct-this-error"></a>このエラーを解決するには  
  
- 制御フロー ロジックをチェックし、戻り値を返すすべてのステートメントの前に値を代入してください。  
  
     常に `Return` ステートメントを使用すれば、プロシージャからのすべての戻り値で、値が返されることを簡単に保証できます。 これを実行する場合、`End Function` の前の最後のステートメントは、`Return` ステートメントでなければなりません。  
  
## <a name="see-also"></a>関連項目

- [Function プロシージャ](../../programming-guide/language-features/procedures/function-procedures.md)
- [Function ステートメント](../statements/function-statement.md)
- [[コンパイル] ページ、プロジェクト デザイナー (Visual Basic)](/visualstudio/ide/reference/compile-page-project-designer-visual-basic)
