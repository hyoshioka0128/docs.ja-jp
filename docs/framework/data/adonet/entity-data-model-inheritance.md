---
title: Entity Data Model:継承
ms.date: 03/30/2017
ms.assetid: 42c7ef24-710a-4af9-8493-cd41c399ecb0
ms.openlocfilehash: 4c4abc371000006d40ede3d904b0437f3f85e3e7
ms.sourcegitcommit: 22be09204266253d45ece46f51cc6f080f2b3fd6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73738455"
---
# <a name="entity-data-model-inheritance"></a>Entity Data Model:継承
Entity Data Model (EDM) では、[エンティティ型](entity-type.md)の継承がサポートされています。 EDM の継承は、オブジェクト指向プログラミング言語におけるクラスの継承に似ています。 オブジェクト指向言語のクラスと同様、概念モデルでは、別のエンティティ型 ("*基本型*") を継承するエンティティ型 ("*派生型*") を定義できます。 ただし、オブジェクト指向プログラミングのクラスとは異なり、概念モデルでは、派生型は基本型のすべての[プロパティ](property.md)と[ナビゲーション プロパティ](navigation-property.md)を常に継承します。 派生型の継承プロパティは、オーバーライドできません。  
  
 概念モデルでは、派生型が別の派生型を継承する継承階層を構築することができます。 階層の最上位にある型 (階層内で派生型ではない唯一の型) は、"*ルート型*" と呼ばれます。 継承階層では、ルート型に[エンティティ キー](entity-key.md)を定義する必要があります。  
  
 複数の型から派生型を継承する継承階層を構築することはできません。 たとえば、`Book` エンティティ型の概念モデルでは、それぞれ `FictionBook` から継承する派生型、`NonFictionBook` および `Book` を定義することができます。 しかし、`FictionBook` 型と `NonFictionBook` 型の両方から継承する型を定義することはできません。  
  
## <a name="example"></a>例  

次の図では、`Book`、`FictionBook`、`Publisher`、`Author` という 4 つのエンティティ型の概念モデルを示します。 `FictionBook` エンティティ型は、`Book` エンティティ型から継承する派生型です。 `FictionBook` 型は、`ISBN (Key)` プロパティ、`Title` プロパティ、および `Revision` プロパティを継承し、`Genre` と呼ばれる追加プロパティを定義します。  
  
 ![4 つのエンティティ型を含む概念モデルを示す図。](./media/entity-data-model-inheritance/entity-type-inheritance.gif)  
  
 [ADO.NET Entity Framework](./ef/index.md) では、概念スキーマ定義言語 ([CSDL](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec)) と呼ばれるドメイン固有言語 (DSL) を使用して概念モデルを定義します。 次の CSDL は、上のダイアグラムに示された `FictionBook` 型を継承する `Book` エンティティ型を定義しています。  
  
 [!code-xml[EDM_Example_Model#DerivedType](../../../../samples/snippets/xml/VS_Snippets_Data/edm_example_model/xml/books5.edmx#derivedtype)]  
  
## <a name="see-also"></a>関連項目

- [Entity Data Model キーの概念](entity-data-model-key-concepts.md)
- [Entity Data Model](entity-data-model.md)
