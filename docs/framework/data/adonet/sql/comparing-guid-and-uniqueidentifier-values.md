---
title: GUID と uniqueidentifier 値の比較
description: .NET Framework Data Provider for SQL Server で GUID 値を作成して比較する方法について説明します。これらの値は、uniqueidentifier データ型で表現されます。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: aababd75-2335-43e3-ace8-4b7ae84191a8
ms.openlocfilehash: 245b7246712822043d302c43a765c29ac2090e00
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84286508"
---
# <a name="comparing-guid-and-uniqueidentifier-values"></a>GUID と uniqueidentifier 値の比較
SQL Server のグローバル一意識別子 (GUID: Globally Unique Identifier) データ型は、16 バイトのバイナリ値を格納する `uniqueidentifier` データ型で表現されます。 GUID はバイナリ数値であり、多くのサイトの多くのコンピューターがあるネットワーク内で一意にする必要がある識別子として主に使用されます。 GUID は、Transact-SQL NEWID 関数を呼び出して生成でき、全世界で一意であることが保証されます。 詳細については、「[uniqueidentifier (Transact-SQL)](/sql/t-sql/data-types/uniqueidentifier-transact-sql)」を参照してください。  
  
## <a name="working-with-sqlguid-values"></a>SqlGuid 値の使用  
 GUID の値は長くて不可解な値であるため、ユーザーには意味がわかりません。 キー値にランダムに生成された GUID を使用しており、大量の行を挿入した場合、インデックスにランダムな I/O が取り込まれるため、パフォーマンスが低下する可能性があります。 GUID はさらに、他のデータ型と比較すると比較的大きいものになります。 通常、GUID は、その他のデータ型が適さないような非常に限られた場合にのみ使用することをお勧めします。  
  
### <a name="comparing-guid-values"></a>GUID 値の比較  
 `uniqueidentifier` 型の値には比較演算子が使用できます。 ただし、順序付けは、2 つの値のビット パターンの比較によっては実装されません。 `uniqueidentifier` 値に対して実行可能な唯一の操作は、比較 (=、<>、\<, >、\<=, >=) と NULL の確認 (IS NULL および IS NOT NULL) です。 これ以外の算術演算子を使用することはできません。  
  
 <xref:System.Guid> と <xref:System.Data.SqlTypes.SqlGuid> はどちらにも、異なる GUID 値を比較するための `CompareTo` メソッドがあります。 ただし、`System.Guid.CompareTo` と `SqlTypes.SqlGuid.CompareTo` の実装方法は異なります。 <xref:System.Data.SqlTypes.SqlGuid> は SQL Server の動作を使用して `CompareTo` を実装し、値の最後の 6 バイトが最も重要になります。 <xref:System.Guid> は 16 バイトすべてを評価します。 次の例は、この動作の違いを示しています。 コードの最初のセクションは、並べ替えられていない <xref:System.Guid> 値を示しており、コードの 2 番目のセクションは並べ替えられた <xref:System.Guid> 値を示しています。 3 番目のセクションは、並べ替えられた <xref:System.Data.SqlTypes.SqlGuid> 値を示しています。 コード リストの下に出力を示しています。  
  
 [!code-csharp[DataWorks SqlTypes.Guid#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlTypes.Guid/CS/source.cs#1)]
 [!code-vb[DataWorks SqlTypes.Guid#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlTypes.Guid/VB/source.vb#1)]  
  
 この例を実行すると、次の結果が得られます。  
  
```output  
Unsorted Guids:  
3aaaaaaa-bbbb-cccc-dddd-2eeeeeeeeeee  
2aaaaaaa-bbbb-cccc-dddd-1eeeeeeeeeee  
1aaaaaaa-bbbb-cccc-dddd-3eeeeeeeeeee  
  
Sorted Guids:  
1aaaaaaa-bbbb-cccc-dddd-3eeeeeeeeeee  
2aaaaaaa-bbbb-cccc-dddd-1eeeeeeeeeee  
3aaaaaaa-bbbb-cccc-dddd-2eeeeeeeeeee  
  
Sorted SqlGuids:  
2aaaaaaa-bbbb-cccc-dddd-1eeeeeeeeeee  
3aaaaaaa-bbbb-cccc-dddd-2eeeeeeeeeee  
1aaaaaaa-bbbb-cccc-dddd-3eeeeeeeeeee  
```  
  
## <a name="see-also"></a>関連項目

- [SQL Server データ型と ADO.NET](sql-server-data-types.md)
- [ADO.NET の概要](../ado-net-overview.md)
