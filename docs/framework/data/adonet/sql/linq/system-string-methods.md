---
title: System.String メソッド
ms.date: 03/30/2017
ms.assetid: ce307f14-87e6-4816-8694-8a4147f6b784
ms.openlocfilehash: 583c0d58562c1605f24b61489d481e19248ebed4
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2019
ms.locfileid: "70792496"
---
# <a name="systemstring-methods"></a>System.String メソッド
[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] は、次の <xref:System.String> メソッドをサポートしていません。  
  
## <a name="unsupported-systemstring-methods-in-general"></a>サポートされていない一般的な System.String メソッド  
 サポートされていない一般的な <xref:System.String> メソッドは次のとおりです。  
  
- カルチャを認識するオーバーロード (`CultureInfo`、`StringComparison`、`IFormatProvider` を受け取るメソッド)  
  
- `char` 配列を受け取るまたは生成するメソッド  
  
## <a name="unsupported-systemstring-static-methods"></a>サポートされていない System.String 静的メソッド  
  
|サポートされていない System.String 静的メソッド|  
|----------------------------------------------|  
|<xref:System.String.Copy%28System.String%29?displayProperty=nameWithType>|  
|<xref:System.String.Compare%28System.String%2CSystem.String%2CSystem.Boolean%29?displayProperty=nameWithType>|  
|<xref:System.String.Compare%28System.String%2CSystem.String%2CSystem.Boolean%2CSystem.Globalization.CultureInfo%29?displayProperty=nameWithType>|  
|<xref:System.String.Compare%28System.String%2CSystem.Int32%2CSystem.String%2CSystem.Int32%2CSystem.Int32%29?displayProperty=nameWithType>|  
|<xref:System.String.Compare%28System.String%2CSystem.Int32%2CSystem.String%2CSystem.Int32%2CSystem.Int32%2CSystem.Boolean%29?displayProperty=nameWithType>|  
|<xref:System.String.Compare%28System.String%2CSystem.Int32%2CSystem.String%2CSystem.Int32%2CSystem.Int32%2CSystem.Boolean%2CSystem.Globalization.CultureInfo%29?displayProperty=nameWithType>|  
|<xref:System.String.CompareOrdinal%28System.String%2CSystem.String%29?displayProperty=nameWithType>|  
|<xref:System.String.CompareOrdinal%28System.String%2CSystem.Int32%2CSystem.String%2CSystem.Int32%2CSystem.Int32%29?displayProperty=nameWithType>|  
|<xref:System.String.Format%2A?displayProperty=nameWithType>|  
|<xref:System.String.Join%2A?displayProperty=nameWithType>|  
  
## <a name="unsupported-systemstring-non-static-methods"></a>サポートされていない System.String 非静的メソッド  
  
|サポートされていない System.String 非静的メソッド|  
|---------------------------------------------------|  
|<xref:System.String.IndexOfAny%28System.Char%5B%5D%29?displayProperty=nameWithType>|  
|<xref:System.String.Split%2A?displayProperty=nameWithType>|  
|<xref:System.String.ToCharArray?displayProperty=nameWithType>|  
|<xref:System.String.ToUpper%28System.Globalization.CultureInfo%29?displayProperty=nameWithType>|  
|<xref:System.String.TrimEnd%28System.Char%5B%5D%29?displayProperty=nameWithType>|  
|<xref:System.String.TrimStart%28System.Char%5B%5D%29?displayProperty=nameWithType>|  
  
## <a name="differences-from-net"></a>.NET との相違  
  
- SQL Server で有効にされている照合順序があっても、クエリには適用されません。したがって、既定では、カルチャ依存で大文字と小文字を区別しない比較が行われます。 この動作は、大文字と小文字を区別する .NET Framework の既定の動作とは異なります。  
  
- `LastIndexOf` から 0 が返された場合は、文字列が `NULL` であるか、または見つかった位置が 0 であることを示します。  
  
- 固定長文字列 (`CHAR`、`NCHAR`) では、データベースにおいて自動的に埋め込みが適用されるため、連結やその他の操作で予期しない結果が生じることがあります。  
  
- `Replace` 列、`ToLower` 列、および XML では、`ToUpper`、`TEXT`、`NTEXT` などの多くのメソッドや文字インデクサーで有効な変換が用意されていないため、通常の変換を行おうとすると `SqlExceptions` が発生します。 これらの型については、これが適切な動作と見なされます。 ただし、`VARCHAR`、`NVARCHAR`、`VARCHAR(max)`、および `NVARCHAR(max)` については、すべての文字列操作が共通言語ランタイム (CLR: Common Language Runtime) のセマンティクと一致している必要があります。  
  
## <a name="see-also"></a>関連項目

- [データ型と関数](data-types-and-functions.md)
