---
title: 0 から始まる文字列アクセスと1 から始まる文字列アクセスの比較
ms.date: 07/20/2015
helpviewer_keywords:
- strings [Visual Basic], indexing
ms.assetid: 0ed39f35-d68e-421d-ae14-460a5c0373b8
ms.openlocfilehash: ce2fcb2610c09a9591a5fd79da4baa74cc533c99
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84363657"
---
# <a name="zero-based-vs-one-based-string-access-in-visual-basic"></a>0 から始まる文字列アクセスと1 から始まる文字列アクセスの比較 (Visual Basic)
このトピックでは、Visual Basic と .NET Framework が文字列内の文字へのアクセスを提供する方法を比較します。 .NET Framework では、文字列内の文字にアクセスする際に、常に 0 から始まるアクセスが提供されます。一方、Visual Basic では、関数に応じて、0 から始まるアクセスと 1 から始まるアクセスが提供されます。  
  
## <a name="one-based"></a>1 から開始  
 1 から始まる Visual Basic 関数の例として、`Mid` 関数について考えてみましょう。 これは、位置 1 から始めて、部分文字列が始まる文字位置を示す引数を受け取ります。 .NET Framework の <xref:System.String.Substring%2A?displayProperty=nameWithType> メソッドは、位置 0 から始めて、文字列内の部分文字列が始まる文字のインデックスを受け取ります。 したがって、文字列 "ABCDE" がある場合、個々の文字に付けられる番号は、`Mid` 関数で使用する際には 1,2,3,4,5 ですが、<xref:System.String.Substring%2A?displayProperty=nameWithType> メソッドで使用する際には 0,1,2,3,4 になります。  
  
## <a name="zero-based"></a>0 から開始  
 0 から始まる Visual Basic 関数の例として、`Split` 関数について考えてみましょう。 これは、文字列を分割し、部分文字列を含む配列を返します。 .NET Framework の <xref:System.String.Split%2A?displayProperty=nameWithType> メソッドも文字列を分割し、部分文字列を含む配列を返します。 `Split` 関数と <xref:System.String.Split%2A> メソッドは .NET Framework の配列を返すため、これらは 0 から始まる必要があります。  
  
## <a name="see-also"></a>関連項目

- <xref:Microsoft.VisualBasic.Strings.Mid%2A>
- <xref:Microsoft.VisualBasic.Strings.Split%2A>
- <xref:System.String.Substring%2A>
- <xref:System.String.Split%2A>
- [Visual Basic の文字列の概要](introduction-to-strings.md)
