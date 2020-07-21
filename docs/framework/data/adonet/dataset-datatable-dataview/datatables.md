---
title: DataTables
description: ADO.NET DataTable について説明します。これは、それが存在する .NET ベースのアプリケーションに対してローカルな、インメモリ リレーショナル データの 1 つのテーブルを表します。
ms.date: 03/30/2017
ms.assetid: 52ff0e32-3e5a-41de-9a3b-7b04ea52b83e
ms.openlocfilehash: da6c9201951a6c7916067011c0a4f01ef9fdeffd
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84286909"
---
# <a name="datatables"></a>DataTables
<xref:System.Data.DataSet> は、テーブル、リレーションシップ、および制約のコレクションで構成されます。 ADO.NET では、<xref:System.Data.DataTable> は **DataSet** 内のテーブルを表すために使用されます。 **DataTable** は、1 つのメモリ内のリレーショナル データ テーブルを表します。このテーブルのデータは、そのデータが存在する .NET ベース アプリケーションのローカル データですが、**DataAdapter** を使用して Microsoft SQL Server などのデータ ソースから読み込むこともできます。詳細については、「[DataAdapter からの DataSet の読み込み](../populating-a-dataset-from-a-dataadapter.md)」を参照してください。  
  
 **DataTable** クラスは、.NET Framework クラス ライブラリ内の **System.Data** 名前空間のメンバーです。 **DataTable** は、単独でも **DataSet** のメンバーとしても作成および使用できます。また、**DataTable** オブジェクトは、<xref:System.Data.DataView> などの他の .NET Framework オブジェクトからも使用できます。 **DataSet** 内のテーブルのコレクションには、**DataSet** オブジェクトの **Tables** プロパティを使用してアクセスします。  
  
 テーブルのスキーマ (構造) は、列と制約で表されます。 **DataTable** のスキーマは、<xref:System.Data.DataColumn> オブジェクト共に <xref:System.Data.ForeignKeyConstraint> および <xref:System.Data.UniqueConstraint> オブジェクトを使用して定義します。 テーブルの列は、データ ソースの列に割り当てたり、式で算出された値を格納したり、格納されている値を自動的にインクリメントしたり、主キー値を格納したりできます。  
  
 **DataTable** には、スキーマだけでなく、データを格納して順序付けるための行も必要です。 <xref:System.Data.DataRow> クラスは、テーブルに格納される実際のデータを表します。 **DataRow** およびそのプロパティとメソッドを使用して、テーブル内のデータを取得、評価、および操作できます。 行内のデータがアクセスされて変更されると、**DataRow** オブジェクトには、現在の状態と元の状態が維持されます。  
  
 テーブル間で 1 つ以上の列を関連付け、テーブル間の親子のリレーションシップを作成できます。 **DataTable** オブジェクト間のリレーションシップを作成するには、<xref:System.Data.DataRelation> を使用します。 **DataRelation** オブジェクトを使用すると、特定の行に関連付けられた子の行または親の行を返すことができます。 詳しくは、「[DataRelation の追加](adding-datarelations.md)」をご覧ください。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [DataTable の作成](creating-a-datatable.md)  
 **DataTable** を作成し、それを **DataSet** に追加する方法について説明します。  
  
 [DataTable スキーマの定義](datatable-schema-definition.md)  
 **DataColumn** オブジェクトと制約の作成および使用について説明します。  
  
 [DataTable 内のデータの操作](manipulating-data-in-a-datatable.md)  
 テーブル内のデータを追加、変更、および削除する方法について説明します。 **DataTable** イベントを使用してテーブル内のデータが変更されたかどうかを確認する方法について説明します。  
  
 [DataTable イベントの処理](handling-datatable-events.md)  
 列値が変更された場合や行が追加または削除された場合のイベントなど、**DataTable** で使用できるイベントについて説明します。  
  
## <a name="related-sections"></a>関連項目  
 [ADO.NET](../index.md)  
 ADO.NET のアーキテクチャとコンポーネントについて説明し、ADO.NET を使用して既存のデータ ソースにアクセスしたり、アプリケーション データを管理する方法について説明します。  
  
 [DataSet、DataTable、および DataView](index.md)  
 テーブル間のリレーションシップを作成する方法も含め、ADO.NET の **DataSet** について説明します。  
  
 <xref:System.Data.Constraint>  
 **Constraint** オブジェクトの参照情報を提供します。  
  
 <xref:System.Data.DataColumn>  
 **DataColumn** オブジェクトの参照情報を提供します。  
  
 <xref:System.Data.DataSet>  
 **DataSet** オブジェクトの参照情報を提供します。  
  
 <xref:System.Data.DataTable>  
 **DataTable** オブジェクトの参照情報を提供します。  
  
 [クラス ライブラリの概要](../../../../standard/class-library-overview.md)  
 **System** 名前空間やその下位レベルの名前空間 **System.Data** が含まれる .NET Framework クラス ライブラリの概要について説明します。  
  
## <a name="see-also"></a>関連項目

- [ADO.NET の概要](../ado-net-overview.md)
