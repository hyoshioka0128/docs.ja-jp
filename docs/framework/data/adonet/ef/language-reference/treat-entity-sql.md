---
title: TREAT (Entity SQL)
ms.date: 03/30/2017
ms.assetid: 5b77f156-55de-4cb4-8154-87f707d4c635
ms.openlocfilehash: 06c4200434f443446e8981dcefe2baf43b1af4b0
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79149896"
---
# <a name="treat-entity-sql"></a>TREAT (Entity SQL)
特定の基本データ型のオブジェクトを指定の派生型のオブジェクトとして処理します。  
  
## <a name="syntax"></a>構文  
  
```sql  
TREAT ( expression as type)  
```  
  
## <a name="arguments"></a>引数  
 `expression`  
 エンティティを返す任意の有効なクエリ式。  
  
> [!NOTE]
> 指定の式の型は、特定のデータ型のサブタイプである必要があります。または、データ型は式の型のサブタイプである必要があります。  
  
 `type`  
 エンティティ型。 型は名前空間で修飾する必要があります。  
  
> [!NOTE]
> 指定の式は、特定のデータ型のサブタイプである必要があります。または、データ型は式のサブタイプである必要があります。  
  
## <a name="return-value"></a>戻り値  
 指定されたデータ型の値。  
  
## <a name="remarks"></a>Remarks  
 TREAT は関連クラス間でキャストを実行するために使用します。 たとえば、 `Employee` が `Person` から派生し、p が `Person`型である場合、 `TREAT(p AS NamespaceName.Employee)` はジェネリック型の `Person` インスタンスを `Employee`にキャストします。つまり、p を `Employee`として処理できます。  
  
 TREAT は、次のようにクエリを実行できる継承シナリオで使用されます。  
  
```sql  
SELECT TREAT(p AS NamespaceName.Employee)  
FROM ContainerName.Person AS p  
WHERE p IS OF (NamespaceName.Employee)
```  
  
 このクエリは、 `Person` エンティティを `Employee` 型にキャストします。 p の値が実際には `Employee`型でない場合、この式は `null`値を返します。  
  
> [!NOTE]
> 指定する式 `Employee` は、指定するデータ型 `Person` のサブタイプである必要があります。または、データ型は式のサブタイプである必要があります。 そうでない場合は、コンパイル時にエラーが発生します。  
  
 次の表に、いくつかの通常パターンと一般的でないパターンにおける TREAT の動作を示します。 すべての例外はクライアント側にスローされてから、プロバイダーが呼び出されます。  
  
|パターン|動作|  
|-------------|--------------|  
|`TREAT (null AS EntityType)`|`DbNull`を返します。|  
|`TREAT (null AS ComplexType)`|例外をスローします。|  
|`TREAT (null AS RowType)`|例外をスローします。|  
|`TREAT (EntityType AS EntityType)`|`EntityType` または `null`を返します。|  
|`TREAT (ComplexType AS ComplexType)`|例外をスローします。|  
|`TREAT (RowType AS RowType)`|例外をスローします。|  
  
## <a name="example"></a>例  
 次の [!INCLUDE[esql](../../../../../../includes/esql-md.md)] クエリでは、TREAT 演算子を使用して、Course 型のオブジェクトを OnsiteCourse 型のオブジェクトのコレクションに変換します。 このクエリは、 [School モデル](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb896300(v=vs.100))に基づいています。  
  
 [!code-sql[DP EntityServices Concepts#TREAT_ISOF](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#treat_isof)]  
  
## <a name="see-also"></a>関連項目

- [Entity SQL リファレンス](entity-sql-reference.md)
- [NULL 値が許容される構造化型](nullable-structured-types-entity-sql.md)
