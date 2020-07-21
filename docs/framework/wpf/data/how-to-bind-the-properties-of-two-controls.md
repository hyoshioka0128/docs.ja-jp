---
title: '方法: 2 つのコントロールのプロパティをバインドする'
ms.date: 03/30/2017
helpviewer_keywords:
- data binding [WPF], binding properties of two controls
- binding properties of two controls [WPF]
- controls [WPF], binding properties of
ms.assetid: 06318fac-6afd-4c7d-a277-6d7ef50f47bc
ms.openlocfilehash: d38c473b8c4d3f71f1e3decd4f66be248665c57b
ms.sourcegitcommit: f348c84443380a1959294cdf12babcb804cfa987
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/12/2019
ms.locfileid: "73974813"
---
# <a name="how-to-bind-the-properties-of-two-controls"></a>方法: 2 つのコントロールのプロパティをバインドする

この例では、<xref:System.Windows.Data.Binding.ElementName%2A> プロパティを使用して、インスタンス化された 1 つのコントロールのプロパティを別のコントロールのプロパティにバインドする方法を示します。

## <a name="example"></a>例

次の例では、<xref:System.Windows.Controls.Canvas> の <xref:System.Windows.Controls.Panel.Background%2A> プロパティを <xref:System.Windows.Controls.ComboBox> の [SelectedItem.Content](xref:System.Windows.Controls.ContentControl.Content%2A) プロパティにバインドする方法を示します。

[!code-xaml[BindDptoDp#1](~/samples/snippets/csharp/VS_Snippets_Wpf/BindDPtoDP/CS/Window1.xaml#1)]

この例をレンダリングすると、次のようになります。

![値 Green が選択され、緑色の四角形が表示されているコンボ ボックスのスクリーンショット。](./media/how-to-bind-the-properties-of-two-controls/data-binding-bind-background-canvas.png)

> [!NOTE]
> バインディング ターゲット プロパティ (この例では <xref:System.Windows.Controls.Panel.Background%2A> プロパティ) は、依存関係プロパティである必要があります。 詳しくは、「[データ バインディングの概要](../../../desktop-wpf/data/data-binding-overview.md)」をご覧ください。

## <a name="see-also"></a>関連項目

- [バインディング ソースを指定する](how-to-specify-the-binding-source.md)
- [方法トピック](data-binding-how-to-topics.md)
