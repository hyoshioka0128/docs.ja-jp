---
title: DataSet での XML の使用
ms.date: 03/30/2017
ms.assetid: 35138159-e199-49ec-baf7-1ec6777e171e
ms.openlocfilehash: ca04f524685e080be6af12a4df6eda585a908683
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2019
ms.locfileid: "70784257"
---
# <a name="using-xml-in-a-dataset"></a>DataSet での XML の使用
ADO.NET では、XML ストリームまたは XML ドキュメントから <xref:System.Data.DataSet> にデータを格納できます。 <xref:System.Data.DataSet> にデータまたはスキーマ情報を格納するには、XML ストリームまたは XML ドキュメントを使用します。 XML ストリームまたは XML ドキュメントから提供される情報を <xref:System.Data.DataSet> の既存のデータまたはスキーマ情報と組み合わせることもできます。  
  
 ADO.NET では、他のアプリケーションや XML 対応プラットフォームで <xref:System.Data.DataSet> が使用される場合に、この <xref:System.Data.DataSet> を HTTP 経由で転送するため、DataSet の XML 表現を作成できます。このとき、DataSet にスキーマが含まれていても、含まれていなくてもかまいません。 <xref:System.Data.DataSet> の XML 表現では、データを XML で記述します。XML 表現にスキーマをインラインで含める場合は、このスキーマを XML スキーマ定義言語 (XSD) で記述します。 XML および XML スキーマには、リモート クライアントとの間で <xref:System.Data.DataSet> の内容を転送するための便利な書式が用意されています。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [DiffGrams](diffgrams.md)  
 <xref:System.Data.DataSet> の内容の読み取りと書き込みに使用される XML 形式である DiffGram について詳しく説明します。  
  
 [XML からの DataSet の読み込み](loading-a-dataset-from-xml.md)  
 XML ドキュメントから <xref:System.Data.DataSet> の内容を読み込むときに考慮する必要のある各種オプションについて説明します。  
  
 [DataSet 内容の XML データとしての書き込み](writing-dataset-contents-as-xml-data.md)  
 <xref:System.Data.DataSet> の内容を XML データとして生成する方法と、使用できる各種 XML 形式オプションについて説明します。  
  
 [XML の DataSet スキーマ情報の読み込み](loading-dataset-schema-information-from-xml.md)  
 XML から <xref:System.Data.DataSet> のスキーマを読み込むために使用される <xref:System.Data.DataSet> のメソッドについて説明します。  
  
 [XSD としての DataSet スキーマ情報の書き込み](writing-dataset-schema-information-as-xsd.md)  
 XML スキーマの使用方法と、<xref:System.Data.DataSet> からの XML スキーマの生成方法について説明します。  
  
 [DataSet と XmlDataDocument の同期](dataset-and-xmldatadocument-synchronization.md)  
 1 つのデータ セットのリレーショナル ビューおよび階層ビューの両方に同期的な方法でアクセスする .NET Framework の機能について説明し、<xref:System.Data.DataSet> と <xref:System.Xml.XmlDataDocument> の間で同期的なリレーションシップを確立する方法について説明します。  
  
 [DataRelation の入れ子化](nesting-datarelations.md)  
 <xref:System.Data.DataRelation> の内容を XML データとして表現する場合において、入れ子になった <xref:System.Data.DataSet> オブジェクトの重要性について説明します。また、入れ子になったこれらのオブジェクトの作成方法について説明します。  
  
 [XML スキーマ (XSD) からの DataSet リレーショナル構造の派生](deriving-dataset-relational-structure-from-xml-schema-xsd.md)  
 XML スキーマから作成された <xref:System.Data.DataSet> のリレーショナル構造 (スキーマ) について説明します。  
  
 [XML からの DataSet リレーショナル構造の推論](inferring-dataset-relational-structure-from-xml.md)  
 XML 要素から推論する際に作成される <xref:System.Data.DataSet> のリレーショナル構造 (スキーマ) について説明します。  
  
## <a name="related-sections"></a>関連項目  
 [ADO.NET の概要](../ado-net-overview.md)  
 ADO.NET のアーキテクチャとコンポーネントについて説明し、それらを使用して既存のデータ ソースにアクセスしたり、アプリケーション データを管理したりする方法を示します。  
  
## <a name="see-also"></a>関連項目

- [DataSet、DataTable、および DataView](index.md)
- [ADO.NET の概要](../ado-net-overview.md)
