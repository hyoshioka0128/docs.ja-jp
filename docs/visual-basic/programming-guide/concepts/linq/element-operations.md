---
title: 要素操作
ms.date: 07/20/2015
ms.assetid: 5fcb0631-dce5-45ff-8abb-353cae21e14f
ms.openlocfilehash: 73d8b5b308b4d1cb8863f38592647a71e62dd15a
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84375292"
---
# <a name="element-operations-visual-basic"></a>要素操作 (Visual Basic)
要素操作では、シーケンスから単一の特定の要素が返されます。  
  
 次のセクションでは、要素操作を実行する標準クエリ演算子のメソッドの一覧を示します。  
  
## <a name="methods"></a>メソッド  
  
|メソッド名|説明|Visual Basic のクエリ式の構文|説明|  
|-----------------|-----------------|------------------------------------------|----------------------|  
|ElementAt|コレクション内の指定されたインデックス位置にある要素を返します。|該当なし。|<xref:System.Linq.Enumerable.ElementAt%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.ElementAt%2A?displayProperty=nameWithType>|  
|ElementAtOrDefault|コレクション内の指定したインデックス位置にある要素を返します。インデックスが範囲外の場合は既定値を返します。|該当なし。|<xref:System.Linq.Enumerable.ElementAtOrDefault%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.ElementAtOrDefault%2A?displayProperty=nameWithType>|  
|First|コレクションの最初の要素、または条件を満たす最初の要素を返します。|該当なし。|<xref:System.Linq.Enumerable.First%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.First%2A?displayProperty=nameWithType>|  
|FirstOrDefault|コレクションの最初の要素、または条件を満たす最初の要素を返します。 そのような要素が存在しない場合は、既定値を返します。|該当なし。|<xref:System.Linq.Enumerable.FirstOrDefault%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.FirstOrDefault%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.FirstOrDefault%60%601%28System.Linq.IQueryable%7B%60%600%7D%29?displayProperty=nameWithType>|  
|末尾|コレクションの最後の要素、または条件を満たす最後の要素を返します。|該当なし。|<xref:System.Linq.Enumerable.Last%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.Last%2A?displayProperty=nameWithType>|  
|LastOrDefault|コレクションの最後の要素、または条件を満たす最後の要素を返します。 そのような要素が存在しない場合は、既定値を返します。|該当なし。|<xref:System.Linq.Enumerable.LastOrDefault%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.LastOrDefault%2A?displayProperty=nameWithType>|  
|Single|コレクションの唯一の要素、または条件を満たす唯一の要素を返します。|該当なし。|<xref:System.Linq.Enumerable.Single%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.Single%2A?displayProperty=nameWithType>|  
|SingleOrDefault|コレクションの唯一の要素、または条件を満たす唯一の要素を返します。 そのような要素が存在しない場合、またはコレクションの要素が 1 つだけでない場合は、既定値を返します。|該当なし。|<xref:System.Linq.Enumerable.SingleOrDefault%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.SingleOrDefault%2A?displayProperty=nameWithType>|  
  
## <a name="see-also"></a>関連項目

- <xref:System.Linq>
- [標準クエリ演算子の概要 (Visual Basic)](standard-query-operators-overview.md)
- [方法: ディレクトリ ツリー内で最もサイズの大きいファイルを照会する (LINQ) (Visual Basic)](how-to-query-for-the-largest-file-or-files-in-a-directory-tree.md)
