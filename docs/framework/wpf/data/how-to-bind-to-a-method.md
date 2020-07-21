---
title: '方法: メソッドにバインドする'
description: 次の例に従って、Windows Presentation Foundation (WPF) でオブジェクトのメソッドにバインドする方法を確認します。
ms.date: 03/30/2017
helpviewer_keywords:
- data binding [WPF], binding to methods using ObjectDataProvider
- binding [WPF], to methods
- methods [WPF], binding to
ms.assetid: 5f55e71e-2182-42a0-88d1-700cc1427a7a
ms.openlocfilehash: 9501e6357203c21651e85f1d65059be1d70becf2
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85619599"
---
# <a name="how-to-bind-to-a-method"></a>方法: メソッドにバインドする
次の例では、<xref:System.Windows.Data.ObjectDataProvider> を使用してメソッドにバインドする方法を示します。  
  
## <a name="example"></a>例  
 この例では、`TemperatureScale` はメソッド `ConvertTemp` を持つクラスで、2 つのパラメーター (1 つは `double` でもう 1 つは `enum` 型 `TempType)`) を取得して、指定した値をある温度尺度から他の温度尺度へ変換します。 次の例では、<xref:System.Windows.Data.ObjectDataProvider> を使用して `TemperatureScale` オブジェクトをインスタンス化する方法を示します。 `ConvertTemp` メソッドは、2 つの指定したパラメーターで呼び出されます。  
  
 [!code-xaml[BindToMethod#WindowResources](~/samples/snippets/csharp/VS_Snippets_Wpf/BindToMethod/CS/Window1.xaml#windowresources)]  
  
 このメソッドはリソースとして使用可能となり、その結果にバインドできます。 次の例では、<xref:System.Windows.Controls.TextBox> の <xref:System.Windows.Controls.TextBox.Text%2A> プロパティと <xref:System.Windows.Controls.ComboBox> の <xref:System.Windows.Controls.Primitives.Selector.SelectedValue%2A> を、メソッドの 2 つのパラメーターにバインドします。 これにより、ユーザーは、変換する温度と変換前の温度尺度を指定できます。 <xref:System.Windows.Data.ObjectDataProvider> によってラップされたオブジェクト (`TemperatureScale` オブジェクト) のプロパティではなく、<xref:System.Windows.Data.ObjectDataProvider> インスタンスの <xref:System.Windows.Data.ObjectDataProvider.MethodParameters%2A> プロパティにバインドしているため、<xref:System.Windows.Data.Binding.BindsDirectlyToSource%2A> が `true` に設定されていることに注意してください。  
  
 ユーザーが <xref:System.Windows.Controls.TextBox> の内容または <xref:System.Windows.Controls.ComboBox> の選択を変更すると、最後の <xref:System.Windows.Controls.Label> の <xref:System.Windows.Controls.ContentControl.Content%2A> が更新されます。  
  
 [!code-xaml[BindToMethod#UI](~/samples/snippets/csharp/VS_Snippets_Wpf/BindToMethod/CS/Window1.xaml#ui)]  
  
 コンバーター `DoubleToString` は、方向が <xref:System.Windows.Data.IValueConverter.Convert%2A> のとき (バインディング ソースからバインディング ターゲット、これは <xref:System.Windows.Controls.TextBox.Text%2A> プロパティです) は double を受け取って string に変換し、方向が <xref:System.Windows.Data.IValueConverter.ConvertBack%2A> のときは `string` を `double` に変換します。  
  
 `InvalidationCharacterRule` は、無効な文字をチェックする <xref:System.Windows.Controls.ValidationRule> です。 入力値が double 値でない場合は、既定のエラー テンプレート (<xref:System.Windows.Controls.TextBox> を囲む赤い境界線) がユーザーへの通知として表示されます。  
  
## <a name="see-also"></a>関連項目

- [方法トピック](data-binding-how-to-topics.md)
- [方法: 列挙値にバインドする](how-to-bind-to-an-enumeration.md)
