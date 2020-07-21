---
title: 型システム (Entity SQL)
ms.date: 03/30/2017
ms.assetid: 818a505b-a196-41dd-aaac-2ccd5f7a2f1a
ms.openlocfilehash: b8b721aff5b7886fdb897ecaa3dcc163ec94ae79
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79149832"
---
# <a name="type-system-entity-sql"></a>型システム (Entity SQL)
[!INCLUDE[esql](../../../../../../includes/esql-md.md)] では、次に示すように多数の型がサポートされています。  
  
- `Int32` や `String.` などのプリミティブ型 (単純型)。  
  
- <xref:System.Data.Metadata.Edm.EntityType>、<xref:System.Data.Metadata.Edm.ComplexType>、<xref:System.Data.Metadata.Edm.RelationshipType> など、スキーマで定義される標準型。  
  
- <xref:System.Data.Metadata.Edm.CollectionType>、<xref:System.Data.Metadata.Edm.RowType>、<xref:System.Data.Metadata.Edm.RefType> など、明示的にはスキーマで定義されない匿名型。  
  
 ここでは、明示的にはスキーマで定義されていなくても Entity SQL でサポートされている匿名型について説明します。 プリミティブ型および標準型については、「[概念モデルの型 (CSDL)](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec#conceptual-model-types-csdl)」を参照してください。  
  
## <a name="rows"></a>行  
 行の構造は、行を構成する型指定された名前付きのメンバーの配列に依存します。 行型には ID がなく、派生元にすることはできません。 同じ行型のインスタンスは、メンバーがそれぞれ同等である場合は同等になります。 行には構造同値以外の動作はなく、共通言語ランタイムに同等のものはありません。 クエリの結果は、行または行のコレクションを含む構造になります。 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] クエリとホスト言語の間の API バインドは、結果を生成したクエリでどのように行が構成されるかを定義します。 行インスタンスの作成方法については、「[コンストラクター](constructing-types-entity-sql.md)」を参照してください。  
  
## <a name="collections"></a>コレクション  
 コレクション型は、他のオブジェクトの 0 個以上のインスタンスを表します。 コレクションの作成方法については、「[コンストラクター](constructing-types-entity-sql.md)」を参照してください。  
  
## <a name="references"></a>関連項目  
 参照とは、特定のエンティティ セットにある特定のエンティティへの論理ポインターです。  
  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] では、参照の構築、分解、およびナビゲートを行うための次の演算子がサポートされています。  
  
- [REF](ref-entity-sql.md)  
  
- [CREATEREF](createref-entity-sql.md)  
  
- [KEY](key-entity-sql.md)  
  
- [DEREF](deref-entity-sql.md)  
  
 メンバー アクセス (ドット) 演算子 (`.`) を使用して参照によるナビゲーションを行うことができます。 次のコード例では、r (参照) プロパティによるナビゲーションで Order の Id プロパティを取得します。  
  
```sql  
select o2.r.Id
from (select ref(o) as r from LOB.Orders as o) as o2
```  
  
 参照値が null であるか、参照先が存在しない場合、結果は null になります。  
  
## <a name="see-also"></a>関連項目

- [Entity SQL の概要](entity-sql-overview.md)
- [Entity SQL リファレンス](entity-sql-reference.md)
- [CAST](cast-entity-sql.md)
- [CSDL、SSDL、および MSL 仕様](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec)
