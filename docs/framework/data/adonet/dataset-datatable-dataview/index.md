---
title: DataSet、DataTable、および DataView
description: 一貫したリレーショナル プログラミング モデルを提供するメモリ常駐型のデータ表現である、ADO.NET の DataSet を使用するいくつかの方法を学習します。
ms.date: 03/30/2017
ms.assetid: 6d4c4b69-8919-4224-8a65-6cca1c61b48f
ms.openlocfilehash: 53e12f701b9be1938d62f46bbeb6e63d95c03386
ms.sourcegitcommit: e7748001b1cee80ced691d8a76ca814c0b02dd9b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/14/2020
ms.locfileid: "86374508"
---
# <a name="datasets-datatables-and-dataviews"></a>DataSet、DataTable、および DataView

ADO.NET <xref:System.Data.DataSet> はメモリ常駐型のデータ表現であり、含まれているデータ ソースとは関係なく、一貫性のあるリレーショナル プログラミング モデルを提供します。 <xref:System.Data.DataSet> とは、テーブル間のリレーションシップだけでなく、包括するテーブル、整列するテーブル、およびデータを制約するテーブルを含むデータのセットを表します。  
  
<xref:System.Data.DataSet> にはさまざまな使用方法があり、単独または組み合わせで使用できます。 次の操作を行うことができます。  
  
- プログラムを使用して <xref:System.Data.DataTable> 内に <xref:System.Data.DataRelation>、<xref:System.Data.Constraint>、および <xref:System.Data.DataSet> を作成し、テーブルにデータを設定できます。  
  
- <xref:System.Data.DataSet> を使用して、既存のリレーショナル データ ソースから取得したデータのテーブルで `DataAdapter` を作成できます。  
  
- XML を使用して、<xref:System.Data.DataSet> の内容を読み込んだり、永続化したりできます。 詳しくは、「[DataSet での XML の使用](using-xml-in-a-dataset.md)」を参照してください。  
  
厳密に型指定された <xref:System.Data.DataSet> も XML Web サービスを使用して転送できます。 <xref:System.Data.DataSet> は、XML Web サービスを使用してデータの転送が理想的に行えるように設計されています。 XML Web サービスの概要については、「[XML Web サービスの概要](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/w9fdtx28(v=vs.100))」を参照してください。 XML Web サービスから <xref:System.Data.DataSet> を使用する例については、「[XML Web サービスからの DataSet の使用](consuming-a-dataset-from-an-xml-web-service.md)」を参照してください。  
  
## <a name="in-this-section"></a>このセクションの内容

 [セキュリティ ガイダンス](security-guidance.md)  
 <xref:System.Data.DataSet> と <xref:System.Data.DataTable> に関するセキュリティ ガイダンスを提供します。

 [DataSet の作成](creating-a-dataset.md)  
 <xref:System.Data.DataSet> のインスタンス作成に使用する構文について説明します。  
  
 [DataSet への DataTable の追加](adding-a-datatable-to-a-dataset.md)  
 テーブルと列の作成方法および <xref:System.Data.DataSet> への追加方法について説明します。  
  
 [DataRelation の追加](adding-datarelations.md)  
 <xref:System.Data.DataSet> のテーブル間のリレーションを作成する方法について説明します。  
  
 [DataRelation の移動](navigating-datarelations.md)  
 <xref:System.Data.DataSet> のテーブル間のリレーションを使用して、親子のリレーションシップに基づく子または親の行を返す方法について説明します。  
  
 [DataSet の内容のマージ](merging-dataset-contents.md)  
 <xref:System.Data.DataSet>、<xref:System.Data.DataTable>、<xref:System.Data.DataRow> の各配列の内容を別の <xref:System.Data.DataSet> にマージする方法について説明します。  
  
 [DataSet の内容のコピー](copying-dataset-contents.md)  
 指定されたデータだけでなく、スキーマを持つことができる <xref:System.Data.DataSet> のコピーを作成する方法について説明します。  
  
 [DataSet のイベント処理](handling-dataset-events.md)  
 <xref:System.Data.DataSet> のイベントおよびその使用方法について説明します。  
  
 [型指定されたデータセット](typed-datasets.md)  
 型指定された <xref:System.Data.DataSet> の概要と、その作成および使用方法について説明します。  
  
 [DataTables](datatables.md)  
 <xref:System.Data.DataTable> の作成方法、スキーマの定義方法、およびデータの操作方法について説明します。  
  
 [DataTableReaders](datatablereaders.md)  
 <xref:System.Data.DataTableReader> の作成方法および使用方法について説明します。  
  
 [DataViews](dataviews.md)  
 `DataViews` の作成方法および操作方法、および <xref:System.Data.DataView> イベントの操作方法について説明します。  
  
 [DataSet での XML の使用](using-xml-in-a-dataset.md)  
 <xref:System.Data.DataSet> がデータ ソースとして XML と対話する方法を、<xref:System.Data.DataSet> の内容を XML データとして読み込んで永続化する方法と共に説明します。  
  
 [XML Web サービスからの DataSet の使用](consuming-a-dataset-from-an-xml-web-service.md)  
 <xref:System.Data.DataSet> を使用してデータを転送する XML Web サービスを作成する方法について説明します。  
  
## <a name="related-sections"></a>関連項目

 [ADO.NET の新機能](../whats-new.md)  
 ADO.NET の新機能について説明します。  
  
 [ADO.NET の概要](../ado-net-overview.md)  
 ADO.NET のデザインとコンポーネントを紹介します。  
  
 [DataAdapter からの DataSet の読み込み](../populating-a-dataset-from-a-dataadapter.md)  
 **DataSet** にデータ ソースのデータを読み込む方法について説明します。  
  
 [DataAdapter によるデータ ソースの更新](../updating-data-sources-with-dataadapters.md)  
 **DataSet** のデータに加えた変更をデータ ソースに反映する方法について説明します。  
  
 [DataSet への既存の制約の追加](../adding-existing-constraints-to-a-dataset.md)  
 **DataSet** にデータ ソースの主キー情報を設定する方法について説明します。  
  
## <a name="see-also"></a>関連項目

- [ADO.NET](../index.md)
- [ADO.NET の概要](../ado-net-overview.md)
