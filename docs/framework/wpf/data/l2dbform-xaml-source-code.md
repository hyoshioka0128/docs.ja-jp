---
title: L2DBForm.xaml ソース コード
ms.date: 10/22/2019
ms.topic: sample
ms.openlocfilehash: 290b00e136f0c49e1b27d4fa1bca7321eebe936e
ms.sourcegitcommit: 82f94a44ad5c64a399df2a03fa842db308185a76
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72921228"
---
# <a name="l2dbformxaml-source-code"></a>L2DBForm.xaml ソース コード

このページでは、「[LINQ to XML を使用した WPF のデータ バインディングの例](linq-to-xml-data-binding-sample.md)」の XAML ソース ファイルの内容と説明を示します。

## <a name="overall-ui-structure"></a>UI の全体的な構造

WPF プロジェクトでよくあるように、このファイルには親要素として <xref:System.Windows.Window> XML 要素が含まれており、この要素に `L2XDBFrom` 名前空間の派生クラス `LinqToXmlDataBinding` が関連付けられています。

クライアント領域は、背景が薄い青になっている <xref:System.Windows.Controls.StackPanel> に含まれています。 このパネルは、 <xref:System.Windows.Controls.DockPanel> バーで区切られた 4 つの <xref:System.Windows.Controls.Separator> UI セクションで構成されています。 これらのセクションの目的については、[こちら](linq-to-xml-data-binding-sample.md#overview)で説明されています。

各セクションには、それぞれを識別するラベルが含まれています。 最初の 2 つのセクションでは、 <xref:System.Windows.FrameworkElement.LayoutTransform%2A>を使用してこのラベルを 90°回転させています。 セクションの残りの部分には、そのセクションの目的に適したテキスト ブロック、テキスト ボックス、ボタンなどの UI 要素が含まれています。 これらの子コントロールの配置には、子 <xref:System.Windows.Controls.StackPanel> が使用されている場合があります。

## <a name="window-resource-section"></a>ウィンドウ リソース セクション

9 行目の `<Window.Resources>` 開始タグは、ウィンドウ リソース セクションの開始を示します。 このセクションは、35 行目の終了タグで終了します。

11 ～ 25 行目にわたる `<ObjectDataProvider>` タグでは、 <xref:System.Windows.Data.ObjectDataProvider>をソースとして使用する `LoadedBooks`という名前の <xref:System.Xml.Linq.XElement> が宣言されています。 <xref:System.Xml.Linq.XElement> は、組み込み XML ドキュメント (`CDATA` 要素) を解析することで初期化されます。 埋め込み XML ドキュメントの宣言時および解析時に、空白が保持されることに注意してください。 空白が保持されるのは、生の XML の表示に使用されている <xref:System.Windows.Controls.TextBlock> コントロールに、特別な XML 書式設定機能がないためです。

最後に、28 ～ 34 行目で <xref:System.Windows.DataTemplate> という名前の `BookTemplate` が定義されています。 このテンプレートは、 **[Book List]** UI セクションにエントリを表示するために使用されます。 ここでは、データ バインドおよび LINQ to XML の動的プロパティを使用し、次の代入を通じて書籍の ID と名前を取得します。

```xaml
Text="{Binding Path=Attribute[id].Value}"Text="{Binding Path=Value}"
```

## <a name="data-binding-code"></a>データ バインド コード

このファイルでは、 <xref:System.Windows.DataTemplate> 要素に加えて、データ バインドが各所で使用されています。

38 行目の `<StackPanel>` 開始タグでは、このパネルの <xref:System.Windows.FrameworkElement.DataContext%2A> プロパティが `LoadedBooks` データ プロバイダーに設定されています。

```xaml
DataContext="{Binding Source={StaticResource LoadedBooks}}
```

データ コンテキストを設定することにより、このデータ プロバイダーの `Xml` プロパティにバインドして、`tbRawXml` という名前の <xref:System.Windows.Controls.TextBlock> に生の XML を表示できるようになります (46 行目)。

```xaml
Text="{Binding Path=Xml}"
```

58 ～ 62 行目では、 <xref:System.Windows.Controls.ListBox> [Book List] **UI セクションの** が、その表示項目のテンプレートをウィンドウ リソース セクションで定義された `BookTemplate` に設定しています。

```xaml
ItemTemplate ="{StaticResource BookTemplate}"
```

59 ～ 62 行目では、書籍の実際の値がこのリスト ボックスにバインドされています。

```xaml
<ListBox.ItemsSource>
    <Binding Path="Elements[{http://www.mybooks.com}book]"/>
</ListBox.ItemsSource>
```

3 番目の UI セクション **[Edit Selected Book]** では、まず親 <xref:System.Windows.FrameworkElement.DataContext%2A> の <xref:System.Windows.Controls.StackPanel> が、 **[Book List]** UI セクション (82 行目) で現在選択されている項目にバインドされています。

```xaml
DataContext="{Binding ElementName=lbBooks, Path=SelectedItem}"
```

次に、双方向データ バインドを使用して、書籍要素の現在の値がこのパネルの 2 つのテキスト ボックスに表示され、そこで更新されるようにしています。 動的プロパティへのデータ バインドは、`BookTemplate` データ テンプレートで使用されるデータ バインドと似ています。

```xaml
Text="{Binding Path=Attribute[id].Value}"...Text="{Binding Path=Value}"
```

最後の UI セクション **[Add New Book]** では、XAML コード内でデータ バインドが使用されません。 代わりに、データ バインドは *L2DBForm.xaml.cs* ファイルのイベント処理コード内にあります。

## <a name="example"></a>例

### <a name="description"></a>説明

> [!NOTE]
> 行番号を追跡しやすいように、次のコードを Visual Studio の C# ソース コード エディターなどのコード エディターにコピーすることをお勧めします。

### <a name="code"></a>コード

```xml
<Window x:Class="LinqToXmlDataBinding.L2XDBForm"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:system="clr-namespace:System;assembly=mscorlib"
    xmlns:xlinq="clr-namespace:System.Xml.Linq;assembly=System.Xml.Linq"
    xmlns:local="clr-namespace:LinqToXmlDataBinding"
    Title="WPF Data Binding using LINQ-to-XML" Height="665" Width="500" ResizeMode="NoResize">

    <Window.Resources>
        <!-- Books provider and inline data -->
        <ObjectDataProvider x:Key="LoadedBooks" ObjectType="{x:Type xlinq:XElement}" MethodName="Parse">
            <ObjectDataProvider.MethodParameters>
                <system:String xml:space="preserve">
<![CDATA[
<books xmlns="http://www.mybooks.com">
  <book id="0">book zero</book>
  <book id="1">book one</book>
  <book id="2">book two</book>
  <book id="3">book three</book>
</books>
]]>
                </system:String>
                <xlinq:LoadOptions>PreserveWhitespace</xlinq:LoadOptions>
            </ObjectDataProvider.MethodParameters>
        </ObjectDataProvider>

        <!-- Template for use in Books List listbox. -->
        <DataTemplate x:Key="BookTemplate">
            <StackPanel Orientation="Horizontal">
                <TextBlock Margin="3" Text="{Binding Path=Attribute[id].Value}"/>
                <TextBlock Margin="3" Text="-"/>
                <TextBlock Margin="3" Text="{Binding Path=Value}"/>
            </StackPanel>
        </DataTemplate>
    </Window.Resources>

    <!-- Main visual content container -->
    <StackPanel Background="lightblue" DataContext="{Binding Source={StaticResource LoadedBooks}}">
        <!-- Raw XML display section -->
        <DockPanel Margin="5">
            <Label  Background="Gray" FontSize="12" BorderBrush="Black" BorderThickness="1" FontWeight="Bold">XML
            <Label.LayoutTransform>
                <RotateTransform Angle="90"/>
            </Label.LayoutTransform>
            </Label>
            <TextBlock Name="tbRawXml" Height="200" Background="LightGray" Text="{Binding Path=Xml}" TextTrimming="CharacterEllipsis" />
        </DockPanel>

        <Separator Height="4" Margin="5" />

        <!-- List box to display all books section -->
        <DockPanel Margin="5">
            <Label  Background="Gray" FontSize="12" BorderBrush="Black" BorderThickness="1" FontWeight="Bold">Book List
                <Label.LayoutTransform>
                    <RotateTransform Angle="90"/>
                </Label.LayoutTransform>
            </Label>
            <ListBox Name="lbBooks" Height="200" Width="415" ItemTemplate ="{StaticResource BookTemplate}">
                <ListBox.ItemsSource>
                    <Binding Path="Elements[{http://www.mybooks.com}book]"/>
                </ListBox.ItemsSource>
            </ListBox>
            <Button Margin="5" DockPanel.Dock="Right" Height="30" Width ="130" Content="Remove Selected Book" Click="OnRemoveBook">
            <Button.LayoutTransform>
                <RotateTransform Angle="90"/>
            </Button.LayoutTransform>
            </Button>
        </DockPanel>

        <Separator Height="4" Margin="5" />

        <!-- Edit current selection section -->
        <DockPanel Margin="5">
            <TextBlock Margin="5" Height="30" Width="65" DockPanel.Dock="Right" Background="LightGray" TextWrapping="Wrap" TextAlignment="Center">
                    Changes are live!
                <TextBlock.LayoutTransform>
                    <RotateTransform Angle="90"/>
                </TextBlock.LayoutTransform>
            </TextBlock>
            <StackPanel>
                <Label Width="450" Background="Gray" FontSize="12" BorderBrush="Black" BorderThickness="1" HorizontalAlignment="Left" FontWeight="Bold">Edit Selected Book</Label>
                <StackPanel Margin="1" DataContext="{Binding ElementName=lbBooks, Path=SelectedItem}">
                    <StackPanel Orientation="Horizontal">
                        <Label Width="40">ID:</Label>
                        <TextBox Name="editAttributeTextBox" Width="410" Text="{Binding Path=Attribute[id].Value}">
                            <TextBox.ToolTip>
                                <TextBlock FontWeight="Bold" TextAlignment="Center">
                                    <Label>Edit the selected book ID and see it changed.</Label>
                                </TextBlock>
                            </TextBox.ToolTip>
                        </TextBox>
                    </StackPanel>
                    <StackPanel Orientation="Horizontal">
                        <Label Width="40">Value:</Label>
                        <TextBox Name="editValueTextBox" Width="410" Text="{Binding Path=Value}" Height="25">
                            <TextBox.ToolTip>
                                <TextBlock FontWeight="Bold" TextAlignment="Center">
                                    <Label>Edit the selected book Value and see it changed.</Label>
                                </TextBlock>
                            </TextBox.ToolTip>
                        </TextBox>
                    </StackPanel>
                </StackPanel>
            </StackPanel>
        </DockPanel>

        <Separator Height="4" Margin="5" />

        <!-- Add new book section -->
        <DockPanel Margin="5">
            <Button Margin="5" Height="30" DockPanel.Dock="Right" Click ="OnAddBook">Add Book
                <Button.LayoutTransform>
                    <RotateTransform Angle="90"/>
                </Button.LayoutTransform>
            </Button>
            <StackPanel>
                <Label Width="450" Background="Gray" FontSize="12" BorderBrush="Black" BorderThickness="1" HorizontalAlignment="Left" FontWeight="Bold">Add New Book</Label>
                <StackPanel Margin="1">
                    <StackPanel Orientation="Horizontal">
                        <Label Width="40">ID:</Label>
                        <TextBox Name="tbAddID" Width="410">
                            <TextBox.ToolTip>
                                <TextBlock FontWeight="Bold" TextAlignment="Center">
                                    <Label>Enter a book ID and Value pair, then click Add Book.</Label>
                                </TextBlock>
                            </TextBox.ToolTip>
                        </TextBox>
                    </StackPanel>
                    <StackPanel Orientation="Horizontal">
                        <Label Width="40">Value:</Label>
                        <TextBox Name="tbAddValue" Width="410" Height="25">
                            <TextBox.ToolTip>
                                <TextBlock FontWeight="UltraBold" TextAlignment="Center">
                                    <Label>Enter a book ID and Value pair, then click Add Book.</Label>
                                </TextBlock>
                            </TextBox.ToolTip>
                        </TextBox>
                    </StackPanel>
                </StackPanel>
            </StackPanel>
        </DockPanel>
    </StackPanel>
</Window>
```

### <a name="comments"></a>コメント

WPF UI 要素に関連付けられているイベント ハンドラーの C# ソース コードについては、「[L2DBForm.xaml.cs Source Code](l2dbform-xaml-cs-source-code.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [チュートリアル: LinqToXmlDataBinding の例](linq-to-xml-data-binding-sample.md)
- [L2DBForm.xaml.cs sauce コード](l2dbform-xaml-cs-source-code.md)
