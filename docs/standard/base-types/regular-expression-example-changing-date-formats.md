---
title: '正規表現の例: 日付形式の変更'
ms.date: 06/30/2020
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- searching with regular expressions, examples
- parsing text with regular expressions, examples
- regular expressions, examples
- .NET Framework regular expressions, examples
- regular expressions [.NET Framework], examples
- pattern-matching with regular expressions, examples
ms.assetid: 5fcc75a5-09d7-45ae-a4c0-9ad6085ac83d
ms.openlocfilehash: 3b657ac6c88a1ee846f7f1d2156a18fd34621808
ms.sourcegitcommit: c23d9666ec75b91741da43ee3d91c317d68c7327
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85803951"
---
# <a name="regular-expression-example-changing-date-formats"></a>正規表現の例: 日付形式の変更
次のコード例では、<xref:System.Text.RegularExpressions.Regex.Replace%2A?displayProperty=nameWithType> メソッドを使用して、*mm*/*dd*/*yy* 形式の日付を *dd*-*mm*-*yy* 形式の日付に置き換えます。  

[!INCLUDE [regex](../../../includes/regex.md)]

## <a name="example"></a>例  
 [!code-csharp[RegularExpressions.Examples.ChangeDateFormats#1](../../../samples/snippets/csharp/VS_Snippets_CLR/RegularExpressions.Examples.ChangeDateFormats/cs/Example_ChangeDateFormats1.cs#1)]
 [!code-vb[RegularExpressions.Examples.ChangeDateFormats#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/RegularExpressions.Examples.ChangeDateFormats/vb/Example_ChangeDateFormats1.vb#1)]  
  
 次のコードは、アプリケーションで `MDYToDMY` メソッドを呼び出す方法を示しています。  
  
 [!code-csharp[RegularExpressions.Examples.ChangeDateFormats#2](../../../samples/snippets/csharp/VS_Snippets_CLR/RegularExpressions.Examples.ChangeDateFormats/cs/Example_ChangeDateFormats1.cs#2)]
 [!code-vb[RegularExpressions.Examples.ChangeDateFormats#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/RegularExpressions.Examples.ChangeDateFormats/vb/Example_ChangeDateFormats1.vb#2)]  
  
## <a name="comments"></a>コメント  
 この正規表現パターン `\b(?<month>\d{1,2})/(?<day>\d{1,2})/(?<year>\d{2,4})\b` の解釈を次の表に示します。  
  
|パターン|[説明]|  
|-------------|-----------------|  
|`\b`|ワード境界から照合を開始します。|  
|`(?<month>\d{1,2})`|1 桁または 2 桁の 10 進数と一致します。 これは、`month` キャプチャ グループです。|  
|`/`|スラッシュ マークと一致します。|  
|`(?<day>\d{1,2})`|1 桁または 2 桁の 10 進数と一致します。 これは、`day` キャプチャ グループです。|  
|`/`|スラッシュ マークと一致します。|  
|`(?<year>\d{2,4})`|2 ～ 4 の 10 進数と一致します。 これは、`year` キャプチャ グループです。|  
|`\b`|ワード境界で照合を終了します。|  
  
 パターン `${day}-${month}-${year}` は、次の表に示すように置換文字列を定義します。  
  
|パターン|[説明]|  
|-------------|-----------------|  
|`$(day)`|`day` キャプチャ グループによってキャプチャされた文字列を追加します。|  
|`-`|ハイフンを追加します。|  
|`$(month)`|`month` キャプチャ グループによってキャプチャされた文字列を追加します。|  
|`-`|ハイフンを追加します。|  
|`$(year)`|`year` キャプチャ グループによってキャプチャされた文字列を追加します。|  
  
## <a name="see-also"></a>参照

- [.NET の正規表現](regular-expressions.md)
