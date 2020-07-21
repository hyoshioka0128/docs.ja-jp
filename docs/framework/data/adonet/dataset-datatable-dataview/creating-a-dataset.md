---
title: DataSet の作成
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 57629d8f-393e-4677-8b83-29ffde27f5fc
ms.openlocfilehash: d496167b7bce31491402414c43ae0bcdee423b89
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2019
ms.locfileid: "70786509"
---
# <a name="creating-a-dataset"></a>DataSet の作成
<xref:System.Data.DataSet> のインスタンスを作成するには、<xref:System.Data.DataSet> のコンストラクターを呼び出します。 必要に応じて、引数 name を指定します。 名前を指定しない場合、<xref:System.Data.DataSet> の名前は "NewDataSet" に設定されます。  
  
 また、既存の <xref:System.Data.DataSet> に基づいて新しい <xref:System.Data.DataSet> を作成することもできます。 既存の <xref:System.Data.DataSet> の正確なコピーを新しい <xref:System.Data.DataSet> として作成できるのは、リレーショナル構造またはスキーマはコピーするけれども既存の <xref:System.Data.DataSet> からのデータは含まない <xref:System.Data.DataSet> のクローン、または <xref:System.Data.DataSet> メソッドを使用して既存の <xref:System.Data.DataSet> から変更された行だけを含む <xref:System.Data.DataSet.GetChanges%2A> のサブセットのいずれかです。 詳しくは、「[DataSet の内容のコピー](copying-dataset-contents.md)」をご覧ください。  
  
 <xref:System.Data.DataSet> のインスタンスの作成方法を示すコード例を次に示します。  
  
```vb  
Dim customerOrders As DataSet = New DataSet("CustomerOrders")  
```  
  
```csharp  
DataSet customerOrders = new DataSet("CustomerOrders");  
```  
  
## <a name="see-also"></a>関連項目

- [DataAdapter からの DataSet の読み込み](../populating-a-dataset-from-a-dataadapter.md)
- [DataSet、DataTable、および DataView](index.md)
- [ADO.NET の概要](../ado-net-overview.md)
