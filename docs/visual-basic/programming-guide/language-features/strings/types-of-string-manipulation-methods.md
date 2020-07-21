---
title: 文字列操作メソッドの種類
ms.date: 07/20/2015
helpviewer_keywords:
- strings [Visual Basic], manipulating [Visual Basic]
- string manipulation
ms.assetid: 905055cd-7f50-48fb-9eed-b0995af1dc1f
ms.openlocfilehash: aba9af9c699cf8d07862c5d2967902bec1623500
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84363760"
---
# <a name="types-of-string-manipulation-methods-in-visual-basic"></a>Visual Basic における文字列操作メソッドの種類
文字列を分析および操作するには、いくつかの方法があります。 Visual Basic 言語の一部であるメソッドもあれば、`String` クラスに固有のメソッドもあります。  
  
## <a name="visual-basic-language-and-the-net-framework"></a>Visual Basic 言語と .NET Framework  
 Visual Basic のメソッドは、この言語の固有の関数として使用されます。 これらはコード内で修飾なしで使用できます。 次の例は、Visual Basic の文字列操作コマンドの一般的な使用方法を示しています。  
  
 [!code-vb[VbVbalrStrings#44](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStrings/VB/Class2.vb#44)]  
  
 この例では、`Mid` 関数は `aString` に対して直接操作を実行し、値を `bString` に割り当てます。  
  
 Visual Basic の文字列操作メソッドの一覧については、「[文字列操作の概要](../../../language-reference/keywords/string-manipulation-summary.md)」をご覧ください。  
  
### <a name="shared-methods-and-instance-methods"></a>共有メソッドとインスタンス メソッド  
 `String` クラスのメソッドを使用して、文字列を操作することもできます。 `String` には、"*共有*" メソッドと "*インスタンス*" メソッドの 2 種類のメソッドがあります。  
  
#### <a name="shared-methods"></a>共有メソッド  
 共有メソッドは、`String` クラス自体に由来するメソッドであり、このクラスのインスタンスが動作する必要はありません。 これらのメソッドは、`String` クラスのインスタンスではなく、クラスの名前 (`String`) で修飾できます。 次に例を示します。  
  
 [!code-vb[VbVbalrStrings#45](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStrings/VB/Class2.vb#45)]  
  
 上記の例では、<xref:System.String.Copy%2A?displayProperty=nameWithType> メソッドは静的メソッドであり、指定されている式に対して動作し、結果の値を `bString` に割り当てます。  
  
#### <a name="instance-methods"></a>インスタンス メソッド  
 インスタンス メソッドは、`String` の特定のインスタンスに由来し、インスタンス名で修飾する必要があります。 次に例を示します。  
  
 [!code-vb[VbVbalrStrings#46](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStrings/VB/Class2.vb#46)]  
  
 この例では、<xref:System.String.Substring%2A?displayProperty=nameWithType> メソッドは、`String` のインスタンス (つまり、`aString`) のメソッドです。 `aString` に対して操作を実行し、その値を `bString` に割り当てます。  
  
 詳細については、<xref:System.String> クラスのドキュメントをご覧ください。  
  
## <a name="see-also"></a>関連項目

- [Visual Basic の文字列の概要](introduction-to-strings.md)
