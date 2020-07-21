---
title: 型定義 (Entity SQL)
ms.date: 03/30/2017
ms.assetid: 306b204a-ade5-47ef-95b5-c785d2da4a7e
ms.openlocfilehash: 35f660a66fd706b37187056830af5e06ac586caa
ms.sourcegitcommit: 628e8147ca10187488e6407dab4c4e6ebe0cac47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/15/2019
ms.locfileid: "72319250"
---
# <a name="type-definitions-entity-sql"></a>型定義 (Entity SQL)
型定義は、[!INCLUDE[esql](../../../../../../includes/esql-md.md)] Inline 関数の宣言ステートメントで使用されます。  
  
## <a name="remarks"></a>Remarks  
 インライン関数の宣言ステートメントは、[FUNCTION](function-entity-sql.md) キーワード、関数名を表す識別子 (例: "MyAvg")、かっこで囲まれたパラメーター定義リスト (例: "dues Collection(Decimal)") で構成されます。  
  
 パラメーター定義リストは、0 個以上のパラメーター定義で構成されます。 各パラメーター定義は、識別子 (関数のパラメーターの名前。例 : "dues") とそれに続く型定義 (例 : "Collection(Decimal)") で構成されます。  
  
 型定義は、次のいずれかになります。  
  
- 識別子の型 ("Int32" や "AdventureWorks.Order" など)。  
  
- キーワード `COLLECTION` とそれに続くかっこに囲まれた別の型定義 (例 : "Collection(AdventureWorks.Order)")。  
  
- キーワード ROW とそれに続くかっこに囲まれたプロパティ定義リスト (例 : "Row(x AdventureWorks.Order)")。 プロパティ定義の形式は、"`identifier type_definition`, `identifier type_definition`, ..." のようになります。  
  
- キーワード REF とそれに続くかっこに囲まれた識別子の型 (例 : "Ref(AdventureWorks.Order)")。 REF 型定義演算子は、引数としてエンティティ型を必要とします。 引数としてプリミティブ型を指定することはできません。  
  
 型定義を入れ子にできます (例 : "Collection(Row(x Ref(AdventureWorks.Order)))")。  
  
 型定義のオプションは、次のとおりです。  
  
- `IdentifierName supported_type`、または   
  
- `IdentifierName` COLLECTION(`type_definition`)、または  
  
- `IdentifierName` ROW(`property_definition`)、または  
  
- `IdentifierName` REF(`supported_entity_type`)  
  
 プロパティ定義オプションは、`IdentifierName type_definition` です。  
  
 現在の名前空間で使用されている型であれば、いずれもサポートされます。 これには、プリミティブ型とエンティティ型の両方が含まれます。  
  
 サポートされるエンティティ型は、現在の名前空間で使用されているエンティティ型だけを参照します。 これには、プリミティブ型は含まれません。  
  
## <a name="examples"></a>使用例  
 簡単な型定義の例を次に示します。  
  
```sql  
USING Microsoft.Samples.Entity  
Function MyRound(p1 EDM.Decimal) AS (  
   Round(p1)  
)  
MyRound(CAST(1.7 as EDM.Decimal))  
```  
  
 COLLECTION 型定義の例を次に示します。  
  
```sql  
USING Microsoft.Samples.Entity  
Function MyRound(p1 Collection(EDM.Decimal)) AS (  
   Select Round(p1) from p1  
)  
MyRound({CAST(1.7 as EDM.Decimal), CAST(2.7 as EDM.Decimal)})  
```  
  
 ROW 型定義の例を次に示します。  
  
```sql  
USING Microsoft.Samples.Entity  
Function MyRound(p1 Row(x EDM.Decimal)) AS (  
   Round(p1.x)  
)  
select MyRound(row(a as x)) from {CAST(1.7 as EDM.Decimal), CAST(2.7 as EDM.Decimal)} as a  
```  
  
 REF 型定義の例を次に示します。  
  
```sql  
USING Microsoft.Samples.Entity  
Function UnReference(p1 Ref(AdventureWorks.Order)) AS (  
   Deref(p1)  
)  
select Ref(x) from AdventureWorksEntities.SalesOrderHeaders as x  
```  
  
## <a name="see-also"></a>関連項目

- [Entity SQL の概要](entity-sql-overview.md)
- [Entity SQL リファレンス](entity-sql-reference.md)
