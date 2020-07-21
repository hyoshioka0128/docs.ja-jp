---
title: ORDER BY (Entity SQL)
ms.date: 03/30/2017
ms.assetid: c0b61572-ecee-41eb-9d7f-74132ec8a26c
ms.openlocfilehash: 1233971b172079aa48227d0ec520068afbdf0952
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79150070"
---
# <a name="order-by-entity-sql"></a>ORDER BY (Entity SQL)
SELECT ステートメントで返されるオブジェクトで使用される並べ替え順を指定します。  
  
## <a name="syntax"></a>構文  
  
```sql  
[ ORDER BY
   {  
      order_by_expression [SKIP n] [LIMIT n]  
      [ COLLATE collation_name ]  
      [ ASC | DESC ]  
   }  
   [ ,…n ]
]  
```  
  
## <a name="arguments"></a>引数  
 `order_by_expression`  
 並べ替えるプロパティを指定する有効なクエリ式。 並べ替えのキーとなる式を複数指定できます。 ORDER BY 句内に記述するキー式の並び順によって、並べ替えられた結果セットの構成が決まります。  
  
 COLLATE {collation_name}  
 ORDER BY 操作が `collation_name`で指定された照合順序に従って実行されることを指定します。 COLLATE は文字列式にのみ適用できます。  
  
 ASC  
 指定したプロパティの値が昇順、つまり小さい値から大きい値へと並べ替えられます。 既定値です。  
  
 DESC  
 指定したプロパティの値が降順、つまり大きい値から小さい値へと並べ替えられます。  
  
 LIMIT `n`  
 最初の `n` 個の項目のみが選択されます。  
  
 SKIP `n`  
 最初の `n` 個の項目をスキップします。  
  
## <a name="remarks"></a>Remarks  
 ORDER BY 句は、SELECT 句の結果に論理的に適用されます。 ORDER BY 句では、別名を使用して選択リストの項目を参照できます。 ORDER BY 句は、現在スコープ内にあるその他の変数も参照できます。 ただし、SELECT 句が DISTINCT 修飾子で指定されている場合は、ORDER BY 句は SELECT 句の別名のみを参照できます。  
  
 `SELECT c AS c1 FROM cs AS c ORDER BY c1.e1, c.e2`  
  
 ORDER BY 句内の各式は、順序付けられた不等号 (より小さい、より大きいなど) について比較できる型として評価される必要があります。 通常、これらの型は数値、文字列、日付などのスカラー プリミティブです。 比較できる型の RowType は順序も比較できます。  
  
 順序付けされたセットで、最上位の投影を除きコードが反復処理を行う場合、出力でその順序が維持されることは保証されません。  

次の例では、順序が維持されることが保証されます。

```sql  
SELECT C1.FirstName, C1.LastName  
        FROM AdventureWorks.Contact as C1  
        ORDER BY C1.LastName  
```  

次のクエリでは、入れ子になったクエリの順序は無視されます。  

```sql  
SELECT C2.FirstName, C2.LastName  
    FROM (SELECT C1.FirstName, C1.LastName  
        FROM AdventureWorks.Contact as C1  
        ORDER BY C1.LastName) as C2  
```  
  
 UNION、UNION ALL、EXCEPT、または INTERSECT 操作を順序付けするには、次のパターンを使用してください。  
  
```sql  
SELECT ...  
FROM ( UNION/EXCEPT/INTERSECT operation )  
ORDER BY ...  
```  
  
## <a name="restricted-keywords"></a>制限付きのキーワード  
 次のキーワードは `ORDER BY` 句で使用する場合には、引用符で囲む必要があります。  
  
- CROSS  
  
- FULL  
  
- KEY  
  
- 左方向 (←) キー  
  
- ORDER  
  
- OUTER  
  
- 右方向 (→) キー  
  
- ROW  
  
- VALUE  
  
## <a name="ordering-nested-queries"></a>入れ子になったクエリの順序  
 Entity Framework では、入れ子になった式をクエリ内の任意の場所に配置できるため、入れ子になったクエリの順序は維持されません。  

次のクエリでは、結果が姓の順に並べ替えられます。  

```sql  
SELECT C1.FirstName, C1.LastName  
        FROM AdventureWorks.Contact as C1  
        ORDER BY C1.LastName  
```  

次のクエリでは、入れ子になったクエリの順序は無視されます。  

```sql  
SELECT C2.FirstName, C2.LastName  
    FROM (SELECT C1.FirstName, C1.LastName  
        FROM AdventureWorks.Contact as C1  
        ORDER BY C1.LastName) as C2  
```  
  
## <a name="example"></a>例  
 次の [!INCLUDE[esql](../../../../../../includes/esql-md.md)] クエリでは、SELECT ステートメントで返されたオブジェクトの並べ替え順序の指定に ORDER BY 演算子を使用します。 このクエリは、AdventureWorks Sales Model に基づいています。 このクエリをコンパイルして実行するには、次の手順を実行します。  
  
1. 「[方法: StructuralType 結果を返すクエリを実行する](../how-to-execute-a-query-that-returns-structuraltype-results.md)」の手順に従います。  
  
2. 次のクエリを引数として `ExecuteStructuralTypeQuery` メソッドに渡します。  
  
 [!code-sql[DP EntityServices Concepts#ORDERBY](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#orderby)]  
  
## <a name="see-also"></a>関連項目

- [クエリ式](query-expressions-entity-sql.md)
- [Entity SQL リファレンス](entity-sql-reference.md)
- [SKIP](skip-entity-sql.md)
- [LIMIT](limit-entity-sql.md)
- [TOP](top-entity-sql.md)
