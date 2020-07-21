---
title: '方法: 文字列から無効な文字を取り除く'
description: 静的 Regex.Replace メソッドを使用して、文字列から害を及ぼす可能性のある文字を取り除く方法を示す例について確認します。
ms.date: 06/30/2020
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- regular expressions, examples
- cleaning input
- user input, examples
- .NET Framework regular expressions, examples
- regular expressions [.NET Framework], examples
- Regex.Replace method
- stripping invalid characters
- Replace method
- validating user input
ms.assetid: b4319c8a-9032-4129-a9d5-6f6fc28e7f32
ms.openlocfilehash: 5e0cd423df7fce03cdefb3da7bc192f3045e8f9c
ms.sourcegitcommit: c23d9666ec75b91741da43ee3d91c317d68c7327
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85803990"
---
# <a name="how-to-strip-invalid-characters-from-a-string"></a>方法: 文字列から無効な文字を取り除く
次の例では、静的 <xref:System.Text.RegularExpressions.Regex.Replace%2A?displayProperty=nameWithType> メソッドを使用して、文字列から無効な文字を取り除いています。  

[!INCLUDE [regex](../../../includes/regex.md)]

## <a name="example"></a>例  
 この例で定義されている `CleanInput` メソッドを使用して、ユーザー入力を受け付けるテキスト フィールドに入力された、問題を引き起こす可能性がある文字を削除することができます。 この場合、`CleanInput` は、ピリオド (.)、アット記号 (@)、ハイフン (-) を除く英数字以外のすべての文字を取り除き、残りの文字列を返します。 ただし、正規表現パターンを変更して、入力文字列に含めない任意の文字を取り除くこともできます。  
  
 [!code-csharp[RegularExpressions.Examples.StripChars#1](../../../samples/snippets/csharp/VS_Snippets_CLR/RegularExpressions.Examples.StripChars/cs/Example.cs#1)]
 [!code-vb[RegularExpressions.Examples.StripChars#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/RegularExpressions.Examples.StripChars/vb/Example.vb#1)]  
  
 正規表現パターン `[^\w\.@-]` は、単語に使用される文字、ピリオド、@ 記号、またはハイフンではないすべての文字に一致します。 単語に使用される文字とは、すべての英字、数字、または区切りのコネクタ文字 (アンダースコアなど) です。 このパターンに一致するすべての文字は、置換パターンで定義されている <xref:System.String.Empty?displayProperty=nameWithType> で置き換えられます。 ユーザー入力で他の文字も許可するには、正規表現パターンの文字クラスにその文字を追加します。 たとえば、正規表現パターン `[^\w\.@-\\%]` は、入力文字列にパーセント記号とバックスラッシュも許可しています。  
  
## <a name="see-also"></a>関連項目

- [.NET の正規表現](regular-expressions.md)
