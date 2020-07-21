---
title: アソシエーション End の多重度
ms.date: 03/30/2017
ms.assetid: 340926ee-aefb-4bef-92cc-453e5251fd03
ms.openlocfilehash: 3f3d8ba9f7e68065024dd3efb599b847496740cd
ms.sourcegitcommit: 22be09204266253d45ece46f51cc6f080f2b3fd6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73738571"
---
# <a name="association-end-multiplicity"></a>アソシエーション End の多重度
"*アソシエーション End の多重度*" は、[アソシエーション](association-type.md)の 1 つの End に存在できる[エンティティ型](entity-type.md)のインスタンス数を定義します。  
  
 アソシエーション End の多重度には、次のいずれかの値を指定できます。  
  
- 1 つ (1): アソシエーション End に 1 個のエンティティ型インスタンスが存在することを示します。  
  
- 0 または 1 (0..1): アソシエーション End に 0 個か 1 個のエンティティ型インスタンスが存在することを示します。  
  
- 多数 (\*): アソシエーション End に 0 個、1 個、または複数個のエンティティ型インスタンスが存在することを示します。  
  
 アソシエーションは、多くの場合、そのアソシエーション End の多重度により特徴付けられます。 たとえば、アソシエーション End の多重度が 1 と多数 (\*) の場合、アソシエーションは一対多のアソシエーションと呼ばれます。 次の例で、`PublishedBy` アソシエーションは一対多のアソシエーションです (出版社が多くの書籍を出版し、書籍は 1 社の出版社により出版されます)。 `WrittenBy` アソシエーションは多対多のアソシエーションです (書籍の著者が複数の場合があり、著者は複数の書籍を執筆することができます)。  
  
## <a name="example"></a>例  
 下のダイアグラムは、`PublishedBy` および `WrittenBy` という 2 つのアソシエーションの概念モデルを示しています。 `PublishedBy` アソシエーションのアソシエーション End は `Book` および `Publisher` のエンティティ型です。 `Publisher` End の多重度は 1 で、`Book` End の多重度は多数 (\*) です。  
  
 ![3 種類のエンティティを持つモデルの例](./media/association-end-multiplicity/example-model-three-entity-types.gif)  
  
 ADO.NET Entity Framework では、概念スキーマ定義言語 ([CSDL](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec)) と呼ばれるドメイン固有言語 (DSL) を使用して、概念モデルを定義します。 次の CSDL は、上のダイアグラムに示された `PublishedBy` アソシエーションを定義しています。  
  
 [!code-xml[EDM_Example_Model#AssociationExample](../../../../samples/snippets/xml/VS_Snippets_Data/edm_example_model/xml/books.edmx#associationexample)]  
  
## <a name="see-also"></a>関連項目

- [Entity Data Model キーの概念](entity-data-model-key-concepts.md)
- [Entity Data Model](entity-data-model.md)
