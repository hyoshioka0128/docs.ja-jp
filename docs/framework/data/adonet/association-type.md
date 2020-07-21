---
title: アソシエーション型
ms.date: 03/30/2017
ms.assetid: 26c409f6-06e8-4441-ac78-1b1076a3c005
ms.openlocfilehash: e1430e6255dce2bae6d82411db5d2a9f11f46e1a
ms.sourcegitcommit: 22be09204266253d45ece46f51cc6f080f2b3fd6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73738556"
---
# <a name="association-type"></a>アソシエーション型
"*アソシエーション型*" (アソシエーションとも呼ばれます) は、Entity Data Model (EDM) でリレーションシップを記述するために不可欠な構成要素です。 概念モデルでは、アソシエーションによって 2 つの[エンティティ型](entity-type.md) (`Customer` や `Order` など) の間のリレーションシップが表されます。 アプリケーションでは、アソシエーションのインスタンスが特定のアソシエーション (`Customer` のインスタンスと `Order` のインスタンスの間のアソシエーションなど) を表します。 アソシエーション インスタンスは、[アソシエーション セット](association-set.md)に論理的にグループ化されます。  
  
 アソシエーションの定義には、次の情報が含まれます。  
  
- 一意の名前  (必須)  
  
- 2 つの[アソシエーション End](association-end.md) (リレーションシップを構成する各エンティティ型に 1 つずつ)。 (必須)  
  
    > [!NOTE]
    > アソシエーションは、2 つ以上のエンティティ型のリレーションシップを表すことができません。 しかし、各アソシエーション End に同じエンティティ型を指定することによって、アソシエーションで自己リレーションシップを定義できます。  
  
- [参照整合性制約](referential-integrity-constraint.md)。 (オプション)。  
  
 各アソシエーション End には、アソシエーションの 1 つの End に存在できるエンティティ型のインスタンス数を示す[アソシエーション End の多重度](association-end-multiplicity.md)を指定する必要があります。 アソシエーション End の多重度には、1 、ゼロか 1 (0..1)、または多数 (\*) の値を指定することができます。 アソシエーションの一方の End にあるエンティティ型のインスタンスには、それらがエンティティ型で公開されている場合、[ナビゲーション プロパティ](navigation-property.md)または外部キーからアクセスできます。 詳しくは、「[Entity Data Model: 外部キー](foreign-key-property.md)」をご覧ください。  
  
## <a name="example"></a>例  
 下のダイアグラムは、`PublishedBy` および `WrittenBy` という 2 つのアソシエーションの概念モデルを示しています。 `PublishedBy` アソシエーションのアソシエーション End は `Book` および `Publisher` のエンティティ型です。 `Publisher` End の多重度は 1 で、`Book` End の多重度は多数 (\*) です。これは、出版社が多くの書籍を出版し、書籍は 1 社の出版社により出版されることを示します。  
  
 ![3 種類のエンティティを持つモデルの例](./media/association-type/example-model-three-entity-types.gif)  
  
 [ADO.NET Entity Framework](./ef/index.md) では、概念スキーマ定義言語 ([CSDL](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec)) と呼ばれるドメイン固有言語 (DSL) を使用して概念モデルを定義します。 次の CSDL は、上のダイアグラムに示された `PublishedBy` アソシエーションを定義しています。  
  
 [!code-xml[EDM_Example_Model#AssociationExample](../../../../samples/snippets/xml/VS_Snippets_Data/edm_example_model/xml/books.edmx#associationexample)]  
  
## <a name="see-also"></a>関連項目

- [Entity Data Model キーの概念](entity-data-model-key-concepts.md)
- [Entity Data Model](entity-data-model.md)
