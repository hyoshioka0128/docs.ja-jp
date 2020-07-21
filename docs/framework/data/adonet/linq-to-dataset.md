---
title: LINQ to DataSet
ms.date: 03/30/2017
ms.assetid: 743e3755-3ecb-45a2-8d9b-9ed41f0dcf17
ms.openlocfilehash: 4995512336ee9eb6e33df011757ed533db57e76e
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2019
ms.locfileid: "70783789"
---
# <a name="linq-to-dataset"></a>LINQ to DataSet
LINQ to DataSet を使うと、<xref:System.Data.DataSet> オブジェクトにキャッシュされたデータに対するクエリを、いっそう簡単かつ高速に実行できるようになります。 具体的には、LINQ to DataSet では、クエリを記述するのにクエリ言語ではなくプログラミング言語そのものを使用できるので、クエリ操作が容易になります。 これは、Visual Studio 開発者にとって特に便利で、Visual Studio によって提供されるコンパイル時の構文チェック、静的な型指定、IntelliSense のサポートをクエリで利用できるようになります。  
  
 また、LINQ to DataSet を使用すると、1 つまたは複数のデータ ソースから取得して統合したデータを照会することもできます。 これにより、ローカルに集計されたデータのクエリや Web アプリケーションでの中間層のキャッシュなど、データの表現方法や扱いに柔軟性が要求されるさまざまなシナリオが実現します。 特に、汎用のレポート作成、分析、ビジネス インテリジェンスを行うアプリケーションでは、この手法を用いたデータ操作が欠かせません。  
  
 LINQ to DataSet の機能は、主に <xref:System.Data.DataRowExtensions> クラスと <xref:System.Data.DataTableExtensions> クラスの拡張メソッドを通して公開されます。 LINQ to DataSet は、既存の ADO.NET アーキテクチャを基にして構築され、それを使用するようになっており、アプリケーション コードで ADO.NET に代わるものではありません。 既存の ADO.NET コードは、LINQ to DataSet アプリケーションでも引き続き機能します。 LINQ to DataSet と ADO.NET の関係およびデータ ストアを、次の図に示します。  
  
 ![LINQ to DataSet が ADO.NET プロバイダーに基づいていることを示す図。](./media/linq-to-dataset/linq-dataset-ado-dotnet-provider.gif)  
  
## <a name="in-this-section"></a>このセクションの内容  
 [はじめに](getting-started-linq-to-dataset.md)  
  
 [プログラミング ガイド](programming-guide-linq-to-dataset.md)  
  
## <a name="reference"></a>関連項目  
 <xref:System.Data.DataTableExtensions>  
  
 <xref:System.Data.DataRowExtensions>  
  
 <xref:System.Data.DataRowComparer>  
  
## <a name="see-also"></a>関連項目

- [統合言語クエリ (LINQ) - C#](../../../csharp/programming-guide/concepts/linq/index.md)
- [統合言語クエリ (LINQ) - Visual Basic](../../../visual-basic/programming-guide/concepts/linq/index.md)
- [LINQ と ADO.NET](linq-and-ado-net.md)
- [ADO.NET](index.md)
