---
title: '方法: 文字列内を検索する-Visual Basic'
ms.date: 07/20/2015
helpviewer_keywords:
- strings [Visual Basic], finding
- strings [Visual Basic], searching
- examples [Visual Basic], strings
ms.assetid: ae4c79e0-08ea-489f-bdb2-5eb6d355f284
ms.openlocfilehash: fe9e50dc5458fdf8546094e5f41c2f001f1d2791
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/01/2019
ms.locfileid: "71700061"
---
# <a name="how-to-search-within-a-string-visual-basic"></a>方法: 文字列内を検索する (Visual Basic)

この記事では、Visual Basic 内の文字列内で検索する方法の例を示します。

## <a name="example"></a>例

この例では、<xref:System.String> オブジェクトの <xref:System.String.IndexOf%2A> メソッドを呼び出して、部分文字列が最初に見つかった位置のインデックスを報告します。

 [!code-vb[VbVbalrStrings#71](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStrings/VB/Class2.vb#71)]

## <a name="robust-programming"></a>信頼性の高いプログラミング

@No__t-0 メソッドは、最初に見つかった部分文字列の最初の文字の位置を返します。 インデックスは0から始まる値です。つまり、文字列の最初の文字のインデックスは0になります。

@No__t-0 が部分文字列を検出しなかった場合は、-1 を返します。

@No__t-0 メソッドでは大文字と小文字が区別され、現在のカルチャが使用されます。

最適なエラーに制御するために文字列の検索をする可能性があります、`Try`のブロックを[Try...Catch...Finally ステートメント](../../../language-reference/statements/try-catch-finally-statement.md)構築します。

## <a name="see-also"></a>関連項目

- <xref:System.String.IndexOf%2A>
- [Try...Catch...Finally ステートメント](../../../language-reference/statements/try-catch-finally-statement.md)
- [Visual Basic の文字列の概要](introduction-to-strings.md)
- [文字列](index.md)
