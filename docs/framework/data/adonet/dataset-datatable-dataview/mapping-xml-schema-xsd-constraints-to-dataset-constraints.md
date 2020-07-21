---
title: XML スキーマ (XSD) 制約の DataSet 制約への割り当て
ms.date: 03/30/2017
ms.assetid: 3d0d1a4b-9104-434f-ac04-6c01ab5716b5
ms.openlocfilehash: b44c3193e1b9e2e52e086111eab0ab0b0cae5c97
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2019
ms.locfileid: "70786075"
---
# <a name="mapping-xml-schema-xsd-constraints-to-dataset-constraints"></a>XML スキーマ (XSD) 制約の DataSet 制約への割り当て
XML スキーマ定義言語 (XSD) を使用すると、定義する要素と属性で制約を指定できます。 XML スキーマを <xref:System.Data.DataSet> のリレーショナル スキーマにマップすると、XML スキーマの制約が **DataSet** 内のテーブルと列の適切なリレーショナル制約にマップされます。  
  
 このセクションでは、次の XML スキーマの制約の割り当てについて説明します。  
  
- **unique** 要素を使用して指定される一意性制約。  
  
- **key** 要素を使用して指定されるキー制約。  
  
- **keyref** 要素を使用して指定されるキー参照制約。  
  
 要素または属性に対して制約を指定することにより、同じスキーマに基づくあらゆるドキュメントで、その要素の値について特定の制限を適用できます。 たとえば、スキーマにある **Customer** 要素の **CustomerID** 子要素のキー制約は、**CustomerID** 子要素の値がすべてのドキュメントのインスタンスで一意であり、null 値が許可されないことを示します。  
  
 さらに、ドキュメント内のリレーションシップを確立するために、ドキュメント内の要素および属性間に制約を指定することもできます。 ドキュメント内で制約を指定するためにスキーマ内で key 制約または keyref 制約を使用すると、ドキュメントの要素と属性間にリレーションシップを持つことになります。  
  
 マッピング処理では、これらのスキーマ制約が **DataSet** 内に作成されたテーブルでの適切な制約に変換されます。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [XML スキーマ (XSD) の UNIQUE 制約の DataSet 制約への割り当て](map-unique-xml-schema-xsd-constraints-to-dataset-constraints.md)  
 **DataSet** での一意制約の作成に使用する XML スキーマの要素について説明します。  
  
 [XML スキーマ (XSD) のキー制約の DataSet 制約への割り当て](map-key-xml-schema-xsd-constraints-to-dataset-constraints.md)  
 **DataSet** でのキー制約 (一意制約では null 値が許可されません) の作成に使用する XML スキーマの要素について説明します。  
  
 [XML スキーマ (XSD) のキー参照制約の DataSet 制約への割り当て](map-keyref-xml-schema-xsd-constraints-to-dataset-constraints.md)  
 **DataSet** でのキー参照 (外部キー) 制約の作成に使用する XML スキーマの要素について説明します。  
  
## <a name="related-sections"></a>関連項目  
 [XML スキーマ (XSD) からの DataSet リレーショナル構造の派生](deriving-dataset-relational-structure-from-xml-schema-xsd.md)  
 XSD スキーマから作成された **DataSet** のリレーショナル構造 (スキーマ) について説明します。  
  
 [XML スキーマ (XSD) からの DataSet リレーションの生成](generating-dataset-relations-from-xml-schema-xsd.md)  
 **DataSet** でのテーブル列間のリレーションの生成に使用する XML スキーマの要素について説明します。  
  
## <a name="see-also"></a>関連項目

- [ADO.NET の概要](../ado-net-overview.md)
