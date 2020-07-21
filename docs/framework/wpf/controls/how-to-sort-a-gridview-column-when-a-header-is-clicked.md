---
title: '方法: ヘッダーがクリックされたときに GridView 列を並べ替える'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- controls [WPF], GridView
- controls [WPF], ListView
- ListView controls [WPF], sorting GridView columns
- GridView controls [WPF], ListView control
ms.assetid: 4865d720-d147-40ed-83a7-af7587f8aad8
ms.openlocfilehash: 3438ab91045a144a7fa1d531e9d7d55ad30e89ea
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62052028"
---
# <a name="how-to-sort-a-gridview-column-when-a-header-is-clicked"></a>方法: ヘッダーがクリックされたときに GridView 列を並べ替える

この例では、<xref:System.Windows.Controls.GridView> 表示モードを実装し、ユーザーが列ヘッダーをクリックしたときにデータ コンテンツを並べ替える <xref:System.Windows.Controls.ListView> コントロールを作成する方法を示します。

## <a name="example"></a>例

次の例では、<xref:System.DateTime> 構造のプロパティである <xref:System.DateTime.Year%2A>、<xref:System.DateTime.Month%2A>、<xref:System.DateTime.Day%2A> にバインドされる 3 つの列で <xref:System.Windows.Controls.GridView> が定義されます。

```xaml
<GridView>
  <GridViewColumn DisplayMemberBinding="{Binding Path=Year}"
                  Header="Year"
                  Width="100"/>
  <GridViewColumn DisplayMemberBinding="{Binding Path=Month}"
                  Header="Month"
                  Width="100"/>
  <GridViewColumn DisplayMemberBinding="{Binding Path=Day}"
                  Header="Day"
                  Width="100"/>
</GridView>
```

次の列では、<xref:System.DateTime> オブジェクトの <xref:System.Collections.ArrayList> として定義されるデータ項目を示します。 <xref:System.Collections.ArrayList> は、<xref:System.Windows.Controls.ListView> コントロールの <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A> として定義されます。

```xaml
<ListView.ItemsSource>
  <s:ArrayList>
    <p:DateTime>1993/1/1 12:22:02</p:DateTime>
    <p:DateTime>1993/1/2 13:2:01</p:DateTime>
    <p:DateTime>1997/1/3 2:1:6</p:DateTime>
    <p:DateTime>1997/1/4 13:6:55</p:DateTime>
    <p:DateTime>1999/2/1 12:22:02</p:DateTime>
    <p:DateTime>1998/2/2 13:2:01</p:DateTime>
    <p:DateTime>2000/2/3 2:1:6</p:DateTime>
    <p:DateTime>2002/2/4 13:6:55</p:DateTime>
    <p:DateTime>2001/3/1 12:22:02</p:DateTime>
    <p:DateTime>2006/3/2 13:2:01</p:DateTime>
    <p:DateTime>2004/3/3 2:1:6</p:DateTime>
    <p:DateTime>2004/3/4 13:6:55</p:DateTime>
  </s:ArrayList>
</ListView.ItemsSource>
```

[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] タグの `s` と `p` の識別子とは、[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] ページのメタデータで定義されている名前空間マッピングを意味しています。 次の例にメタデータの定義を示します。

```xaml
<Window
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    x:Class="ListViewSort.Window1"
    xmlns:s="clr-namespace:System.Collections;assembly=mscorlib"
    xmlns:p="clr-namespace:System;assembly=mscorlib">
```

この例では列の内容に従ってデータを並べ替えるために、列ヘッダーのボタンを押したときに発生する <xref:System.Windows.Controls.Primitives.ButtonBase.Click> イベントを処理するイベント ハンドラーを定義します。 次の例では、<xref:System.Windows.Controls.GridViewColumnHeader> コントロールのイベント ハンドラーを指定する方法を示します。

```xaml
<ListView x:Name='lv' Height="150" HorizontalAlignment="Center"
  VerticalAlignment="Center"
  GridViewColumnHeader.Click="GridViewColumnHeaderClickedHandler"
 >
```

この例では、列ヘッダーのボタンをクリックするたびに並べ替えの方向の昇順と降順が切り替わるようにイベント ハンドラーを定義します。 次の例ではイベント ハンドラーを示します。

```csharp
public partial class Window1 : Window
{
    public Window1()
    {
        InitializeComponent();
    }

    GridViewColumnHeader _lastHeaderClicked = null;
    ListSortDirection _lastDirection = ListSortDirection.Ascending;

    void GridViewColumnHeaderClickedHandler(object sender,
                                            RoutedEventArgs e)
    {
        var headerClicked = e.OriginalSource as GridViewColumnHeader;
        ListSortDirection direction;

        if (headerClicked != null)
        {
            if (headerClicked.Role != GridViewColumnHeaderRole.Padding)
            {
                if (headerClicked != _lastHeaderClicked)
                {
                    direction = ListSortDirection.Ascending;
                }
                else
                {
                    if (_lastDirection == ListSortDirection.Ascending)
                    {
                        direction = ListSortDirection.Descending;
                    }
                    else
                    {
                        direction = ListSortDirection.Ascending;
                    }
                }

                var columnBinding = headerClicked.Column.DisplayMemberBinding as Binding;
                var sortBy = columnBinding?.Path.Path ?? headerClicked.Column.Header as string;

                Sort(sortBy, direction);

                if (direction == ListSortDirection.Ascending)
                {
                    headerClicked.Column.HeaderTemplate =
                      Resources["HeaderTemplateArrowUp"] as DataTemplate;
                }
                else
                {
                    headerClicked.Column.HeaderTemplate =
                      Resources["HeaderTemplateArrowDown"] as DataTemplate;
                }

                // Remove arrow from previously sorted header
                if (_lastHeaderClicked != null && _lastHeaderClicked != headerClicked)
                {
                    _lastHeaderClicked.Column.HeaderTemplate = null;
                }

                _lastHeaderClicked = headerClicked;
                _lastDirection = direction;
            }
        }
    }
}
```

```vb
Partial Public Class Window1
    Inherits Window
    Public Sub New()
        InitializeComponent()
    End Sub

    Private _lastHeaderClicked As GridViewColumnHeader = Nothing
    Private _lastDirection As ListSortDirection = ListSortDirection.Ascending

    Private Sub GridViewColumnHeaderClickedHandler(ByVal sender As Object, ByVal e As RoutedEventArgs)
        Dim headerClicked = TryCast(e.OriginalSource, GridViewColumnHeader)
        Dim direction As ListSortDirection

        If headerClicked IsNot Nothing Then
            If headerClicked.Role <> GridViewColumnHeaderRole.Padding Then
                If headerClicked IsNot _lastHeaderClicked Then
                    direction = ListSortDirection.Ascending
                Else
                    If _lastDirection = ListSortDirection.Ascending Then
                        direction = ListSortDirection.Descending
                    Else
                        direction = ListSortDirection.Ascending
                    End If
                End If

                Dim columnBinding = TryCast(headerClicked.Column.DisplayMemberBinding, Binding)
                Dim sortBy = If(columnBinding?.Path.Path, TryCast(headerClicked.Column.Header, String))

                Sort(sortBy, direction)

                If direction = ListSortDirection.Ascending Then
                    headerClicked.Column.HeaderTemplate = TryCast(Resources("HeaderTemplateArrowUp"), DataTemplate)
                Else
                    headerClicked.Column.HeaderTemplate = TryCast(Resources("HeaderTemplateArrowDown"), DataTemplate)
                End If

                ' Remove arrow from previously sorted header
                If _lastHeaderClicked IsNot Nothing AndAlso _lastHeaderClicked IsNot headerClicked Then
                    _lastHeaderClicked.Column.HeaderTemplate = Nothing
                End If

                _lastHeaderClicked = headerClicked
                _lastDirection = direction
            End If
        End If
    End Sub
End Class
```

次の例では、データを並べ替えるためにイベント ハンドラーにより呼び出される並べ替えアルゴリズムを示します。 並べ替えは、新しい <xref:System.ComponentModel.SortDescription> 構造体を作成することで実行されます。

```csharp
private void Sort(string sortBy, ListSortDirection direction)
{
    ICollectionView dataView =
      CollectionViewSource.GetDefaultView(lv.ItemsSource);

    dataView.SortDescriptions.Clear();
    SortDescription sd = new SortDescription(sortBy, direction);
    dataView.SortDescriptions.Add(sd);
    dataView.Refresh();
}
```

```vb
Private Sub Sort(ByVal sortBy As String, ByVal direction As ListSortDirection)
    Dim dataView As ICollectionView = CollectionViewSource.GetDefaultView(lv.ItemsSource)

    dataView.SortDescriptions.Clear()
    Dim sd As New SortDescription(sortBy, direction)
    dataView.SortDescriptions.Add(sd)
    dataView.Refresh()
End Sub
```

## <a name="see-also"></a>関連項目

- <xref:System.Windows.Controls.ListView>
- <xref:System.Windows.Controls.GridView>
- [ListView の概要](listview-overview.md)
- [GridView の概要](gridview-overview.md)
- [方法トピック](listview-how-to-topics.md)
