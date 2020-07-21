---
title: DLL を正しく呼び出せません。
ms.date: 07/20/2015
f1_keywords:
- vbrID49
ms.assetid: 7c7def45-b0ab-450f-ad3f-4383dfd9aed7
ms.openlocfilehash: a60e44ce92b1805b0a5a6f1d4ce397c295eef202
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84409882"
---
# <a name="bad-dll-calling-convention"></a>DLL を正しく呼び出せません。
ダイナミック リンク ライブラリ (DLL) に渡される引数は、ルーチンによって予期されるものと完全に一致する必要があります。 呼び出し規則は、引数の数、型、および順序を扱います。 プログラムが DLL 内のルーチンを呼び出しているときに、間違った型または数の引数が渡されている可能性があります。  
  
## <a name="to-correct-this-error"></a>このエラーを解決するには  
  
1. すべての引数の型が、呼び出しているルーチンの宣言で指定されている型と一致していることを確認します。  
  
2. 呼び出しているルーチンの宣言で指定したものと同じ数の引数を渡していることを確認します。  
  
3. DLL ルーチンが値渡しの引数を予期している場合は、ルーチンの宣言でこれらの引数に `ByVal` が指定されていることを確認します。  
  
## <a name="see-also"></a>関連項目

- [エラーの種類](../../programming-guide/language-features/error-types.md)
- [Call ステートメント](../statements/call-statement.md)
- [Declare ステートメント](../statements/declare-statement.md)
