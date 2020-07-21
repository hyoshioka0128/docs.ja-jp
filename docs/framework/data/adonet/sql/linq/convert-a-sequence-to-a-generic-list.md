---
title: ジェネリック リストへのシーケンスの変換
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 7ab76d93-6898-4e75-b76f-290a66ecead8
ms.openlocfilehash: 43960d100cde7f746a56c023d305795e13bc04e7
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2019
ms.locfileid: "70247865"
---
# <a name="convert-a-sequence-to-a-generic-list"></a>ジェネリック リストへのシーケンスの変換
シーケンスからジェネリック リストを作成するには、<xref:System.Linq.Enumerable.ToList%2A> を使用します。  
  
## <a name="example"></a>例  
 次のサンプルでは、<xref:System.Linq.Enumerable.ToList%2A> を使用して、クエリを直ちにジェネリック <xref:System.Collections.Generic.List%601> に評価します。  
  
 [!code-csharp[DLinqQueryExamples#45](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#45)]
 [!code-vb[DLinqQueryExamples#45](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#45)]  
  
## <a name="see-also"></a>関連項目

- [クエリの例](query-examples.md)
