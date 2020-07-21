---
title: DataSet のイベント処理
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 54edefe0-bc38-419b-b486-3d8a0c356f13
ms.openlocfilehash: b2b71dac58838a826933af570934bf4bbb35e025
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2019
ms.locfileid: "70784608"
---
# <a name="handling-dataset-events"></a>DataSet のイベント処理
<xref:System.Data.DataSet> オブジェクトには、 <xref:System.ComponentModel.MarshalByValueComponent.Disposed>、 <xref:System.Data.DataSet.Initialized>、 <xref:System.Data.DataSet.MergeFailed>という 3 つのイベントがあります。  
  
## <a name="the-mergefailed-event"></a>MergeFailed イベント  
 `DataSet` オブジェクトのイベントの中で最も使用頻度が高いイベントは、マージしようとしている `MergeFailed`オブジェクトのスキーマが競合する場合に発生する `DataSet` です。 この状況は、ターゲットとソースの <xref:System.Data.DataRow> が同じ主キー値を持ち、なおかつ、 <xref:System.Data.DataSet.EnforceConstraints%2A> プロパティが `true`に設定されている場合に発生します。 たとえば、マージ対象のテーブルの主キーの列が 2 つの `DataSet` オブジェクトのテーブル間で同じ場合、例外がスローされ、 `MergeFailed` イベントが発生します。 <xref:System.Data.MergeFailedEventArgs> イベントに渡される `MergeFailed` オブジェクトには、2 つの <xref:System.Data.MergeFailedEventArgs.Conflict%2A> オブジェクト間のスキーマで発生した競合を示す `DataSet` プロパティ、および競合が発生したテーブルの名前を示す <xref:System.Data.MergeFailedEventArgs.Table%2A> プロパティがあります。  
  
 次のコードは、 `MergeFailed` イベントのイベント ハンドラーを追加する方法を示しています。  
  
```vb  
AddHandler workDS.MergeFailed, New MergeFailedEventHandler( _  
  AddressOf DataSetMergeFailed)  
  
Private Shared Sub DataSetMergeFailed(  _  
  sender As Object,args As MergeFailedEventArgs)  
  Console.WriteLine("Merge failed for table " & args.Table.TableName)  
  Console.WriteLine("Conflict = " & args.Conflict)  
End Sub  
```  
  
```csharp  
workDS.MergeFailed += new MergeFailedEventHandler(DataSetMergeFailed);  
  
private static void DataSetMergeFailed(  
  object sender, MergeFailedEventArgs args)  
{  
  Console.WriteLine("Merge failed for table " + args.Table.TableName);  
  Console.WriteLine("Conflict = " + args.Conflict);  
}  
```  
  
## <a name="the-initialized-event"></a>Initialized イベント  
 <xref:System.Data.DataSet.Initialized> イベントは、 `DataSet` のコンストラクターによって `DataSet`の新しいインスタンスが初期化された後に発生します。  
  
 <xref:System.Data.DataSet.IsInitialized%2A> プロパティは、 `true` の初期化が完了した場合に `DataSet` を返します。それ以外の場合は `false`を返します。 この値は、 <xref:System.Data.DataSet.BeginInit%2A> の初期化を開始する `DataSet`メソッドによって <xref:System.Data.DataSet.IsInitialized%2A> が `false`に設定されます。 また、 <xref:System.Data.DataSet.EndInit%2A> の初期化を終了する `DataSet`メソッドによって `true`に設定されます。 これらのメソッドは、別のコンポーネントによって使用されている `DataSet` を初期化するために、Visual Studio のデザイン環境によって使用されます。 通常、コード内で直接使用することはありません。  
  
## <a name="the-disposed-event"></a>Disposed イベント  
 `DataSet` は、 <xref:System.ComponentModel.MarshalByValueComponent> メソッドおよび <xref:System.ComponentModel.MarshalByValueComponent.Dispose%2A> イベントの両方を公開する <xref:System.ComponentModel.MarshalByValueComponent.Disposed> クラスから派生しています。 <xref:System.ComponentModel.MarshalByValueComponent.Disposed> イベントでは、コンポーネントが破棄されたことを伝えるイベントをリッスンするためのイベント ハンドラーが追加されます。 <xref:System.ComponentModel.MarshalByValueComponent.Dispose%2A> メソッドが呼び出されたときにコードを実行したい場合は、`DataSet` の <xref:System.ComponentModel.MarshalByValueComponent.Disposed> イベントを使用できます。 <xref:System.ComponentModel.MarshalByValueComponent.Dispose%2A> では、<xref:System.ComponentModel.MarshalByValueComponent> によって使用されたリソースが解放されます。  
  
> [!NOTE]
> `DataSet` オブジェクトと `DataTable` オブジェクトでは、<xref:System.ComponentModel.MarshalByValueComponent> が継承されていて、リモート処理用の <xref:System.Runtime.Serialization.ISerializable> インターフェイスがサポートされています。 これらは、リモート処理ができる唯一の ADO.NET オブジェクトです。 詳しくは、「[.NET リモート処理](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/72x4h507(v=vs.100))」をご覧ください。  
  
 `DataSet` を操作するときに使用できる他のイベントについては、「[DataTable イベントの処理](handling-datatable-events.md)」および「[DataAdapter のイベント処理](../handling-dataadapter-events.md)」をご覧ください。  
  
## <a name="see-also"></a>関連項目

- [DataSet、DataTable、および DataView](index.md)
- [データの検証](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/t3b36awf(v=vs.120))
- [ADO.NET でのデータの取得および変更](../retrieving-and-modifying-data.md)
- [ADO.NET の概要](../ado-net-overview.md)
