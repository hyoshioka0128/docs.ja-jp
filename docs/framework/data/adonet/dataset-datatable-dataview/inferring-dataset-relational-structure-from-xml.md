---
title: XML からの DataSet リレーショナル構造の推論
ms.date: 03/30/2017
ms.assetid: cd2f41c6-6785-420e-aa43-3ceb0bdccdce
ms.openlocfilehash: 1c8325d7ed52fea7397a7b5aa8744bdfa90b2c6e
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2019
ms.locfileid: "70785318"
---
# <a name="inferring-dataset-relational-structure-from-xml"></a>XML からの DataSet リレーショナル構造の推論
<xref:System.Data.DataSet> のリレーショナル構造 (スキーマ) は、テーブル、列、制約、およびリレーションで構成されます。 XML から <xref:System.Data.DataSet> を読み込むときには、事前定義されたスキーマを使用するか、または読み込む対象の XML から明示的にまたは推論によってスキーマを作成できます。 XML から <xref:System.Data.DataSet> のスキーマおよび内容を読み込む方法の詳細については、「[XML からの DataSet の読み込み](loading-a-dataset-from-xml.md)」および「[XML の DataSet スキーマ情報の読み込み](loading-dataset-schema-information-from-xml.md)」を参照してください。  
  
 <xref:System.Data.DataSet> のスキーマを XML から作成する場合は、XML スキーマ定義言語 (「[XML スキーマ (XSD) からの DataSet リレーショナル構造の派生](deriving-dataset-relational-structure-from-xml-schema-xsd.md)」を参照) または XDR (XML-Data Reduced) を使用して、スキーマを明示的に指定することをお勧めします。 XML で利用できる XML スキーマまたは XDR スキーマがない場合は、XML の要素および属性の構造から <xref:System.Data.DataSet> のスキーマを推論できます。  
  
 ここでは、XML の要素と属性およびその構造を示し、<xref:System.Data.DataSet> スキーマの推論に関する規則について説明します。また、その規則に基づいて推論した <xref:System.Data.DataSet> スキーマも示します。  
  
 XML ドキュメント内のすべての属性を推論プロセスの対象には含めないでください。 名前空間で修飾された属性には、XML ドキュメントにとっては重要ですが、<xref:System.Data.DataSet> スキーマにとっては不要なメタデータが含まれていることがあります。 <xref:System.Data.DataSet.InferXmlSchema%2A> を使用して、推論プロセスの間に無視する特定の名前空間を指定できます。 詳しくは、「[XML の DataSet スキーマ情報の読み込み](loading-dataset-schema-information-from-xml.md)」をご覧ください。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [DataSet スキーマの推論プロセスの概要](summary-of-the-dataset-schema-inference-process.md)  
 XML から <xref:System.Data.DataSet> のスキーマを推論するときの規則について概要を示します。  
  
 [テーブルの推論](inferring-tables.md)  
 <xref:System.Data.DataSet> のテーブルとして推論される XML の要素について説明します。  
  
 [列の推論](inferring-columns.md)  
 テーブルの列として推論される XML の要素と属性について説明します。  
  
 [リレーションシップの推論](inferring-relationships.md)  
 推論された入れ子状のテーブルに対して作成される <xref:System.Data.DataRelation> オブジェクトおよび <xref:System.Data.ForeignKeyConstraint> オブジェクトについて説明します。  
  
 [要素のテキストの推論](inferring-element-text.md)  
 XML 要素のテキストに対して作成される列について、および XML 要素のテキストが無視される場合について説明します。  
  
 [推論の制限事項](inference-limitations.md)  
 スキーマ推論の制限事項について説明します。  
  
## <a name="related-sections"></a>関連項目  
 [DataSet での XML の使用](using-xml-in-a-dataset.md)  
 <xref:System.Data.DataSet> オブジェクトと XML データとの対話について説明します。  
  
 [XML スキーマ (XSD) からの DataSet リレーショナル構造の派生](deriving-dataset-relational-structure-from-xml-schema-xsd.md)  
 XML スキーマ定義言語 (XSD) スキーマから作成された <xref:System.Data.DataSet> のリレーショナル構造 (スキーマ) について説明します。  
  
 [ADO.NET の概要](../ado-net-overview.md)  
 ADO.NET のアーキテクチャとコンポーネントについて、また ADO.NET を使用して既存のデータ ソースにアクセスしたり、アプリケーション データを管理する方法について説明します。  
  
## <a name="see-also"></a>関連項目

- [ADO.NET の概要](../ado-net-overview.md)
