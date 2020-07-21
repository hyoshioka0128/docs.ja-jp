---
title: '方法: TextBox テキストでソースを更新するタイミングを制御する'
description: Windows Presentation Foundation (WPF) で UpdateSourceTrigger プロパティを使用して、バインディング ソースの更新のタイミングを制御します。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- source updates [WPF], timing of
- data binding [WPF], timing of source updates
- timing of source updates [WPF]
ms.assetid: ffb7b96a-351d-4c68-81e7-054033781c64
ms.openlocfilehash: 8f6eb5beb0d14a951f6e6cf6eb81e130f5a3e194
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85622784"
---
# <a name="how-to-control-when-the-textbox-text-updates-the-source"></a>方法: TextBox テキストでソースを更新するタイミングを制御する
このトピックでは、<xref:System.Windows.Data.Binding.UpdateSourceTrigger%2A> プロパティを使用して、バインディング ソースの更新のタイミングを制御する方法について説明します。 このトピックでは、例として <xref:System.Windows.Controls.TextBox> コントロールを使用します。

## <a name="example"></a>例
 <xref:System.Windows.Controls.TextBox.Text%2A?displayProperty=nameWithType> プロパティの <xref:System.Windows.Data.Binding.UpdateSourceTrigger%2A> の既定値は <xref:System.Windows.Data.UpdateSourceTrigger.LostFocus> です。 つまり、アプリケーションにデータ バインドされた <xref:System.Windows.Controls.TextBox.Text%2A?displayProperty=nameWithType> プロパティを持つ <xref:System.Windows.Controls.TextBox> がある場合、<xref:System.Windows.Controls.TextBox> がフォーカスを失うまで (たとえば、<xref:System.Windows.Controls.TextBox> からクリックして移動したとき)、<xref:System.Windows.Controls.TextBox> に入力したテキストでソースは更新されません。

 入力したらソースが更新されるようにしたい場合は、バインディングの <xref:System.Windows.Data.Binding.UpdateSourceTrigger%2A> を <xref:System.Windows.Data.UpdateSourceTrigger.PropertyChanged> に設定します。 次の例の強調表示されているコード行は、<xref:System.Windows.Controls.TextBox> と <xref:System.Windows.Controls.TextBlock> 両方の `Text` プロパティが、同じソース プロパティにバインドされていることを示します。 <xref:System.Windows.Controls.TextBox> バインディングの <xref:System.Windows.Data.Binding.UpdateSourceTrigger%2A> プロパティは、<xref:System.Windows.Data.UpdateSourceTrigger.PropertyChanged> に設定されています。

 [!code-xaml[SimpleBinding#USTHowTo](~/samples/snippets/visualbasic/VS_Snippets_Wpf/SimpleBinding/VisualBasic/Page1.xaml?highlight=33-39,41-42)]

 結果として、次のスクリーンショットの例に示すように、<xref:System.Windows.Controls.TextBlock> には、ユーザーが <xref:System.Windows.Controls.TextBox> に入力したのと同じテキストが表示されます (ソースが変更されるため)。

 ![簡単なデータ バインディングを示すスクリーンショット。](./media/how-to-control-when-the-textbox-text-updates-the-source/data-binding-simple-binding-sample.png)

 ダイアログまたはユーザーが編集できるフォームがあり、ユーザーがフィールドの編集を終えて [OK] をクリックするまでソースの更新を遅延させる場合は、次の例のように、バインディングの <xref:System.Windows.Data.Binding.UpdateSourceTrigger%2A> の値を <xref:System.Windows.Data.UpdateSourceTrigger.Explicit> に設定します。

 [!code-xaml[UpdateSource#2](~/samples/snippets/csharp/VS_Snippets_Wpf/UpdateSource/CSharp/Window1.xaml#2)]

 <xref:System.Windows.Data.Binding.UpdateSourceTrigger%2A> の値を <xref:System.Windows.Data.UpdateSourceTrigger.Explicit> に設定すると、ソースの値は、アプリケーションで <xref:System.Windows.Data.BindingExpression.UpdateSource%2A> メソッドが呼び出された場合にのみ変更されます。 次の例では、`itemNameTextBox` に対して <xref:System.Windows.Data.BindingExpression.UpdateSource%2A> を呼び出す方法を示します。

 [!code-csharp[UpdateSource#1](~/samples/snippets/csharp/VS_Snippets_Wpf/UpdateSource/CSharp/Window1.xaml.cs#1)]
 [!code-vb[UpdateSource#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/UpdateSource/VisualBasic/Window1.xaml.vb#1)]

> [!NOTE]
> 他のコントロールのプロパティにも同じ手法を使用できますが、他のほとんどのプロパティでは <xref:System.Windows.Data.UpdateSourceTrigger.PropertyChanged> の既定値が <xref:System.Windows.Data.Binding.UpdateSourceTrigger%2A> であることに注意してください。 詳細については、<xref:System.Windows.Data.Binding.UpdateSourceTrigger%2A> プロパティのページを参照してください。

> [!NOTE]
> <xref:System.Windows.Data.Binding.UpdateSourceTrigger%2A> プロパティではソースの更新が処理されるため、このプロパティは <xref:System.Windows.Data.BindingMode.TwoWay> または <xref:System.Windows.Data.BindingMode.OneWayToSource> のバインディングにのみ関連します。 <xref:System.Windows.Data.BindingMode.TwoWay> および <xref:System.Windows.Data.BindingMode.OneWayToSource> のバインディングを機能させるには、ソース オブジェクトでプロパティ変更通知を提供する必要があります。 詳しくは、このトピック内にあるサンプルをご覧ください。 また、「[方法 : プロパティの変更通知を実装する](how-to-implement-property-change-notification.md)」もご覧ください。

## <a name="see-also"></a>関連項目

- [方法トピック](data-binding-how-to-topics.md)
