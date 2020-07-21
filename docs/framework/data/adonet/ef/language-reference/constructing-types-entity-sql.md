---
title: コンストラクター (Entity SQL)
ms.date: 03/30/2017
ms.assetid: 41fa7bde-8d20-4a3f-a3d2-fb791e128010
ms.openlocfilehash: 7113aaf1c2caa982a8ab4751928856c1271570cb
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2019
ms.locfileid: "70251118"
---
# <a name="constructing-types-entity-sql"></a>コンストラクター (Entity SQL)
[!INCLUDE[esql](../../../../../../includes/esql-md.md)] には、行コンストラクター、名前付きの型コンストラクター、およびコレクション コンストラクターの 3 種類のコンストラクターが用意されています。  
  
## <a name="row-constructors"></a>行コンストラクター  
 1 つまたは複数の値から構造的に型付けされた匿名レコードを構築するには、[!INCLUDE[esql](../../../../../../includes/esql-md.md)] の行コンストラクターを使用します。 行コンストラクターの結果の型は、行の構築に使用された値の型に対応するフィールド型を持つ行型です。 たとえば、次の式では `Record(a int, b string, c int)`型の値が構築されます。  
  
 `ROW(1 AS a, "abc" AS b, a + 34 AS c)`  
  
 行コンストラクターで式の別名が指定されていなければ、Entity Framework は別名の生成を試みます。 詳細については、「[識別子](identifiers-entity-sql.md)」の「別名の規則」のセクションを参照してください。  
  
 次の規則は、行コンストラクターで別名を定義する式に適用されます。  
  
- 行コンストラクターの式で同じコンストラクターの他の別名を参照することはできません。  
  
- 同じ行コンストラクター内の 2 つの式に同じ別名を指定することはできません。  
  
 行コンストラクターの詳細については、「[ROW](row-entity-sql.md)」を参照してください。  
  
## <a name="collection-constructors"></a>コレクション コンストラクター  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] のコレクション コンストラクターを使用して、値のリストからマルチセットのインスタンスを作成します。 コンストラクターのすべての値は、相互に互換性のある型 `T` でなければなりません。また、コンストラクターは `Multiset<T>` 型のコレクションを生成します。 たとえば、次の式は整数のコレクションを作成します。  
  
 `Multiset(1, 2, 3)`  
  
 `{1, 2, 3}`  
  
 要素の型が確認できないため、空のマルチセット コンストラクターは使用できません。 次の式は無効です。  
  
 `multiset() {}`  
  
 詳細については、「[MULTISET](multiset-entity-sql.md)」を参照してください。  
  
## <a name="named-type-constructors-namedtype-initializers"></a>名前付きの型コンストラクター (NamedType 初期化子)  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] では、型コンストラクター (初期化子) を使用して、名前付きの複合型およびエンティティ型のインスタンスを作成できます。 たとえば、次の式は `Person` 型のインスタンスを作成します。  
  
 `Person("abc", 12)`  
  
 次の式は、複合型のインスタンスを作成する式です。  
  
 `MyModel.ZipCode(‘98118’, ‘4567’)`  
  
 次の式は、入れ子になった複合型のインスタンスを作成する式です。  
  
 `MyModel.AddressInfo('My street address', 'Seattle', 'WA', MyModel.ZipCode('98118', '4567'))`  
  
 次の式は、入れ子になった複合型を持つエンティティのインスタンスを作成する式です。  
  
 `MyModel.Person("Bill", MyModel.AddressInfo('My street address', 'Seattle', 'WA', MyModel.ZipCode('98118', '4567')))`  
  
 次の例は、複合型のプロパティを null に初期化する方法を示しています。 `MyModel.ZipCode(‘98118’, null)`  
  
 コンストラクターに対する引数は、型の属性の宣言と同じ順序であると見なされます。  
  
 詳細については、「[名前付きの型コンストラクター](named-type-constructor-entity-sql.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- [Entity SQL リファレンス](entity-sql-reference.md)
- [Entity SQL の概要](entity-sql-overview.md)
- [型システム](type-system-entity-sql.md)
