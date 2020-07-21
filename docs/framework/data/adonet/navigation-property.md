---
title: ナビゲーション プロパティ
ms.date: 03/30/2017
ms.assetid: d0bf1a6a-1d84-484c-b7c3-b410fd8dc0b1
ms.openlocfilehash: eaf22ad4dd24b4bf046f14ccabd435a9ecd1776f
ms.sourcegitcommit: 011314e0c8eb4cf4a11d92078f58176c8c3efd2d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/09/2020
ms.locfileid: "77094385"
---
# <a name="navigation-property"></a>ナビゲーション プロパティ

"*ナビゲーション プロパティ*" は、[アソシエーション](association-type.md)の 1 つの [End](association-end.md) から別の End へのナビゲーションを可能にする、[エンティティ型](entity-type.md)の省略可能なプロパティです。 他の[プロパティ](property.md)とは異なり、ナビゲーション プロパティではデータは伝達されません。

ナビゲーション プロパティの定義には、以下が含まれます。

- 名前。 (必須)

- 移動対象のアソシエーション。 (必須)

- 移動対象のアソシエーションの End。 (必須)

ナビゲーション プロパティは、アソシエーション End の両方のエンティティ型で省略可能です。 1 つのアソシエーション End のエンティティ型にナビゲーション プロパティを定義した場合に、そのアソシエーションの他方の End でもエンティティ型にナビゲーション プロパティを定義する必要はありません。

ナビゲーション プロパティのデータ型は、リモートの[アソシエーション End](association-end.md) の[多重度](association-end-multiplicity.md)により決まります。 たとえば、ナビゲーション プロパティ `OrdersNavProp` が `Customer` エンティティ型に存在し、`Customer` と `Order` の間の一対多のアソシエーションで移動するとします。 ナビゲーション プロパティのリモートのアソシエーション End の多重度が多数 (\*) であるため、そのデータ型は (`Order` の) コレクションになります。 同様に、`CustomerNavProp` エンティティ型にナビゲーション プロパティ、`Order` が存在する場合、リモート End の多重度が (1) であるため、データ型は `Customer` になります。

## <a name="example"></a>例

下のダイアグラムは、`Book`、`Publisher`、および `Author` という 3 つのエンティティ型の概念モデルを示しています。 ナビゲーション プロパティ `Publisher` と `Authors` が、Book エンティティ型で定義されています。 Publisher エンティティ型と `Books` エンティティ型には、ナビゲーション プロパティ、`Author` が定義されています。

![3 つのエンティティ型を含む概念モデルを示す図。](./media/navigation-property/conceptual-model-entity-types-associations.gif)  

[ADO.NET Entity Framework](./ef/index.md) では、概念スキーマ定義言語 ([CSDL](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec)) と呼ばれるドメイン固有言語 (DSL) を使用して概念モデルを定義します。 次の CSDL は、上のダイアグラムに示された `Book` エンティティ型を定義しています。

[!code-xml[EDM_Example_Model#EntityExample](~/samples/snippets/xml/VS_Snippets_Data/edm_example_model/xml/books.edmx#entityexample)]

ナビゲーション プロパティの定義に必要な情報の伝達には、XML 属性が使用されます。属性 `Name` にはプロパティ名が含まれ、`Relationship` にはナビゲートするアソシエーション名が含まれ、`FromRole` と `ToRole` にはアソシエーションの End が含まれています。

## <a name="see-also"></a>関連項目

- [Entity Data Model キーの概念](entity-data-model-key-concepts.md)
- [Entity Data Model](entity-data-model.md)
- [リレーションシップ、ナビゲーション プロパティ、および外部キー](/ef/ef6/fundamentals/relationships)
