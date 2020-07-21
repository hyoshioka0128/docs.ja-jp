---
title: 正規関数
ms.date: 03/30/2017
ms.assetid: bbcc9928-36ea-4dff-9e31-96549ffed958
ms.openlocfilehash: f8ca9e2027e82db89e91287fda02d2014d53f325
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2019
ms.locfileid: "70854516"
---
# <a name="canonical-functions"></a>正規関数
このセクションでは、すべてのデータ プロバイダーがサポートし、あらゆるクエリ テクノロジで使用されている正規関数について説明します。 正規関数は、プロバイダーが拡張することはできません。  
  
 これらの正規関数は、プロバイダーの対応するデータ ソース機能に変換されます。 これによって、全データ ソースに共通する形式で表現される関数を呼び出すことができます。  
  
 これらの正規関数はデータ ソースから独立しているため、正規関数の引数の型と戻り値の型は、概念モデルの型の語句で定義されます。 ただし、データ ソースの中には概念モデルのすべての型をサポートしていないものもあります。  
  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] クエリで正規関数を使用すると、適切な関数がデータ ソースで呼び出されます。  
  
 すべての正規関数は、NULL が入力された場合の動作と明示的に指定されたエラー状況の両方を含んでいます。 ストア プロバイダーはその動作に従う必要がありますが、Entity Framework にはこの動作が適用されません。  
  
 LINQ のシナリオの場合、Entity Framework に対するクエリでは、基になるデータ ソース内のメソッドへの CLR メソッドのマッピングも行われます。 特定の一連のメソッドが適切にマップされるように、CLR メソッドはデータ ソースに関係なく正規関数にマップされます。  
  
## <a name="canonical-functions-namespace"></a>正規関数の名前空間  
 正規関数の名前空間は <xref:System.Data.Metadata.Edm> です。 <xref:System.Data.Metadata.Edm> 名前空間は、自動的にすべてのクエリに含まれます。 ただし、<xref:System.Data.Metadata.Edm> 名前空間に正規関数と同じ名前の関数を含む別の名前空間がインポートされている場合は、名前空間を指定する必要があります。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [集計正規関数](aggregate-canonical-functions.md)  
 集計 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 正規関数について説明します。  
  
 [数値演算正規関数](math-canonical-functions.md)  
 数学 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 正規関数について説明します。  
  
 [文字列正規関数](string-canonical-functions.md)  
 文字列 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 正規関数について説明します。  
  
 [日付と時刻の正規関数](date-and-time-canonical-functions.md)  
 日付および時刻の [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 正規関数について説明します。  
  
 [ビット単位の正規関数](bitwise-canonical-functions.md)  
 ビット単位の [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 正規関数について説明します。  
  
 [空間関数](spatial-functions.md)  
 空間に関する [!INCLUDE[esql](../../../../../../includes/esql-md.md)] の正規関数について説明します。  
  
 [その他の正規関数](other-canonical-functions.md)  
 ビット単位、日付/時刻、文字列、数学、または集計に分類されない関数について説明します。  
  
## <a name="see-also"></a>関連項目

- [Entity SQL の概要](entity-sql-overview.md)
- [Entity SQL リファレンス](entity-sql-reference.md)
- [概念モデル正規関数と SQL Server 関数とのマッピング](../conceptual-model-canonical-to-sql-server-functions-mapping.md)
- [ユーザー定義関数](user-defined-functions-entity-sql.md)
