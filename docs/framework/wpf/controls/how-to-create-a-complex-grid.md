---
title: 複雑なグリッドを作成する方法
description: グリッド コントロールを使用して、月間カレンダーのようなレイアウトを作成する方法の例。
ms.date: 03/30/2017
helpviewer_keywords:
- calendar [WPF], creating
- monthly calendar [WPF], creating
- Grid control [WPF], creating [WPF], complex grid
ms.assetid: 4ce3040a-a156-4364-9596-98ca1eca5550
ms.openlocfilehash: ab5490d608b21fe8b29a078dc1f0147f038c27a3
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/15/2019
ms.locfileid: "65645670"
---
# <a name="how-to-create-a-complex-grid"></a>複雑なグリッドを作成する方法

この例では、<xref:System.Windows.Controls.Grid> コントロールを使用して、月間カレンダーのようなレイアウトを作成する方法を示します。

## <a name="example"></a>例

次の例では、<xref:System.Windows.Controls.RowDefinition> クラスと <xref:System.Windows.Controls.ColumnDefinition> クラスを使用して、8 つの行と 8 つの列が定義されます。 <xref:System.Windows.Controls.Grid.ColumnSpan%2A?displayProperty=nameWithType> と <xref:System.Windows.Controls.Grid.RowSpan%2A?displayProperty=nameWithType> 添付プロパティが <xref:System.Windows.Shapes.Rectangle> 要素と共に使用され、さまざまな列と行の背景が塗りつぶされます。 この設計は、<xref:System.Windows.Controls.Grid> 内の各セルに複数の要素が存在できるため可能です。これは、<xref:System.Windows.Controls.Grid> と <xref:System.Windows.Documents.Table> の基本的な違いです。

この例では、垂直方向のグラデーションの使用により列と行が <xref:System.Windows.Shapes.Shape.Fill%2A> され、カレンダーの視覚表示と読みやすさが向上します。 スタイル設定された <xref:System.Windows.Controls.TextBlock> 要素により、日付と曜日が表されます。 <xref:System.Windows.Controls.TextBlock> 要素は、アプリケーションのスタイル内で定義されている <xref:System.Windows.FrameworkElement.Margin%2A> プロパティと配置プロパティを使用して、セル内に絶対位置で配置されます。

[!code-xaml[GridComplex#1](~/samples/snippets/csharp/VS_Snippets_Wpf/GridComplex/CS/default.xaml#1)]

次の図は、結果であるコントロール、つまりカスタマイズ可能なカレンダーを示しています。

![結果であるコントロールのスクリーン ショット](././media/how-to-create-a-complex-grid/wpf-manual-calendar.png)

## <a name="see-also"></a>関連項目

- <xref:System.Windows.Controls.Grid?displayProperty=nameWithType>
- <xref:System.Windows.Documents.TableCell?displayProperty=nameWithType>
- [純色およびグラデーションによる塗りつぶしの概要](../graphics-multimedia/painting-with-solid-colors-and-gradients-overview.md)
- [パネルの概要](panels-overview.md)
- [テーブルの概要](../advanced/table-overview.md)
