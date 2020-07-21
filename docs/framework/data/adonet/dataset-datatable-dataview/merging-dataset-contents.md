---
title: DataSet の内容のマージ
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: e5e9309a-3ebb-4a9c-9d78-21c4e2bafc5b
ms.openlocfilehash: abc9183666602a7ef369e690e3ae499f8c7b8b11
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2019
ms.locfileid: "70784399"
---
# <a name="merging-dataset-contents"></a>DataSet の内容のマージ

<xref:System.Data.DataSet.Merge%2A> メソッドを使用して、<xref:System.Data.DataSet>、<xref:System.Data.DataTable>、または <xref:System.Data.DataRow> の配列の内容を既存の `DataSet` にマージできます。 いくつかの要因とオプションが、新しいデータを既存の `DataSet` にマージする方法に影響します。

## <a name="primary-keys"></a>主キー

マージによって新しいデータとスキーマを受け取るテーブルに主キーがある場合、受信データの新しい行と、<xref:System.Data.DataRowVersion.Original> 行バージョンの主キーの値が受信データの主キーの値と同じである既存の行が照合されます。 受信スキーマの列が既存のスキーマの列と一致する場合、既存の行にあるデータが変更されます。 既存のスキーマと一致しない列は、<xref:System.Data.Common.DataAdapter.MissingSchemaAction%2A> パラメーターに基づいて無視または追加されます。 主キーの値が既存の行と一致しない新しい行は、既存のテーブルに追加されます。

受信する行または既存の行の状態が <xref:System.Data.DataRowState.Added> の場合、<xref:System.Data.DataRowVersion.Current> 行バージョンが存在しないため、`Added` の行の `Original` 行バージョンの主キーの値を使用して、その 2 つの行の主キーの値を照合します。

受信テーブルと既存のテーブルに、名前が同じでデータ型が異なる列が含まれている場合、例外がスローされ、<xref:System.Data.DataSet.MergeFailed> の `DataSet` イベントが発生します。 受信テーブルと既存のテーブルの両方にキーが定義されていても、主キーの対象の列が異なる場合、例外がスローされ、`MergeFailed` の `DataSet` イベントが発生します。

マージによって新しいデータを受け取るテーブルに主キーがない場合、受信データの新しい行とそのテーブルの既存の行は一致しません。その代わりに新しい行が既存のテーブルに追加されます。

## <a name="table-names-and-namespaces"></a>テーブル名と名前空間

<xref:System.Data.DataTable> オブジェクトには、<xref:System.Data.DataTable.Namespace%2A> プロパティ値を割り当てることができます。 <xref:System.Data.DataTable.Namespace%2A> の値が割り当てられている場合、<xref:System.Data.DataSet> には、<xref:System.Data.DataTable> の値が同じである複数の <xref:System.Data.DataTable.TableName%2A> オブジェクトを含めることができます。 マージ操作の際には、<xref:System.Data.DataTable.TableName%2A> と <xref:System.Data.DataTable.Namespace%2A> の両方を使用してマージの対象を識別します。 <xref:System.Data.DataTable.Namespace%2A> が割り当てられていない場合、<xref:System.Data.DataTable.TableName%2A> のみを使用してマージの対象を識別します。

> [!NOTE]
> この動作は .NET Framework version 2.0 で変更されました。 .NET Framework version 1.1 では、名前空間はサポートされていましたが、マージ操作中には無視されました。 そのため、<xref:System.Data.DataSet> プロパティ値を使用する <xref:System.Data.DataTable.Namespace%2A> の動作は、実行されている .NET Framework のバージョンに応じて変わります。 たとえば、`DataSets` を含む 2 つの `DataTables` があり、どちらの <xref:System.Data.DataTable.TableName%2A> プロパティの値も同じですが、<xref:System.Data.DataTable.Namespace%2A> プロパティの値が異なっているとします。 .NET Framework 1.1 では、この 2 つの <xref:System.Data.DataTable.Namespace%2A> オブジェクトをマージするときには <xref:System.Data.DataSet> の名前の違いが無視されます。 しかし、バージョン 2.0 以降では、マージを実行すると対象の `DataTables` に新しい <xref:System.Data.DataSet> が 2 つ作成されます。 元の `DataTables` はマージの影響を受けません。

## <a name="preservechanges"></a>PreserveChanges

`DataSet`、`DataTable`、または `DataRow` の各配列を `Merge` メソッドに渡すときに、オプション パラメーターを含めることができます。そのパラメーターを使用して、変更内容を既存の `DataSet` に保存するかどうか、および受信データで見つかった新しいスキーマの要素を処理する方法を指定します。 受信データの後に続く最初のオプション パラメーターは、Boolean 型のフラグ <xref:System.Data.LoadOption.PreserveChanges> で、変更内容を既存の `DataSet` に保存するかどうかを指定します。 `PreserveChanges` フラグを `true` に設定した場合、既存の行の `Current` 行バージョンの値は受信する値で上書きされません。 `PreserveChanges` フラグを `false` に設定した場合、既存の行の `Current` 行バージョンの値が受信した値で上書きされます。 `PreserveChanges` フラグを指定しない場合は、既定で `false` に設定されます。 行バージョンについて詳しくは、「[行の状態とバージョン](row-states-and-row-versions.md)」をご覧ください。

`PreserveChanges` を `true` に設定すると、既存の行のデータは <xref:System.Data.DataRowVersion.Current> 行バージョンで保存されますが、既存の行の <xref:System.Data.DataRowVersion.Original> 行バージョンのデータは受信した行の `Original` 行バージョンのデータで上書きされます。 既存の行の <xref:System.Data.DataRow.RowState%2A> は、<xref:System.Data.DataRowState.Modified> に設定されます。 適用される例外を次に示します。

- 既存の行の `RowState` が `Deleted` の場合、この `RowState` は `Deleted` のままであり、`Modified` には設定されません。 この場合、受信した行のデータは既存の行の `Original` 行バージョンとして保存され、既存の行の `Original` 行バージョンのデータが上書きされます (受信する行の `RowState` が `Added` でない場合)。

- 受信した行の `RowState` が `Added` の場合、受信した行には `Original` 行バージョンが存在しないため、既存の行の `Original` 行バージョンのデータは受信した行のデータで上書きされません。

`PreserveChanges` が `false` の場合、既存の行の `Current` と `Original` の両方の行バージョンが受信した行のデータで上書きされます。さらに、既存の行の `RowState` が、受信した行の `RowState` に設定されます。 適用される例外を次に示します。

- 受信した行の `RowState` が `Unchanged` であり、既存の行の `RowState` が `Modified`、`Deleted`、または `Added` である場合、既存の行の `RowState` は `Modified` に設定されます。

- 受信した行の `RowState` が `Added` であり、既存の行の `RowState` が `Unchanged`、`Modified`、または `Deleted` である場合、既存の行の `RowState` は `Modified` に設定されます。 また、受信した行には `Original` 行バージョンが存在しないため、既存の行の `Original` 行バージョンのデータは、受信した行のデータで上書きされません。

## <a name="missingschemaaction"></a>MissingSchemaAction

<xref:System.Data.MissingSchemaAction> メソッドのオプションである `Merge` パラメーターを使用して、既存の `Merge` に含まれない受信データのスキーマ要素を `DataSet` で処理する方法を指定できます。

次の表で、`MissingSchemaAction` のオプションについて説明します。

|MissingSchemaAction のオプション|説明|
|--------------------------------|-----------------|
|<xref:System.Data.MissingSchemaAction.Add>|新しいスキーマ情報を `DataSet` に追加し、受信した値を新しい列に読み込みます。 既定値です。|
|<xref:System.Data.MissingSchemaAction.AddWithKey>|新しいスキーマおよび主キーの情報を `DataSet` に追加し、受信した値を新しい列に読み込みます。|
|<xref:System.Data.MissingSchemaAction.Error>|一致しないスキーマ情報が見つかった場合、例外をスローします。|
|<xref:System.Data.MissingSchemaAction.Ignore>|新しいスキーマ情報を無視します。|

## <a name="constraints"></a>制約

`Merge` メソッドでは、新しいデータがすべて既存の `DataSet` に追加されるまで制約がチェックされません。 データが追加されると、`DataSet` の現在の値に制約が適用されます。 開発者は、制約違反のためにスローされる例外をコードで処理する必要があります。

`DataSet` 内に、`Unchanged` に設定され、主キー値が 1 である既存の行があるとします。 マージ操作の際、受信した行が `Modified` に設定され、`Original` 行バージョンの主キーの値が 2 であり、`Current` 行バージョンの主キーの値が 1 である場合、`Original` 行バージョンの主キーの値が一致しないため、既存の行と受信した行は一致していると見なされません。 マージが完了し、制約がチェックされると、`Current` 行バージョンの主キーの値が主キー列の UNIQUE 制約に違反するため、例外がスローされます。

> [!NOTE]
> ID 列などの自動インクリメント列を含むデータベース テーブルに行を挿入すると、挿入によって返される ID 列の値が `DataSet` の列の値と一致せず、返された列がマージされずに追加されることがあります。 詳しくは、「[ID 値および Autonumber 値の取得](../retrieving-identity-or-autonumber-values.md)」をご覧ください。

次のコード例では、スキーマが異なる 2 つの `DataSet` オブジェクトをマージし、2 つの受信 `DataSet` オブジェクトが組み合わされたスキーマを持つ 1 つの `DataSet` を作成します。

[!code-csharp[DataWorks DataSet.Merge#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks DataSet.Merge/CS/source.cs#1)]
[!code-vb[DataWorks DataSet.Merge#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks DataSet.Merge/VB/source.vb#1)]

次のコード サンプルでは、更新内容を含む既存の `DataSet` を取得し、その更新内容を `DataAdapter` に渡してデータ ソースで処理します。 次に、その結果を元の `DataSet` にマージします。 エラーとなった変更内容が拒否された後、マージされた変更内容が `AcceptChanges` を使用してコミットされます。

[!code-csharp[DataWorks DataSet.MergeAcceptChanges#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks DataSet.MergeAcceptChanges/CS/source.cs#1)]
[!code-vb[DataWorks DataSet.MergeAcceptChanges#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks DataSet.MergeAcceptChanges/VB/source.vb#1)]

[!code-csharp[DataWorks DataSet.MergeAcceptChanges#2](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks DataSet.MergeAcceptChanges/CS/source.cs#2)]
[!code-vb[DataWorks DataSet.MergeAcceptChanges#2](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks DataSet.MergeAcceptChanges/VB/source.vb#2)]

## <a name="see-also"></a>関連項目

- [DataSet、DataTable、および DataView](index.md)
- [行の状態とバージョン](row-states-and-row-versions.md)
- [DataAdapter と DataReader](../dataadapters-and-datareaders.md)
- [ADO.NET でのデータの取得および変更](../retrieving-and-modifying-data.md)
- [ID 値および Autonumber 値の取得](../retrieving-identity-or-autonumber-values.md)
- [ADO.NET の概要](../ado-net-overview.md)
