---
title: DataGridView コントロールのサイズ変更オプション
description: Windows フォーム DataGridView コントロールのサイズ変更オプションについて説明します。 DataGridView の行、列、およびヘッダーは、異なる発生の結果としてサイズが変更されます。
ms.date: 03/30/2017
helpviewer_keywords:
- DataGridView control [Windows Forms], row sizing
- data grids [Windows Forms], column sizing
- DataGridView control [Windows Forms], column sizing
- DataGridView control [Windows Forms], sizing options
- data grids [Windows Forms], row sizing
- data grids [Windows Forms], sizing options
ms.assetid: a5620a9c-0d06-41e3-8934-c25ddb16c9e6
ms.openlocfilehash: 8ddf72c412db74df35bc3f035ff05d1e7e9738d1
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85613723"
---
# <a name="sizing-options-in-the-windows-forms-datagridview-control"></a>Windows フォーム DataGridView コントロールのサイズ変更オプション
<xref:System.Windows.Forms.DataGridView>行、列、およびヘッダーは、さまざまな発生の結果としてサイズを変更できます。 次の表は、これらの出現を示しています。  
  
|個数|説明|  
|----------------|-----------------|  
|ユーザーのサイズ変更|ユーザーは、行、列、またはヘッダーの区切り線をドラッグまたはダブルクリックしてサイズ調整を行うことができます。|  
|コントロールのサイズ変更|列の塗りつぶしモードでは、コントロールの幅が変化したときに列幅が変化します。たとえば、コントロールが親フォームにドッキングされ、ユーザーがフォームのサイズを変更した場合などです。|  
|セル値の変更|コンテンツベースの自動サイズ調整モードでは、新しい表示値に合わせてサイズが変更されます。|  
|メソッド呼び出し|プログラムによるコンテンツベースのサイズ変更では、メソッド呼び出し時のセル値に基づいて、便宜的なサイズ調整を行うことができます。|  
|プロパティの設定|また、特定の高さと幅の値を設定することもできます。|  
  
 既定では、ユーザーのサイズ変更が有効になり、自動サイズ調整が無効になり、列よりも幅の広いセル値がクリップされます。  
  
 次の表は、既定の動作を調整したり、特定のサイズ変更オプションを使用して特定の効果を実現するために使用できるシナリオを示しています。  
  
|シナリオ|実装|  
|--------------|--------------------|  
|列の塗りつぶしモードは、水平スクロールバーを表示せずに、コントロールの幅全体を占める、比較的少数の列に同じサイズのデータを表示する場合に使用します。|<xref:System.Windows.Forms.DataGridView.AutoSizeColumnsMode%2A> プロパティを <xref:System.Windows.Forms.DataGridViewAutoSizeColumnsMode.Fill>に設定します。|  
|さまざまなサイズの表示値を使用して、列フィルモードを使用します。|<xref:System.Windows.Forms.DataGridView.AutoSizeColumnsMode%2A> プロパティを <xref:System.Windows.Forms.DataGridViewAutoSizeColumnsMode.Fill>に設定します。 列のプロパティを設定するか、コントロール <xref:System.Windows.Forms.DataGridViewColumn.FillWeight%2A> <xref:System.Windows.Forms.DataGridView.AutoResizeColumns%2A> にデータを格納した後でコントロールメソッドを呼び出すことによって、列の相対幅を初期化します。|  
|列フィルモードは、さまざまな重要度の値と共に使用してください。|<xref:System.Windows.Forms.DataGridView.AutoSizeColumnsMode%2A> プロパティを <xref:System.Windows.Forms.DataGridViewAutoSizeColumnsMode.Fill>に設定します。 <xref:System.Windows.Forms.DataGridViewColumn.MinimumWidth%2A>データの一部を常に表示するか、特定の列に対して fill モード以外のサイズ変更オプションを使用する必要がある列に大きな値を設定します。|  
|コントロールの背景が表示されないようにするには、列フィルモードを使用します。|最後の <xref:System.Windows.Forms.DataGridViewColumn.AutoSizeMode%2A> 列のプロパティをに設定 <xref:System.Windows.Forms.DataGridViewAutoSizeColumnMode.Fill> し、他の列に対して他のサイズ変更オプションを使用します。 他の列で使用可能な領域が多すぎる場合は、 <xref:System.Windows.Forms.DataGridViewColumn.MinimumWidth%2A> 最後の列のプロパティを設定します。|  
|固定幅の列 (アイコンや ID 列など) を表示します。|列のをに設定 <xref:System.Windows.Forms.DataGridViewColumn.AutoSizeMode%2A> <xref:System.Windows.Forms.DataGridViewAutoSizeColumnMode.None> し、をに設定し <xref:System.Windows.Forms.DataGridViewColumn.Resizable%2A> <xref:System.Windows.Forms.DataGridViewTriState.False> ます。 プロパティを設定するか、コントロール <xref:System.Windows.Forms.DataGridViewColumn.Width%2A> <xref:System.Windows.Forms.DataGridView.AutoResizeColumn%2A> にデータを入力した後でコントロールメソッドを呼び出すことによって、幅を初期化します。|  
|クリッピングを回避し、領域の使用を最適化するためにセルの内容が変更されるたびに、サイズを自動的に調整します。|自動サイズ変更プロパティを、コンテンツベースのサイズ変更モードを表す値に設定します。 大量のデータを処理するときにパフォーマンスが低下しないようにするには、表示されている行のみを計算するサイズ変更モードを使用します。|  
|多数の行を処理するときにパフォーマンスが低下しないように、表示される行の値に合わせてサイズを調整します。|自動またはプログラムによるサイズ変更で、適切なサイズ変更モードの列挙値を使用します。 スクロール中に新しく表示された行の値に合わせてサイズを調整するには、イベントハンドラーでサイズ変更メソッドを呼び出し <xref:System.Windows.Forms.DataGridView.Scroll> ます。 ユーザーがダブルクリックしたサイズ変更をカスタマイズして、表示される行の値だけが新しいサイズを決定できるようにするに <xref:System.Windows.Forms.DataGridView.RowDividerDoubleClick> は、イベントハンドラーまたはイベントハンドラーでサイズ変更メソッドを呼び出し <xref:System.Windows.Forms.DataGridView.ColumnDividerDoubleClick> ます。|  
|パフォーマンスの低下を避けるため、またはユーザーのサイズ変更を可能にするために、特定の時点でのみセルの内容に合わせてサイズを調整します。|イベントハンドラーでコンテンツベースのサイズ変更メソッドを呼び出します。 たとえば、イベントを使用して、 <xref:System.Windows.Forms.DataGridView.DataBindingComplete> バインド後のサイズを初期化し、イベントまたはイベントを処理して、 <xref:System.Windows.Forms.DataGridView.CellValidated> バインドされた <xref:System.Windows.Forms.DataGridView.CellValueChanged> データソースのユーザーの編集や変更に合わせてサイズを調整します。|  
|複数行のセルの内容の行の高さを調整します。|列の幅がテキストの段落を表示するのに適していることを確認し、自動またはプログラムによるコンテンツベースの行のサイズ設定を使用して高さを調整します。 また、セルスタイルの値を使用して、複数行のコンテンツを含むセルが表示されることを確認し <xref:System.Windows.Forms.DataGridViewCellStyle.WrapMode%2A> <xref:System.Windows.Forms.DataGridViewTriState.True> ます。<br /><br /> 通常、列の幅を維持するには自動列サイズ変更モードを使用し、行の高さを調整する前に特定の幅に設定します。|  
  
## <a name="resizing-with-the-mouse"></a>マウスによるサイズ変更  
 既定では、ユーザーは、セル値に基づいて自動サイズ変更モードを使用しない行、列、およびヘッダーのサイズを変更できます。 列の塗りつぶしモードなど、他のモードでユーザーのサイズを変更できないようにするには、次のプロパティの1つまたは複数を設定し <xref:System.Windows.Forms.DataGridView> ます。  
  
- <xref:System.Windows.Forms.DataGridView.AllowUserToResizeColumns%2A>  
  
- <xref:System.Windows.Forms.DataGridView.AllowUserToResizeRows%2A>  
  
- <xref:System.Windows.Forms.DataGridView.ColumnHeadersHeightSizeMode%2A>  
  
- <xref:System.Windows.Forms.DataGridView.RowHeadersWidthSizeMode%2A>  
  
 また、ユーザーが個々の行や列のサイズを変更できないようにするには、プロパティを設定し <xref:System.Windows.Forms.DataGridViewBand.Resizable%2A> ます。 既定では、 <xref:System.Windows.Forms.DataGridViewBand.Resizable%2A> プロパティ値は、 <xref:System.Windows.Forms.DataGridView.AllowUserToResizeColumns%2A> 列のプロパティ値と行のプロパティ値に基づいてい <xref:System.Windows.Forms.DataGridView.AllowUserToResizeRows%2A> ます。 ただし、を明示的にまたはに設定した場合、 <xref:System.Windows.Forms.DataGridViewBand.Resizable%2A> 指定された値は <xref:System.Windows.Forms.DataGridViewTriState.True> <xref:System.Windows.Forms.DataGridViewTriState.False> その行または列のコントロール値よりも優先されます。 <xref:System.Windows.Forms.DataGridViewBand.Resizable%2A>継承を復元するには、に設定し <xref:System.Windows.Forms.DataGridViewTriState.NotSet> ます。  
  
 <xref:System.Windows.Forms.DataGridViewTriState.NotSet>は値の継承を復元するため、 <xref:System.Windows.Forms.DataGridViewBand.Resizable%2A> <xref:System.Windows.Forms.DataGridViewTriState.NotSet> 行または列がコントロールに追加されていない場合、プロパティは値を返しません <xref:System.Windows.Forms.DataGridView> 。 <xref:System.Windows.Forms.DataGridViewBand.Resizable%2A>行または列のプロパティ値が継承されているかどうかを判断する必要がある場合は、そのプロパティを調べ <xref:System.Windows.Forms.DataGridViewElement.State%2A> ます。 値に <xref:System.Windows.Forms.DataGridViewElement.State%2A> フラグが含まれている場合 <xref:System.Windows.Forms.DataGridViewElementStates.ResizableSet> 、 <xref:System.Windows.Forms.DataGridViewBand.Resizable%2A> プロパティ値は継承されません。  
  
## <a name="automatic-sizing"></a>自動サイズ調整  
 コントロールには、 <xref:System.Windows.Forms.DataGridView> 列の塗りつぶしモードとコンテンツベースの自動サイズ調整という2種類の自動サイズ変更があります。  
  
 [列フィルモード] を指定すると、コントロールの表示列がコントロールの表示領域の幅に合わせて表示されます。 このモードの詳細については、「 [Windows フォーム DataGridView コントロールでの列の塗りつぶしモード](column-fill-mode-in-the-windows-forms-datagridview-control.md)」を参照してください。  
  
 また、行、列、ヘッダーを構成して、セルの内容に合わせてサイズを自動的に調整することもできます。 この場合、セルの内容が変更されるたびにサイズの調整が発生します。  
  
> [!NOTE]
> 仮想モードを使用してカスタムデータキャッシュのセル値を維持すると、ユーザーがセル値を編集したときに自動サイズ変更が発生しますが、イベントハンドラーの外部でキャッシュされた値を変更しても、自動サイズ調整は行われません <xref:System.Windows.Forms.DataGridView.CellValuePushed> 。 この場合は、メソッドを呼び出して、 <xref:System.Windows.Forms.DataGridView.UpdateCellValue%2A> コントロールにセルの表示を強制的に更新し、現在の自動サイズ変更モードを適用します。  
  
 コンテンツベースの自動サイズ変更が1つのディメンションに対してのみ有効になっている場合 (つまり、行ではなく、列でも、列でも有効になっていない場合) は、 <xref:System.Windows.Forms.DataGridViewCellStyle.WrapMode%2A> 他のディメンションが変更されるたびにサイズの調整も行われます。 たとえば、列ではなく行を自動サイズ変更するように構成されていて、有効になっている場合、ユーザーは列 <xref:System.Windows.Forms.DataGridViewCellStyle.WrapMode%2A> の区切り線をドラッグして列の幅を変更することができ、行の高さはセルの内容が完全に表示されるように自動的に調整されます。  
  
 コンテンツベースの自動サイズ変更用に行と列の両方を構成し、有効にした場合 <xref:System.Windows.Forms.DataGridViewCellStyle.WrapMode%2A> 、 <xref:System.Windows.Forms.DataGridView> コントロールはセルの内容が変更されるたびにサイズを調整し、新しいサイズを計算するときに最適なセルの高さと幅の比率を使用します。  
  
 ヘッダーと行のサイズ変更モードと、コントロールの値をオーバーライドしない列のサイズ変更モードを構成するには、次のプロパティの1つまたは複数を設定し <xref:System.Windows.Forms.DataGridView> ます。  
  
- <xref:System.Windows.Forms.DataGridView.ColumnHeadersHeightSizeMode%2A>  
  
- <xref:System.Windows.Forms.DataGridView.RowHeadersWidthSizeMode%2A>  
  
- <xref:System.Windows.Forms.DataGridView.AutoSizeColumnsMode%2A>  
  
- <xref:System.Windows.Forms.DataGridView.AutoSizeRowsMode%2A>  
  
 個々の列のコントロールの列のサイズ変更モードをオーバーライドするには、その <xref:System.Windows.Forms.DataGridViewColumn.AutoSizeMode%2A> プロパティを以外の値に設定し <xref:System.Windows.Forms.DataGridViewAutoSizeColumnMode.NotSet> ます。 列のサイズ変更モードは、実際にはプロパティによって決定され <xref:System.Windows.Forms.DataGridViewColumn.InheritedAutoSizeMode%2A> ます。 このプロパティの値は、その値がである場合を除いて、列のプロパティ値に基づいてい <xref:System.Windows.Forms.DataGridViewColumn.AutoSizeMode%2A> <xref:System.Windows.Forms.DataGridViewAutoSizeColumnMode.NotSet> ます。この場合、コントロールの <xref:System.Windows.Forms.DataGridView.AutoSizeColumnsMode%2A> 値は継承されます。  
  
 大量のデータを扱うときは、コンテンツベースの自動サイズ変更を慎重に使用してください。 パフォーマンスの低下を回避するには、コントロールのすべての行を分析するのではなく、表示された行のみに基づいてサイズを計算する自動サイズ調整モードを使用します。 パフォーマンスを最大にするには、代わりにプログラムによるサイズ変更を使用します。これにより、新しいデータが読み込まれた直後など、特定の時間にサイズを変更できます。  
  
 コンテンツベースの自動サイズ変更モードでは、行、列、またはプロパティをに設定することによって、非表示になっている行、列、またはヘッダーには影響しません <xref:System.Windows.Forms.DataGridViewBand.Visible%2A> <xref:System.Windows.Forms.DataGridView.RowHeadersVisible%2A> <xref:System.Windows.Forms.DataGridView.ColumnHeadersVisible%2A> `false` 。 たとえば、大きなセル値に合わせて自動的にサイズが変更された後に列が非表示になっている場合、大きなセル値を含む行が削除されると、非表示の列のサイズは変更されません。 自動サイズ変更は、可視性が変更されたときには発生しません。そのため、列プロパティをに変更すると、 <xref:System.Windows.Forms.DataGridViewColumn.Visible%2A> `true` 現在のコンテンツに基づいて列のサイズが再計算されません。  
  
 プログラムによるコンテンツベースのサイズ変更は、表示に関係なく、行、列、およびヘッダーに影響します。  
  
## <a name="programmatic-resizing"></a>プログラムによるサイズ変更  
 自動サイズ変更が無効になっている場合は、次のプロパティを使用して、行、列、またはヘッダーの正確な幅または高さをプログラムで設定できます。  
  
- <xref:System.Windows.Forms.DataGridView.RowHeadersWidth%2A?displayProperty=nameWithType>  
  
- <xref:System.Windows.Forms.DataGridView.ColumnHeadersHeight%2A?displayProperty=nameWithType>  
  
- <xref:System.Windows.Forms.DataGridViewRow.Height%2A?displayProperty=nameWithType>  
  
- <xref:System.Windows.Forms.DataGridViewColumn.Width%2A?displayProperty=nameWithType>  
  
 次の方法を使用して、行、列、ヘッダーのサイズをプログラムによって内容に合わせて変更することもできます。  
  
- <xref:System.Windows.Forms.DataGridView.AutoResizeColumn%2A>  
  
- <xref:System.Windows.Forms.DataGridView.AutoResizeColumns%2A>  
  
- <xref:System.Windows.Forms.DataGridView.AutoResizeColumnHeadersHeight%2A>  
  
- <xref:System.Windows.Forms.DataGridView.AutoResizeRow%2A>  
  
- <xref:System.Windows.Forms.DataGridView.AutoResizeRows%2A>  
  
- <xref:System.Windows.Forms.DataGridView.AutoResizeRowHeadersWidth%2A>  
  
 これらのメソッドでは、行、列、またはヘッダーのサイズを、連続したサイズ変更用に構成するのではなく、1回だけ変更します。 新しいサイズは、すべてのセルの内容をクリッピングせずに表示するために自動的に計算されます。 ただし、プロパティ値がである列のサイズをプログラムで変更する場合、列のプロパティ値を比例して調整するために、計算された <xref:System.Windows.Forms.DataGridViewColumn.InheritedAutoSizeMode%2A> <xref:System.Windows.Forms.DataGridViewAutoSizeColumnMode.Fill> コンテンツベースの幅が使用され <xref:System.Windows.Forms.DataGridViewColumn.FillWeight%2A> ます。実際の列の幅は、これらの新しい比率に従って計算され、コントロールの使用可能な表示領域がすべての列に表示されます。  
  
 プログラムによるサイズ変更は、継続的なサイズ変更によるパフォーマンスの低下を回避するために役立ちます。 また、ユーザーがサイズ変更可能な行、列、ヘッダー、および列の塗りつぶしモードの初期サイズを指定する場合にも役立ちます。  
  
 通常は、特定のタイミングでプログラムによるサイズ変更メソッドを呼び出します。 たとえば、データを読み込んだ直後にすべての列のサイズをプログラムで変更することも、特定のセルの値が変更された後に特定の行のサイズをプログラムで変更することもできます。  
  
## <a name="customizing-content-based-sizing-behavior"></a>コンテンツベースのサイズ変更動作のカスタマイズ  
 派生した <xref:System.Windows.Forms.DataGridView> セル、行、および列の型を操作するときに、、、またはの各メソッドをオーバーライドする <xref:System.Windows.Forms.DataGridViewCell.GetPreferredSize%2A?displayProperty=nameWithType> か、派生し <xref:System.Windows.Forms.DataGridViewRow.GetPreferredHeight%2A?displayProperty=nameWithType> <xref:System.Windows.Forms.DataGridViewColumn.GetPreferredWidth%2A?displayProperty=nameWithType> たコントロールで保護されたサイズ変更メソッドのオーバーロードを呼び出すことによって、サイズ変更動作をカスタマイズでき <xref:System.Windows.Forms.DataGridView> ます。 保護されたサイズ変更メソッドのオーバーロードは、ペアで動作するように設計されています。これにより、セルの高さが非常に広くなるのを防ぐことができます。 たとえば、 `AutoResizeRows(DataGridViewAutoSizeRowsMode,Boolean)` メソッドのオーバーロードを呼び出し、 <xref:System.Windows.Forms.DataGridView.AutoResizeRows%2A> パラメーターにの値を渡すと、その `false` オーバーロードによって行の <xref:System.Boolean> セルの理想的な高さと幅が計算されますが、行の高さのみが調整されます。 次に、メソッドを呼び出して、 <xref:System.Windows.Forms.DataGridView.AutoResizeColumns%2A> 列の幅を最適な計算結果に調整する必要があります。  
  
## <a name="content-based-sizing-options"></a>コンテンツベースのサイズ変更オプション  
 サイズ変更プロパティとメソッドによって使用される列挙体の値は、コンテンツベースのサイズ変更に似ています。 これらの値を使用すると、どのセルを使用して適切なサイズを計算するかを制限できます。 すべてのサイズ指定の列挙体では、表示されているセルを参照する名前を持つ値は、表示される行のセルに対する計算を制限します。 行を除外すると、大量の行を処理するときにパフォーマンスが低下しないようにするのに役立ちます。 また、ヘッダーまたは nonheader セルのセル値に対して計算を制限することもできます。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Forms.DataGridView>
- <xref:System.Windows.Forms.DataGridView.AllowUserToResizeColumns%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridView.AllowUserToResizeRows%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridView.ColumnHeadersHeightSizeMode%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridView.RowHeadersWidthSizeMode%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridViewBand.Resizable%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridView.AutoSizeColumnsMode%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridView.AutoSizeRowsMode%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridViewColumn.AutoSizeMode%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridViewColumn.InheritedAutoSizeMode%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridView.RowHeadersWidth%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridView.ColumnHeadersHeight%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridViewRow.Height%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridViewColumn.Width%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridView.AutoResizeColumn%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridView.AutoResizeColumns%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridView.AutoResizeColumnHeadersHeight%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridView.AutoResizeRow%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridView.AutoResizeRows%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridView.AutoResizeRowHeadersWidth%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridViewAutoSizeRowMode>
- <xref:System.Windows.Forms.DataGridViewAutoSizeRowsMode>
- <xref:System.Windows.Forms.DataGridViewAutoSizeColumnMode>
- <xref:System.Windows.Forms.DataGridViewAutoSizeColumnsMode>
- <xref:System.Windows.Forms.DataGridViewColumnHeadersHeightSizeMode>
- <xref:System.Windows.Forms.DataGridViewRowHeadersWidthSizeMode>
- [Windows フォーム DataGridView コントロール内の列と行のサイズ変更](resizing-columns-and-rows-in-the-windows-forms-datagridview-control.md)
- [Windows フォーム DataGridView コントロールの列フィル モード](column-fill-mode-in-the-windows-forms-datagridview-control.md)
- [方法: Windows フォーム DataGridView コントロールのサイズ変更モードを設定する](how-to-set-the-sizing-modes-of-the-windows-forms-datagridview-control.md)
