---
title: データセット
description: メモリ内に常駐するデータ表現で、ADO.NET のデータ ソースの違いにかかわらず、一貫性のあるリレーショナル プログラミング モデルを提供する、DataSet について説明します。
ms.date: 03/30/2017
ms.assetid: 82b641bb-6001-4512-bf1a-2830acdd92ab
ms.openlocfilehash: 2fc5963937f7bf15dc192c6dc0a980d544a23194
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84287130"
---
# <a name="adonet-datasets"></a>ADO.NET データセット
<xref:System.Data.DataSet> オブジェクトは、ADO.NET で非接続型分散データ シナリオをサポートするうえで中心的な役割を果たします。 **DataSet** はメモリ内に常駐するデータ表現であり、データ ソースの違いにかかわらず、一貫性のあるリレーショナル プログラミング モデルを提供します。 複数の異なるデータ ソースや XML データと組み合わせて使用でき、アプリケーションにとってローカルなデータの管理にも使用できます。 **DataSet** では、関連テーブル、制約、およびテーブル間のリレーションシップを含む、完全なデータ セットが表されます。 次の図は、**DataSet** オブジェクト モデルを示したものです。  
  
 ![ADO.NET の図](./media/ado-1-bpuedev11.png "ado_1_bpuedev11")  
DataSet オブジェクト モデル  
  
 1 つの **DataSet** に含まれるメソッドとオブジェクトは、リレーショナル データベース モデルに含まれるメソッドやオブジェクトと整合性があります。  
  
 **DataSet** では、その内容を XML として、またそのスキーマを XML スキーマ定義言語 (XSD) スキーマとして、永続化したり再度読み込んだりできます。 詳しくは、「[DataSet での XML の使用](./dataset-datatable-dataview/using-xml-in-a-dataset.md)」を参照してください。  
  
## <a name="the-datatablecollection"></a>DataTableCollection  
 ADO.NET の **DataSet** には、<xref:System.Data.DataTable> オブジェクトによって表わされる 0 個以上のテーブルのコレクションが含まれます。 <xref:System.Data.DataTableCollection> には、**DataSet** 内のすべての **DataTable** オブジェクトが含まれます。  
  
 **DataTable** は <xref:System.Data> 名前空間で定義されており、メモリ常駐データの 1 つのテーブルを表わします。 このテーブルには、共にテーブルのスキーマを定義する <xref:System.Data.DataColumnCollection> で表現される列と <xref:System.Data.ConstraintCollection> で表現される制約のコレクションが含まれます。 **DataTable** には、<xref:System.Data.DataRowCollection> によって表わされる行のコレクションも含まれ、それにはテーブル内のデータが含まれます。 <xref:System.Data.DataRow> には、行に格納された値の変更を識別できるように、行の現在の状態と共に、行の現在のバージョンと元のバージョンの両方が保持されます。  
  
## <a name="the-dataview-class"></a>DataView クラス  
 <xref:System.Data.DataView> では、<xref:System.Data.DataTable> に格納されているデータのさまざまなビューを作成できます。この機能は、データ連結アプリケーションで頻繁に使用されます。 <xref:System.Data.DataView> を使用すると、テーブルのデータをさまざまな並べ替え順序で公開したり、行の状態やフィルター式に基づいてデータをフィルター処理したりできます。 詳しくは、「[DataView](./dataset-datatable-dataview/dataviews.md)」をご覧ください。  
  
## <a name="the-datarelationcollection"></a>DataRelationCollection  
 **DataSet** の <xref:System.Data.DataRelationCollection> オブジェクトには、リレーションシップが含まれます。 <xref:System.Data.DataRelation> オブジェクトによって表されるリレーションシップでは、ある **DataTable** の行と別の **DataTable** の行が関連付けられます。 リレーションシップは、リレーショナル データベースの主キー列と外部キー列の間に存在する結合パスに似ています。 **DataRelation** では、1 つの **DataSet** の 2 つのテーブルで一致する列が識別されます。  
  
 リレーションシップを使用すると、**DataSet** 内の、あるテーブルと別のテーブルを行き来できます。 **DataRelation** の必須要素は、リレーションシップの名前、関連付けられているテーブルの名前、各テーブル内の関連する列です。 <xref:System.Data.DataColumn> オブジェクトの配列をキー列として指定することによって、テーブルごとに複数の列を使用してリレーションシップを構築できます。 <xref:System.Data.DataRelationCollection> にリレーションシップを追加するときに、必要に応じて **UniqueKeyConstraint** と **ForeignKeyConstraint** を追加し、関連する列の値が変更されたときの整合性制約を適用できます。  
  
 詳しくは、「[DataRelation の追加](./dataset-datatable-dataview/adding-datarelations.md)」をご覧ください。  
  
## <a name="xml"></a>XML  
 XML ストリームまたは XML ドキュメントから **DataSet** を設定できます。 XML ストリームまたは XML ドキュメントを使用して **DataSet** に提供できるのは、データまたはスキーマ情報のいずれか、あるいはその両方です。 XML のストリームまたはドキュメントから提供される情報を、**DataSet** に既に存在するデータまたはスキーマ情報と組み合わせることもできます。 詳しくは、「[DataSet での XML の使用](./dataset-datatable-dataview/using-xml-in-a-dataset.md)」を参照してください。  
  
## <a name="extendedproperties"></a>ExtendedProperties  
 **DataSet**、**DataTable**、**DataColumn** のすべてに、**ExtendedProperties** プロパティがあります。 **ExtendedProperties** は **PropertyCollection** であり、ここには、結果セットの生成に使われた SELECT ステートメントやデータが生成された時刻など、独自の情報を格納できます。 **ExtendedProperties** コレクションは、**DataSet** のスキーマ情報と共に永続化されます。  
  
## <a name="linq-to-dataset"></a>LINQ to DataSet  
 LINQ to DataSet では、DataSet に格納された非接続型データに対する統合言語クエリ機能が提供されます。 LINQ to DataSet では標準の LINQ 構文が使用されており、Visual Studio IDE を使用するとコンパイル時の構文チェック、静的な型指定、IntelliSense のサポートが提供されます。  
  
 詳細については、「[LINQ to DataSet](linq-to-dataset.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- [ADO.NET の概要](ado-net-overview.md)
- [DataSet、DataTable、および DataView](./dataset-datatable-dataview/index.md)
- [ADO.NET でのデータの取得および変更](retrieving-and-modifying-data.md)
