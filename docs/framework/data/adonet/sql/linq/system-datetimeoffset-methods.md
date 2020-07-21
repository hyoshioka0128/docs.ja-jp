---
title: System.DateTimeOffset メソッド
ms.date: 03/30/2017
ms.assetid: 25b3e5c0-7603-4a70-b3e5-2149e3da69a2
ms.openlocfilehash: 2e29cf02d4f7e8004782264bf940bb1faf393269
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2019
ms.locfileid: "70781549"
---
# <a name="systemdatetimeoffset-methods"></a>System.DateTimeOffset メソッド
オブジェクト モデルまたは外部マッピング ファイルにマッピングされると、<xref:System.DateTimeOffset?displayProperty=nameWithType> メソッド、演算子、プロパティのほとんどを LINQ to SQL のクエリ内から呼び出すことができます。  
  
 サポートされていないメソッドは、<xref:System.Object?displayProperty=nameWithType>、`Finalize`、`GetHashCode`、`GetType` など、LINQ to SQL クエリ内のコンテキストで意味を持たない `MemberwiseClone` から継承されたメソッドだけです。 これらのメソッドは LINQ to SQL で変換して SQL Server で実行することができないため、サポートされていません。  
  
> [!NOTE]
> 共通言語ランタイム (CLR) の <xref:System.DateTimeOffset?displayProperty=nameWithType> 構造体、およびそれを LINQ to SQL で SQL の `DATETIMEOFFSET` 列にマッピングする機能を使用するには、.NET Framework 3.5 SP1 以降が必要です。 SQL の `DATETIMEOFFSET` 列は、Microsoft SQL Server 2008 以降でのみ使用できます。  
  
## <a name="sqlmethods-date-and-time-methods"></a>SQLMethods の日付と時刻のメソッド  
 LINQ to SQL では、<xref:System.DateTimeOffset> 構造体で提供されるメソッドの他に、次の表に示すように、日付と時刻を操作する <xref:System.Data.Linq.SqlClient.SqlMethods?displayProperty=nameWithType> クラスのメソッドも提供しています。  
  
||||  
|-|-|-|  
|<xref:System.Data.Linq.SqlClient.SqlMethods.DateDiffDay%2A>|<xref:System.Data.Linq.SqlClient.SqlMethods.DateDiffMillisecond%2A>|<xref:System.Data.Linq.SqlClient.SqlMethods.DateDiffNanosecond%2A>|  
|<xref:System.Data.Linq.SqlClient.SqlMethods.DateDiffHour%2A>|<xref:System.Data.Linq.SqlClient.SqlMethods.DateDiffMinute%2A>|<xref:System.Data.Linq.SqlClient.SqlMethods.DateDiffSecond%2A>|  
|<xref:System.Data.Linq.SqlClient.SqlMethods.DateDiffMicrosecond%2A>|<xref:System.Data.Linq.SqlClient.SqlMethods.DateDiffMonth%2A>|<xref:System.Data.Linq.SqlClient.SqlMethods.DateDiffYear%2A>|  
  
## <a name="see-also"></a>関連項目

- [クエリの概念](query-concepts.md)
- [オブジェクト モデルの作成](creating-the-object-model.md)
- [SQL と CLR の型マッピング](sql-clr-type-mapping.md)
