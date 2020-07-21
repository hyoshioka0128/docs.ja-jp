---
title: ISOF (Entity SQL)
ms.date: 03/30/2017
ms.assetid: 5b2b0d34-d0a7-4bcd-baf2-58aa8456d00b
ms.openlocfilehash: c4c4cbf74cb17cf43e79c42ff42d1e68122fd534
ms.sourcegitcommit: 628e8147ca10187488e6407dab4c4e6ebe0cac47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/15/2019
ms.locfileid: "72319714"
---
# <a name="isof-entity-sql"></a>ISOF (Entity SQL)
式の型が指定の型であるか、またはそのサブタイプであるかを判断します。  
  
## <a name="syntax"></a>構文  
  
```sql  
expression IS [ NOT ] OF ( [ ONLY ] type )  
```  
  
## <a name="arguments"></a>引数  
 `expression`  
 型を判断するための任意の有効なクエリ式。  
  
 NOT  
 IS OF の EDM.Boolean の結果を否定します。  
  
 ONLY  
 `true` が `expression` 型であり、そのサブタイプでない場合に限り、IS OF が `type` を返すことを指定します。  
  
 `type`  
 `expression` を判定するための型。 型は名前空間で修飾する必要があります。  
  
## <a name="return-value"></a>戻り値  
 `true` が型 T で、T が基本データ型または `expression` の派生型である場合は、`type` となります。`expression` が実行時に null である場合は null となり、それ以外の場合は `false` となります。  
  
## <a name="remarks"></a>Remarks  
 式 `expression IS NOT OF (type)` および `expression IS NOT OF (ONLY type)` は、構文的にはそれぞれ `NOT (expression IS OF (type))` および `NOT (expression IS OF (ONLY type))` に相当します。  
  
 次の表に、いくつかの通常およびコーナー パターンにおける `IS OF` 演算子の動作を示します。 すべての例外はクライアント側にスローされてから、プロバイダーが呼び出されます。  
  
|パターン|動作|  
|-------------|--------------|  
|null IS OF (EntityType)|スロー|  
|null IS OF (ComplexType)|スロー|  
|null IS OF (RowType)|スロー|  
|TREAT (null AS EntityType) IS OF (EntityType)|DBNull を返します。|  
|TREAT (null AS ComplexType) IS OF (ComplexType)|スロー|  
|TREAT (null AS RowType) IS OF (RowType)|スロー|  
|EntityType IS OF (EntityType)|true または false を返します。|  
|ComplexType IS OF (ComplexType)|スロー|  
|RowType IS OF (RowType)|スロー|  
  
## <a name="example"></a>例  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] の次のクエリでは、IS OF 演算子を使用してクエリ式の型を判定し、次に TREAT 演算子を使用して Course 型のオブジェクトを OnsiteCourse 型のオブジェクトのコレクションに変換します。 このクエリは、 [School モデル](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb896300(v=vs.100))に基づいています。  
  
 [!code-sql[DP EntityServices Concepts#TREAT_ISOF]~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#treat_isof)]  
  
## <a name="see-also"></a>関連項目

- [Entity SQL リファレンス](entity-sql-reference.md)
