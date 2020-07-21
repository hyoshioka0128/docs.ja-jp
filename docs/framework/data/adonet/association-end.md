---
title: アソシエーション End
ms.date: 03/30/2017
ms.assetid: 2c345213-0296-4d90-ac6d-cef179798a75
ms.openlocfilehash: 489802ca18708e076c0cd5dd380ad1361916ad5f
ms.sourcegitcommit: 22be09204266253d45ece46f51cc6f080f2b3fd6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73732357"
---
# <a name="association-end"></a>アソシエーション End
"*アソシエーション End*" では、[アソシエーション](association-type.md)の一方の End にある[エンティティ型](entity-type.md)と、アソシエーションのその End に存在できるエンティティ型のインスタンス数が示されます。 アソシエーション End はアソシエーションの一部として定義され、アソシエーションには必ず 2 つのアソシエーション End が必要です。 [ナビゲーション プロパティ](navigation-property.md)により、一方のアソシエーション End から他方のアソシエーション End へのナビゲーションが可能になります。  
  
 アソシエーション End の定義には、次の情報が含まれます。  
  
- アソシエーションに含まれるエンティティ型の 1 つ。 (必須)  
  
    > [!NOTE]
    > アソシエーションでは、各アソシエーション End に同じエンティティ型を指定することができます。 これにより、自己アソシエーションが作成されます。  
  
- アソシエーションの 1 つの End に存在できるエンティティ型のインスタンス数を示す[アソシエーション End の多重度](association-end-multiplicity.md)。 アソシエーション End の多重度には、1 、ゼロか 1 (0..1)、または多数 (\*) の値を指定することができます。  
  
- アソシエーション End の名前。 (オプション)。  
  
- アソシエーション End に実行する CASCADE ON DELETE などの操作の情報。 (オプション)。  
  
## <a name="example"></a>例  
 下のダイアグラムは、`PublishedBy` および `WrittenBy` という 2 つのアソシエーションの概念モデルを示しています。 `PublishedBy` アソシエーションのアソシエーション End は `Book` および `Publisher` のエンティティ型です。 `Publisher` End の多重度は 1 で、`Book` End の多重度は多数 (\*) です。これは、出版社が多くの書籍を出版し、書籍は 1 社の出版社により出版されることを示します。  
  
 ![3 種類のエンティティを持つモデルの例](./media/association-end/example-model-three-entity-types.gif)  
  
 ADO.NET Entity Framework では、概念スキーマ定義言語 ([CSDL](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec)) と呼ばれるドメイン固有言語 (DSL) を使用して、概念モデルを定義します。 次の CSDL は、上のダイアグラムに示された `PublishedBy` アソシエーションを定義します。 各アソシエーション End の型、名前、および多重度は、XML 属性 (それぞれ `Type` 属性、`Role` 属性、および `Multiplicity` 属性) で指定されます。 アソシエーション End に実行する操作に関するオプション情報は、XML 要素 (`OnDelete` 要素) に指定します。 この場合、出版社を削除すると、関連付けられたすべての書籍も削除されます。  
  
 [!code-xml[EDM_Example_Model#AssociationEnd](../../../../samples/snippets/xml/VS_Snippets_Data/edm_example_model/xml/books3.edmx#associationend)]  
  
## <a name="see-also"></a>関連項目

- [Entity Data Model キーの概念](entity-data-model-key-concepts.md)
- [Entity Data Model](entity-data-model.md)
