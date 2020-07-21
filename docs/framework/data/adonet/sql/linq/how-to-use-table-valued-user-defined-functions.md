---
title: '方法: テーブル値のユーザー定義関数を使用する'
description: これらの例を使用して、1 つの行セットを返すテーブル値関数を作成する方法を学習します。 テーブルと同じように、このようなテーブル値関数を使用します。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 5a4ae2b4-3290-4aa1-bc95-fc70c51b54cf
ms.openlocfilehash: 44866367393e321d7dd2db965e2fad8a2e6b63e9
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84286327"
---
# <a name="how-to-use-table-valued-user-defined-functions"></a>方法: テーブル値のユーザー定義関数を使用する
テーブル値関数は、単一の行セットを返します (複数の結果形状を返すことができるストアド プロシージャとは異なります)。 テーブル値関数の戻り値の型は `Table` であるため、テーブルを使用できる SQL の任意の場所でテーブル値関数を使用できます。 テーブル値関数をテーブルのように扱うこともできます。  
  
## <a name="example"></a>例  
 次の SQL 関数は、`TABLE` を返すことを明示的に示しています。 そのため、返される行セットの構造が暗黙的に定義されます。  
  
```sql
CREATE FUNCTION ProductsCostingMoreThan(@cost money)  
RETURNS TABLE  
AS  
RETURN  
    SELECT ProductID, UnitPrice  
    FROM Products  
    WHERE UnitPrice > @cost  
```  
  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] は、関数を次のように割り当てます。  
  
 [!code-csharp[DLinqUDFS#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqUDFS/cs/northwind-tfunc.cs#1)]
 [!code-vb[DLinqUDFS#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqUDFS/vb/northwind-tfunc.vb#1)]  
  
## <a name="example"></a>例  
 次の SQL コードは、関数が返すテーブルに結合できることを示しており、それ以外の場合は、他のテーブルと同じように扱います。  
  
```sql
SELECT p2.ProductName, p1.UnitPrice  
FROM dbo.ProductsCostingMoreThan(80.50)  
AS p1 INNER JOIN Products AS p2 ON p1.ProductID = p2.ProductID  
```  
  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] では、クエリは次のように表示されます。  
  
 [!code-csharp[DLinqUDFS#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqUDFS/cs/Program.cs#2)]
 [!code-vb[DLinqUDFS#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqUDFS/vb/Module1.vb#2)]  
  
## <a name="see-also"></a>関連項目

- [ユーザー定義関数](user-defined-functions.md)
