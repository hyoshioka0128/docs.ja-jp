---
title: '方法: StackPanel を作成する'
ms.date: 03/30/2017
helpviewer_keywords:
- StackPanel control [WPF], creating
ms.assetid: e7ce65cb-720a-4bb6-95b6-286b74488a58
ms.openlocfilehash: bcf6decff2fbc012b5f8b62794f0d7b2cd9f29fc
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62051002"
---
# <a name="how-to-create-a-stackpanel"></a>方法: StackPanel を作成する
この例では、<xref:System.Windows.Controls.StackPanel> を作成する方法を示します。  
  
## <a name="example"></a>例  
 <xref:System.Windows.Controls.StackPanel> では、指定した方向で要素を積み重ねることができます。 <xref:System.Windows.Controls.StackPanel> で定義されているプロパティを使用することで、コンテンツを上下 (既定) または左右に浮動させることができます。  
  
 次の例では、<xref:System.Windows.Controls.StackPanel> を使用することで、5 つの <xref:System.Windows.Controls.TextBlock> コントロールが縦に積み重ねられます。それぞれ、<xref:System.Windows.Controls.Border> と <xref:System.Windows.Controls.Border.Background%2A> が異なります。 <xref:System.Windows.FrameworkElement.Width%2A> が指定されていない子要素は拡張され、親ウィンドウを満たします。ただし、<xref:System.Windows.FrameworkElement.Width%2A> が指定されている子要素はウィンドウ内の中心に配置されます。  
  
 <xref:System.Windows.Controls.StackPanel> における積み重ねの既定の方向は縦です。 <xref:System.Windows.Controls.StackPanel> でコンテンツ フローを制御するには、<xref:System.Windows.Controls.StackPanel.Orientation%2A> プロパティを使用します。 <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A> プロパティを使用することで横の配置を制御できます。  
  
```xaml  
<Page xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation" WindowTitle="StackPanel Sample">  
  <StackPanel>  
    <Border Background="SkyBlue" BorderBrush="Black" BorderThickness="1">  
      <TextBlock Foreground="Black" FontSize="12">Stacked Item #1</TextBlock>  
    </Border>  
    <Border Width="400" Background="CadetBlue" BorderBrush="Black" BorderThickness="1">  
      <TextBlock Foreground="Black" FontSize="14">Stacked Item #2</TextBlock>  
    </Border>  
    <Border Background="LightGoldenRodYellow" BorderBrush="Black" BorderThickness="1">  
      <TextBlock Foreground="Black" FontSize="16">Stacked Item #3</TextBlock>  
    </Border>  
    <Border Width="200" Background="PaleGreen" BorderBrush="Black" BorderThickness="1">  
      <TextBlock Foreground="Black" FontSize="18">Stacked Item #4</TextBlock>  
    </Border>  
    <Border Background="White" BorderBrush="Black" BorderThickness="1">  
      <TextBlock Foreground="Black" FontSize="20">Stacked Item #5</TextBlock>  
    </Border>  
  </StackPanel>  
</Page>  
```  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Controls.StackPanel>
- [パネルの概要](panels-overview.md)
- [方法トピック](stackpanel-how-to-topics.md)
