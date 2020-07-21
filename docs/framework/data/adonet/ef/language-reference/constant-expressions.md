---
title: 定数式
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 9d98a7be-b110-4edb-8eba-bed10f250b6d
ms.openlocfilehash: b31cd881f1307ec734c026d3c873d7a650e19a20
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2019
ms.locfileid: "70251134"
---
# <a name="constant-expressions"></a>定数式
定数式は、定数値で構成されています。 定数値は、クライアント側で変換されることなく、コマンド ツリーの定数式に直接変換されます。 これには、定数値になる式が含まれます。 したがって、定数にかかわるすべての式でデータ ソースの動作が、予期したとおりになります。 これは CLR の動作とは異なる結果となります。  
  
 次の例では、サーバーで評価される定数式を示します。  
  
 [!code-csharp[DP L2E Conceptual Examples#ConstantExpression](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Conceptual Examples/CS/Program.cs#constantexpression)]
 [!code-vb[DP L2E Conceptual Examples#ConstantExpression](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#constantexpression)]  
  
 LINQ to Entities では、ユーザー クラスを定数として使用することはできません。 ただし、ユーザー クラスのプロパティ参照は定数と見なされます。そのため、コマンド ツリーの定数式に変換され、データ ソースで実行されます。  
  
## <a name="see-also"></a>関連項目

- [LINQ to Entities クエリ内の式](expressions-in-linq-to-entities-queries.md)
