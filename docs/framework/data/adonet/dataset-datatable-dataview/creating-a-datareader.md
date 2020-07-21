---
title: DataReader の作成
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 49d4422a-7464-4ab8-8ec7-90185fde3ecf
ms.openlocfilehash: 696eb4dfc334390e1968dd317d441f3c987a1f77
ms.sourcegitcommit: ad800f019ac976cb669e635fb0ea49db740e6890
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/29/2019
ms.locfileid: "73040109"
---
# <a name="creating-a-datareader"></a>DataReader の作成
<xref:System.Data.DataTable> クラスおよび <xref:System.Data.DataSet> クラスには、<xref:System.Data.DataTable.CreateDataReader%2A> の内容または <xref:System.Data.DataTable> オブジェクトの <xref:System.Data.DataSet> コレクションの内容を、読み取り専用で前方参照専用の 1 つ以上の結果セットとして返す <xref:System.Data.DataSet.Tables%2A> メソッドがあります。  
  
## <a name="example"></a>例  
 <xref:System.Data.DataTable> インスタンスを作成するコンソール アプリケーションの例を次に示します。 その後、データが格納された <xref:System.Data.DataTable> を、<xref:System.Data.DataTable.CreateDataReader%2A> メソッドを呼び出すプロシージャに渡し、そこで <xref:System.Data.DataTableReader> 内に格納された結果の反復処理が行われます。  
  
 [!code-csharp[DataWorks DataTable.CreateDataReader#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks DataTable.CreateDataReader/CS/source.cs#1)]
 [!code-vb[DataWorks DataTable.CreateDataReader#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks DataTable.CreateDataReader/VB/source.vb#1)]  
  
 この例では、次の出力がコンソール ウィンドウに表示されます。  
  
```output  
1 Mary  
2 Andy  
3 Peter  
4 Russ  
```  
  
## <a name="see-also"></a>関連項目

- <xref:System.Data.DataTable.CreateDataReader%2A>
- <xref:System.Data.DataSet.CreateDataReader%2A>
- [DataTableReaders](datatablereaders.md)
- [ADO.NET の概要](../ado-net-overview.md)
