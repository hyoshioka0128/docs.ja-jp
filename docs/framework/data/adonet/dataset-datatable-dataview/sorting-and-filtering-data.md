---
title: データの並べ替えとフィルター処理
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: fdd9c753-39df-48cd-9822-2781afe76200
ms.openlocfilehash: 09cee2f2b2c3288c835912c9f311bf2511c7b0d0
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2019
ms.locfileid: "70785914"
---
# <a name="sorting-and-filtering-data"></a>データの並べ替えとフィルター処理
<xref:System.Data.DataView> には、<xref:System.Data.DataTable> のデータの並べ替えとフィルター処理を行うさまざまな方法が用意されています。  
  
- <xref:System.Data.DataView.Sort%2A> プロパティを使用すれば、1 列または複数列の並べ替え順序を指定し、ASC (昇順) パラメーターと DESC (降順) パラメーターを含めることができます。  
  
- <xref:System.Data.DataView.ApplyDefaultSort%2A> プロパティを使用すると、テーブルの主キー列 (1 列または複数列) に基づいて、昇順の並べ替え順序を自動的に作成できます。 **Sort** プロパティが null 参照または空の文字列の場合、およびテーブルに主キーが定義されている場合は、<xref:System.Data.DataView.ApplyDefaultSort%2A> だけが適用されます。  
  
- <xref:System.Data.DataView.RowFilter%2A> プロパティを使用すると、列の値に基づいて行のサブセットを指定できます。 **RowFilter** プロパティの有効な式の詳細については、<xref:System.Data.DataColumn> クラスの <xref:System.Data.DataColumn.Expression%2A> プロパティの情報を参照してください。  
  
     データ サブセットの動的ビューの作成とは対照的に、データに対して特定のクエリの実行結果を返す場合、パフォーマンスを最大限に引き出すには、**RowFilter** プロパティを設定する代わりに **DataView** の <xref:System.Data.DataView.Find%2A> メソッドまたは <xref:System.Data.DataView.FindRows%2A> メソッドを使用します。 **RowFilter** プロパティを設定すると、データのインデックスが再作成され、アプリケーションのオーバーヘッドが増加してパフォーマンスの低下を招きます。 **RowFilter** プロパティは、データ連結アプリケーションでの使用に適しています。このアプリケーションでは、連結されたコントロールによってフィルター処理結果が表示されます。 **Find** メソッドと **FindRows** メソッドでは、現在のインデックスが使用されます。このため、インデックスを再作成する必要はありません。 **Find** メソッドと **FindRows** メソッドの詳細については、「[行の検索](finding-rows.md)」を参照してください。  
  
- <xref:System.Data.DataView.RowStateFilter%2A> プロパティを使用して、表示する行バージョンを指定できます。 **DataView** では、基になる行の **RowState** に応じて、公開する行バージョンが暗黙的に管理されます。 たとえば、**RowStateFilter** が **DataViewRowState.Deleted** に設定されている場合は、**Current** 行バージョンが存在しないため、**DataView** ではすべての **Deleted** 行の **Original** 行バージョンが公開されます。 **DataRowView** の **RowVersion** プロパティを使用すると、公開される行のバージョンを確認できます。  
  
     **DataViewRowState** のオプションを次の表に示します。  
  
    |DataViewRowState のオプション|説明|  
    |------------------------------|-----------------|  
    |**CurrentRows**|すべての **Unchanged** 行、**Added** 行、**Modified** 行の **Current** 行バージョン。 既定値です。|  
    |**追加**|すべての **Added** 行の **Current** 行バージョン。|  
    |**削除済み**|すべての **Deleted** 行の **Original** 行バージョン。|  
    |**ModifiedCurrent**|すべての **Modified** 行の **Current** 行バージョン。|  
    |**ModifiedOriginal**|すべての **Modified** 行の **Original** 行バージョン。|  
    |**None**|行がありません。|  
    |**OriginalRows**|すべての **Unchanged** 行、**Modified** 行、**Deleted** 行の **Original** 行バージョン。|  
    |**Unchanged**|すべての **Unchanged** 行の **Current** 行バージョン。|  
  
 行の状態と行バージョンの詳細については、「[行の状態とバージョン](row-states-and-row-versions.md)」を参照してください。  
  
 在庫数が標準在庫数以下である製品を、仕入先 ID (supplier ID) で並べ替え、さらに製品名 (product name) で並べ替えたビューを作成するコード サンプルを次に示します。  
  
```vb  
Dim prodView As DataView = New DataView(prodDS.Tables("Products"), _  
   "UnitsInStock <= ReorderLevel", _  
   "SupplierID, ProductName", _  
   DataViewRowState.CurrentRows)  
```  
  
```csharp  
DataView prodView = new DataView(prodDS.Tables["Products"],  
   "UnitsInStock <= ReorderLevel",  
   "SupplierID, ProductName",  
   DataViewRowState.CurrentRows);  
```  
  
## <a name="see-also"></a>関連項目

- <xref:System.Data.DataViewRowState>
- <xref:System.Data.DataColumn.Expression%2A?displayProperty=nameWithType>
- <xref:System.Data.DataTable>
- <xref:System.Data.DataView>
- [DataViews](dataviews.md)
- [ADO.NET の概要](../ado-net-overview.md)
