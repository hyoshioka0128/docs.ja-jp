---
title: .NET での文字列の埋め込み
description: .NET で文字列を埋め込む方法について学習します。 先頭または末尾の文字を追加して指定した合計の長さを得るには、String.PadLeft と String.PadRight メソッドを使用します。
ms.date: 03/15/2018
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- strings [.NET Framework], padding
- white space
- PadRight method
- PadLeft method
- padding strings
ms.assetid: 84a9f142-3244-4c90-ba02-21af9bbaff71
ms.openlocfilehash: 5bf7023a3429e932a44ad0a0bd3409012f77cbf9
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84594531"
---
# <a name="padding-strings-in-net"></a>.NET での文字列の埋め込み

ある文字の先頭または末尾に文字を埋め込み、合計を指定の長さにするとき、元の文字列で構成される新しい文字列を次の <xref:System.String> メソッドの 1 つを利用して作成します。 埋め込み文字は、スペースまたは指定した文字にすることができます。 結果の文字列は右揃えまたは左揃えのように見えます。 元の文字列の長さが既に必要な合計の長さ以上である場合、埋め込みメソッドは元の文字列をそのまま返します。詳細については、<xref:System.String.PadLeft%2A?displayProperty=nameWithType> および <xref:System.String.PadRight%2A?displayProperty=nameWithType> メソッドの 2 つのオーバーロードの**戻り値**に関するセクションを参照してください。
  
|メソッド名|使用|  
|-----------------|---------|  
|<xref:System.String.PadLeft%2A?displayProperty=nameWithType>|文字列の先頭に文字を埋め込み、合計を指定の長さにします。|  
|<xref:System.String.PadRight%2A?displayProperty=nameWithType>|文字列の末尾に文字を埋め込み、合計を指定の長さにします。|  
  
## <a name="padleft"></a>PadLeft  
 <xref:System.String.PadLeft%2A?displayProperty=nameWithType> メソッドでは、元の文字列の先頭に埋め込み文字をつなげ、合計を指定の長さにすることで新しい文字列を作成します。 <xref:System.String.PadLeft%28System.Int32%29?displayProperty=nameWithType> メソッドでは、空白文字が埋め込み文字として利用されます。<xref:System.String.PadLeft%28System.Int32%2CSystem.Char%29?displayProperty=nameWithType> メソッドでは、独自の埋め込み文字を指定できます。  
  
 次のコード例では、<xref:System.String.PadLeft%2A> メソッドを利用し、長さが 20 文字の新しい文字列を作成します。 この例は、コンソールに "`--------Hello World!`" と出力します。  
  
 [!code-cpp[Conceptual.String.BasicOps#3](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.string.basicops/cpp/padding.cpp#3)]
 [!code-csharp[Conceptual.String.BasicOps#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.string.basicops/cs/padding.cs#3)]
 [!code-vb[Conceptual.String.BasicOps#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.string.basicops/vb/padding.vb#3)]  
  
## <a name="padright"></a>PadRight  
 <xref:System.String.PadRight%2A?displayProperty=nameWithType> メソッドでは、元の文字列の末尾に埋め込み文字をつなげ、合計を指定の長さにすることで新しい文字列を作成します。 <xref:System.String.PadRight%28System.Int32%29?displayProperty=nameWithType> メソッドでは、空白文字が埋め込み文字として利用されます。<xref:System.String.PadRight%28System.Int32%2CSystem.Char%29?displayProperty=nameWithType> メソッドでは、独自の埋め込み文字を指定できます。  
  
 次のコード例では、<xref:System.String.PadRight%2A> メソッドを利用し、長さが 20 文字の新しい文字列を作成します。 この例は、コンソールに "`Hello World!--------`" と出力します。  
  
 [!code-cpp[Conceptual.String.BasicOps#4](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.string.basicops/cpp/padding.cpp#4)]
 [!code-csharp[Conceptual.String.BasicOps#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.string.basicops/cs/padding.cs#4)]
 [!code-vb[Conceptual.String.BasicOps#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.string.basicops/vb/padding.vb#4)]  
  
## <a name="see-also"></a>関連項目

- [基本的な文字列操作](basic-string-operations.md)
