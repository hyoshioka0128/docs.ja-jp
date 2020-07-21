---
title: DataSet への DataTable の追加
description: このコード例を参照して、DataTable オブジェクトを作成し、ADO.NET 内の既存の DataSet に追加する方法を学習します。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 556d29a3-8fc9-4e38-b3ee-c188f7e7b155
ms.openlocfilehash: 42bd36b394de560884a2ec607f4cbc65d1171e4e
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84286961"
---
# <a name="adding-a-datatable-to-a-dataset"></a>DataSet への DataTable の追加
ADO.NET を使用して <xref:System.Data.DataTable> オブジェクトを作成し、そのオブジェクトを既存の <xref:System.Data.DataSet> に追加できます。 <xref:System.Data.DataTable> プロパティと <xref:System.Data.DataTable.PrimaryKey%2A> プロパティを使用することで、<xref:System.Data.DataColumn.Unique%2A> の制約情報を設定できます。  
  
## <a name="example"></a>例  
 <xref:System.Data.DataSet> を構築し、<xref:System.Data.DataTable> に新しい <xref:System.Data.DataSet> オブジェクトを追加してから、3 つの <xref:System.Data.DataColumn> オブジェクトをそのテーブルに追加する例を次に示します。 コードの最後では、1 つの列が主キーの列として設定されています。  
  
 [!code-csharp[DataWorks Data.DataTableAdd#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks Data.DataTableAdd/CS/source.cs#1)]
 [!code-vb[DataWorks Data.DataTableAdd#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks Data.DataTableAdd/VB/source.vb#1)]  
  
## <a name="case-sensitivity"></a>大文字と小文字の区別  
 大文字と小文字の区別が異なれば、<xref:System.Data.DataSet> に存在する 2 つ以上のテーブルまたはリレーションが同じ名前を持つことができます。 この場合、名前を使用してテーブルとリレーションを参照する際に大文字と小文字が区別されます。 たとえば、 <xref:System.Data.DataSet> **dataSet** にテーブル **Table1** と **table1** が含まれる場合、**Table1** を参照するには **dataSet.Tables["Table1"]** 、**table1** を参照するには **dataSet.Tables ["table1"]** と名前を指定します。 このいずれかのテーブルの参照に **dataSet.Tables["TABLE1"]** と指定すると、例外が発生します。  
  
 特定の名前を持つテーブルまたはリレーションが 1 つのみの場合、大文字と小文字は区別されません。 たとえば、<xref:System.Data.DataSet> に **Table1** しか存在しない場合は、**dataSet.Tables["TABLE1"]** を使用してそのテーブルを参照できます。  
  
> [!NOTE]
> この動作は <xref:System.Data.DataSet.CaseSensitive%2A> の <xref:System.Data.DataSet> プロパティの影響を受けません。 <xref:System.Data.DataSet.CaseSensitive%2A> プロパティは、<xref:System.Data.DataSet> 内のデータに適用され、並べ替え、検索、フィルター処理、制約の適用などに影響を及ぼします。  
  
## <a name="namespace-support"></a>名前空間のサポート  
 2\.0 より前のバージョンの ADO.NET では、異なる名前空間に存在しているテーブルであっても、2 つのテーブルが同じ名前を持つことはできませんでした。 ADO.NET 2.0 には、この制限はありません。 したがって、<xref:System.Data.DataSet> に、<xref:System.Data.DataTable.TableName%2A> プロパティ値が異なり、<xref:System.Data.DataTable.Namespace%2A> プロパティ値が一致する 2 つのテーブルが存在しても問題ありません。  
  
## <a name="see-also"></a>関連項目

- [DataSet、DataTable、および DataView](index.md)
- [ADO.NET の概要](../ado-net-overview.md)
