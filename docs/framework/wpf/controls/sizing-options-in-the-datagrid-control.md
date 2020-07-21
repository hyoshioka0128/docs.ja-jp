---
title: DataGrid コントロールのサイズ変更方法
ms.date: 03/30/2017
helpviewer_keywords:
- DataGrid control [WPF], sizing
- size [WPF], DataGrid
- automatically size DataGrid [WPF]
ms.assetid: 96a0e47e-b010-4302-98ef-2daac446d8db
ms.openlocfilehash: 6d100fb17b1ee3e652985a637d333d9f65e20d36
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61970990"
---
# <a name="sizing-options-in-the-datagrid-control"></a>DataGrid コントロールのサイズ変更方法
<xref:System.Windows.Controls.DataGrid> 自体でサイズをどのように変更するかを制御するために、さまざまなオプションを使用できます。 <xref:System.Windows.Controls.DataGrid>、および <xref:System.Windows.Controls.DataGrid> 内の個々の行と列は、その内容に合わせて自動的にサイズ変更するように設定することも、特定の値に設定することもできます。 既定では、<xref:System.Windows.Controls.DataGrid> はその内容のサイズに合わせて拡大縮小します。  
  
## <a name="sizing-the-datagrid"></a>DataGrid のサイズ変更  
  
### <a name="cautions-when-using-automatic-sizing"></a>自動サイズ変更を使用する場合の注意事項  
 既定では、<xref:System.Windows.Controls.DataGrid> の <xref:System.Windows.FrameworkElement.Height%2A> および <xref:System.Windows.FrameworkElement.Width%2A> プロパティは <xref:System.Double.NaN?displayProperty=nameWithType> (XAML では "`Auto`") に設定され、<xref:System.Windows.Controls.DataGrid> でその内容のサイズに合わせて調整されます。  
  
 <xref:System.Windows.Controls.Canvas> や <xref:System.Windows.Controls.StackPanel> など、その子のサイズが制限されないコンテナー内に配置された場合、<xref:System.Windows.Controls.DataGrid> はコンテナーの可視境界を超えて広がり、スクロールバーは表示されません。 この状況は、使いやすさとパフォーマンスの両方に影響します。  
  
 データ セットにバインドされているときに、<xref:System.Windows.Controls.DataGrid> の <xref:System.Windows.FrameworkElement.Height%2A> が制限されていない場合、バインドされたデータ セット内の各データ項目に対する行の追加が続行されます。 これにより、行が追加されるにつれて、アプリケーションの可視境界外に <xref:System.Windows.Controls.DataGrid> が拡大する可能性があります。 この場合、<xref:System.Windows.Controls.DataGrid> にはスクロールバーが表示されません。これは、その <xref:System.Windows.FrameworkElement.Height%2A> が新しい行に合わせて拡大し続けるためです。  
  
 <xref:System.Windows.Controls.DataGrid> 内の行ごとにオブジェクトが作成されます。 大規模なデータ セットを操作し、<xref:System.Windows.Controls.DataGrid> 自体で自動的にサイズ変更できるようにする場合に、多数のオブジェクトを作成すると、アプリケーションのパフォーマンスに影響する可能性があります。  
  
 大規模なデータ セットを操作するときにこれらの問題を回避するには、<xref:System.Windows.Controls.DataGrid> の <xref:System.Windows.FrameworkElement.Height%2A> を明示的に設定するか、<xref:System.Windows.Controls.Grid> など、その <xref:System.Windows.FrameworkElement.Height%2A> を制限するコンテナーに配置することをお勧めします。 <xref:System.Windows.FrameworkElement.Height%2A> が制限されている場合、<xref:System.Windows.Controls.DataGrid> では、その指定された <xref:System.Windows.FrameworkElement.Height%2A> 内に収まる行のみを作成し、新しいデータを表示するために必要に応じて、それらの行をリサイクルします。  
  
### <a name="setting-the-datagrid-size"></a>DataGrid サイズの設定  
 <xref:System.Windows.Controls.DataGrid> を指定された境界内で自動的にサイズ変更するように設定することも、<xref:System.Windows.Controls.DataGrid> を特定のサイズに設定することもできます。 次の表には、<xref:System.Windows.Controls.DataGrid> サイズを制御するために設定できるプロパティが示されています。  
  
|プロパティ|説明|  
|--------------|-----------------|  
|<xref:System.Windows.FrameworkElement.Height%2A>|<xref:System.Windows.Controls.DataGrid> の特定の高さを設定します。|  
|<xref:System.Windows.FrameworkElement.MaxHeight%2A>|<xref:System.Windows.Controls.DataGrid> の高さの上限を設定します。 <xref:System.Windows.Controls.DataGrid> は、この高さに達するまで垂直方向に拡大します。|  
|<xref:System.Windows.FrameworkElement.MinHeight%2A>|<xref:System.Windows.Controls.DataGrid> の高さの下限を設定します。 <xref:System.Windows.Controls.DataGrid> は、この高さに達するまで垂直方向に縮小します。|  
|<xref:System.Windows.FrameworkElement.Width%2A>|<xref:System.Windows.Controls.DataGrid> の特定の幅を設定します。|  
|<xref:System.Windows.FrameworkElement.MaxWidth%2A>|<xref:System.Windows.Controls.DataGrid> の幅の上限を設定します。 <xref:System.Windows.Controls.DataGrid> は、この幅に達するまで水平方向に拡大します。|  
|<xref:System.Windows.FrameworkElement.MinWidth%2A>|<xref:System.Windows.Controls.DataGrid> の幅の下限を設定します。 <xref:System.Windows.Controls.DataGrid> は、この幅に達するまで水平方向に縮小します。|  
  
## <a name="sizing-rows-and-row-headers"></a>行と行ヘッダーのサイズ変更  
  
### <a name="datagrid-rows"></a>DataGrid 行  
 既定では、<xref:System.Windows.Controls.DataGrid> 行の <xref:System.Windows.FrameworkElement.Height%2A> プロパティが <xref:System.Double.NaN?displayProperty=nameWithType> (XAML では "`Auto`") に設定され、行の高さはその内容のサイズに合わせて拡張されます。 <xref:System.Windows.Controls.DataGrid> 内のすべての行の高さは、<xref:System.Windows.Controls.DataGrid.RowHeight%2A?displayProperty=nameWithType> プロパティを設定することで指定できます。 ユーザーは行ヘッダーの区切り線をドラッグすることで、行の高さを変更できます。  
  
### <a name="datagrid-row-headers"></a>DataGrid 行ヘッダー  
 行ヘッダーを表示するには、<xref:System.Windows.Controls.DataGrid.HeadersVisibility%2A> プロパティを <xref:System.Windows.Controls.DataGridHeadersVisibility.Row?displayProperty=nameWithType> または <xref:System.Windows.Controls.DataGridHeadersVisibility.All?displayProperty=nameWithType> に設定する必要があります。 行ヘッダーは既定で表示され、その内容に合わせて自動的にサイズ変更されます。 行ヘッダーには、<xref:System.Windows.Controls.DataGrid.RowHeaderWidth%2A?displayProperty=nameWithType> プロパティを設定することで特定の幅を指定できます。  
  
## <a name="sizing-columns-and-column-headers"></a>列と列ヘッダーのサイズ変更  
  
### <a name="datagrid-columns"></a>DataGrid 列  
 <xref:System.Windows.Controls.DataGrid> では、<xref:System.Windows.Controls.DataGridLength> および <xref:System.Windows.Controls.DataGridLengthUnitType> 構造体の値を使用して、絶対または自動のサイズ変更モードを指定します。  
  
 次の表には、<xref:System.Windows.Controls.DataGridLengthUnitType> 構造体で提供される値が示されています。  
  
|名前|説明|  
|----------|-----------------|  
|<xref:System.Windows.Controls.DataGridLengthUnitType.Auto>|既定の自動サイズ変更モードでは、セルと列ヘッダーの両方の内容に基づいて、<xref:System.Windows.Controls.DataGrid> 列のサイズが変更されます。|  
|<xref:System.Windows.Controls.DataGridLengthUnitType.SizeToCells>|セルベースの自動サイズ変更モードでは、列ヘッダーを含まない列のセルの内容に基づいて、<xref:System.Windows.Controls.DataGrid> 列のサイズが変更されます。|  
|<xref:System.Windows.Controls.DataGridLengthUnitType.SizeToHeader>|ヘッダーベースの自動サイズ変更モードでは、列ヘッダーの内容のみに基づいて、<xref:System.Windows.Controls.DataGrid> 列のサイズが変更されます。|  
|<xref:System.Windows.Controls.DataGridLengthUnitType.Pixel>|ピクセルベースのサイズ変更モードでは、指定された数値に基づいて、<xref:System.Windows.Controls.DataGrid> 列のサイズが変更されます。|  
|<xref:System.Windows.Controls.DataGridLengthUnitType.Star>|スター サイズ指定モードは、使用可能な領域を重み付け比率で分散させるために使用されます。<br /><br /> XAML では、スター値は n* で表されます。ここで、n は数値を表します。 1\* は \* と同じです。 たとえば、<xref:System.Windows.Controls.DataGrid> の 2 つの列の幅が \* と 2\* である場合、最初の列では使用可能な領域の 1 つの部分を受け取り、2 番目の列では使用可能な領域の 2 つの部分を受け取ります。|  
  
 <xref:System.Windows.Controls.DataGridLengthConverter> クラスを使用すると、数値または文字列値と <xref:System.Windows.Controls.DataGridLength> 値の間でデータを変換できます。  
  
 既定では、<xref:System.Windows.Controls.DataGrid.ColumnWidth%2A?displayProperty=nameWithType> プロパティは <xref:System.Windows.Controls.DataGridLength.SizeToHeader%2A> に設定され、<xref:System.Windows.Controls.DataGridColumn.Width%2A?displayProperty=nameWithType> プロパティは <xref:System.Windows.Controls.DataGridLength.Auto%2A> に設定されます。 サイズ変更モードが <xref:System.Windows.Controls.DataGridLength.Auto%2A> または <xref:System.Windows.Controls.DataGridLength.SizeToCells%2A> に設定されている場合、列は表示される最も幅の広い内容の幅に合わせて拡大します。 スクロール時に、現在の列のサイズより大きい内容がスクロールされて表示されると、これらのサイズ変更モードにより列が拡張されます。 内容がスクロールされて表示されなくなると、列は圧縮されません。  
  
 <xref:System.Windows.Controls.DataGrid> 内の列は、指定された境界内でのみ自動的にサイズ変更されるように設定することも、列を特定のサイズに設定することもできます。 次の表に、列のサイズを制御するために設定できるプロパティを示します。  
  
|プロパティ|説明|  
|--------------|-----------------|  
|<xref:System.Windows.Controls.DataGrid.MaxColumnWidth%2A?displayProperty=nameWithType>|<xref:System.Windows.Controls.DataGrid> 内のすべての列の上限を設定します。|  
|<xref:System.Windows.Controls.DataGridColumn.MaxWidth%2A?displayProperty=nameWithType>|個々の列の上限を設定します。 <xref:System.Windows.Controls.DataGrid.MaxColumnWidth%2A?displayProperty=nameWithType> をオーバーライドします。|  
|<xref:System.Windows.Controls.DataGrid.MinColumnWidth%2A?displayProperty=nameWithType>|<xref:System.Windows.Controls.DataGrid> 内のすべての列の下限を設定します。|  
|<xref:System.Windows.Controls.DataGridColumn.MinWidth%2A?displayProperty=nameWithType>|個々の列の下限を設定します。 <xref:System.Windows.Controls.DataGrid.MinColumnWidth%2A?displayProperty=nameWithType> をオーバーライドします。|  
|<xref:System.Windows.Controls.DataGrid.ColumnWidth%2A?displayProperty=nameWithType>|<xref:System.Windows.Controls.DataGrid> 内のすべての列に対して特定の幅を設定します。|  
|<xref:System.Windows.Controls.DataGridColumn.Width%2A?displayProperty=nameWithType>|個々の列に対して特定の幅を設定します。 <xref:System.Windows.Controls.DataGrid.ColumnWidth%2A?displayProperty=nameWithType> をオーバーライドします。|  
  
### <a name="datagrid-column-headers"></a>DataGrid 列ヘッダー  
 既定では、<xref:System.Windows.Controls.DataGrid> 列ヘッダーが表示されます。 列ヘッダーを非表示にするには、<xref:System.Windows.Controls.DataGrid.HeadersVisibility%2A> プロパティを <xref:System.Windows.Controls.DataGridHeadersVisibility.Row?displayProperty=nameWithType> または <xref:System.Windows.Controls.DataGridHeadersVisibility.None?displayProperty=nameWithType> に設定する必要があります。 既定では、列ヘッダーが表示されると、その内容に合わせて自動的にサイズが変更されます。 列ヘッダーには、<xref:System.Windows.Controls.DataGrid.ColumnHeaderHeight%2A?displayProperty=nameWithType> プロパティを設定することで、特定の高さを指定できます。  
  
### <a name="resizing-with-the-mouse"></a>マウスによるサイズ変更  
 ユーザーは、行または列ヘッダー区分線をドラッグして、<xref:System.Windows.Controls.DataGrid> の行と列のサイズを変更できます。 <xref:System.Windows.Controls.DataGrid> では、行または列ヘッダー区分線をダブルクリックすることによる行と列の自動サイズ変更もサポートされます。 特定の列のサイズがユーザーに変更されないようにするには、個々の列に対して <xref:System.Windows.Controls.DataGridColumn.CanUserResize%2A?displayProperty=nameWithType> プロパティを `false` に設定します。 すべての列のサイズがユーザーに変更されないようにするには、<xref:System.Windows.Controls.DataGrid.CanUserResizeColumns%2A?displayProperty=nameWithType> プロパティを `false` に設定します。 すべての行のサイズがユーザーに変更されないようにするには、<xref:System.Windows.Controls.DataGrid.CanUserResizeRows%2A?displayProperty=nameWithType> プロパティを `false` に設定します。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Controls.DataGrid>
- <xref:System.Windows.Controls.DataGridColumn>
- <xref:System.Windows.Controls.DataGridLength>
- <xref:System.Windows.Controls.DataGridLengthConverter>
