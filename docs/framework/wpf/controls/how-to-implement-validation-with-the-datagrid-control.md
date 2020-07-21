---
title: '方法: DataGrid コントロールを使用して検証を実装する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- DataGrid [WPF], validation
- validation [WPF], DataGrid
ms.assetid: ec6078a8-1e42-4648-b414-f4348e81bda1
ms.openlocfilehash: 38b4c9cd7679f0d8da9b18fb5bd6bb729d33ed54
ms.sourcegitcommit: 62285ec11fa8e8424bab00511a90760c60e63c95
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/20/2020
ms.locfileid: "81646100"
---
# <a name="how-to-implement-validation-with-the-datagrid-control"></a>方法: DataGrid コントロールを使用して検証を実装する
<xref:System.Windows.Controls.DataGrid> コントロールを使用すると、セル レベルと行レベルの両方で検証を実行できます。 セル レベルの検証では、ユーザーが値を更新するときに、バインドされたデータ オブジェクトの個々のプロパティが検証されます。 行レベルの検証では、ユーザーが変更を行にコミットするときに、データ オブジェクト全体が検証されます。 また、検証エラーに対してカスタマイズした視覚的フィードバックを提供したり、<xref:System.Windows.Controls.DataGrid> コントロールで提供される既定の視覚的フィードバックを使用したりすることもできます。  
  
 次の手順では、<xref:System.Windows.Controls.DataGrid> のバインディングに検証規則を適用する方法、および視覚的なフィードバックをカスタマイズする方法について説明します。  
  
### <a name="to-validate-individual-cell-values"></a>個々のセルの値を検証するには  
  
- 列で使用されているバインディングに対して 1 つ以上の検証規則を指定します。 これは、[データ バインディングの概要](../../../desktop-wpf/data/data-binding-overview.md)に関する記事で説明されている、単純なコントロールでのデータの検証に似ています。  
  
     次の例では、ビジネス オブジェクトの異なるプロパティにバインドされた 4 つの列が含まれる <xref:System.Windows.Controls.DataGrid> コントロールを示します。 3 つの列では、<xref:System.Windows.Data.Binding.ValidatesOnExceptions%2A> プロパティを `true` に設定することによって、<xref:System.Windows.Controls.ExceptionValidationRule> を指定します。  
  
     [!code-xaml[DataGrid_Validation#BasicXaml](~/samples/snippets/csharp/VS_Snippets_Wpf/datagrid_validation/cs/window1.xaml#basicxaml)]  
  
     ユーザーが無効な値を入力すると (たとえば、[Course ID] 列に対して整数以外の値)、そのセルの周囲に赤い枠線が表示されます。 次の手順で説明するようにして、この既定の検証フィードバックを変更できます。  
  
### <a name="to-customize-cell-validation-feedback"></a>セルの検証のフィードバックをカスタマイズするには  
  
- 列の <xref:System.Windows.Controls.DataGridBoundColumn.EditingElementStyle%2A> プロパティを、列の編集コントロールに適したスタイルに設定します。 編集コントロールは実行時に作成されるため、単純なコントロールの場合のような、<xref:System.Windows.Controls.Validation.ErrorTemplate%2A?displayProperty=nameWithType> 添付プロパティを使用することはできません。  
  
     次の例では、前の例を更新して、検証規則のある 3 つの列によって共有されるエラー スタイルを追加します。 ユーザーが無効な値を入力すると、スタイルによってセルの背景色が変更され、ツールヒントが追加されます。 検証エラーがあるかどうかを確認するためのトリガーの使用に注意してください。 現在はセルに専用のエラー テンプレートがないため、このようにする必要があります。  
  
     [!code-xaml[DataGrid_Validation#CellValidationXaml](~/samples/snippets/csharp/VS_Snippets_Wpf/datagrid_validation/cs/mainwindow.xaml#cellvalidationxaml)]  
  
     列で使用されている <xref:System.Windows.Controls.DataGridColumn.CellStyle%2A> を置き換えることで、より広範なカスタマイズを実装できます。  
  
### <a name="to-validate-multiple-values-in-a-single-row"></a>1 つの行で複数の値を検証するには  
  
1. バインドされたデータ オブジェクトの複数のプロパティを調べる <xref:System.Windows.Controls.ValidationRule> サブクラスを実装します。 <xref:System.Windows.Controls.ValidationRule.Validate%2A> メソッドの実装では、`value` パラメーター値を <xref:System.Windows.Data.BindingGroup> インスタンスにキャストします。 その後は、<xref:System.Windows.Data.BindingGroup.Items%2A> プロパティを使用してデータ オブジェクトにアクセスできます。  
  
     次の例では、`Course` オブジェクトの `StartDate` プロパティ値が `EndDate` プロパティ値より前かどうかを検証するための、このプロセスを示します。  
  
     [!code-csharp[DataGrid_Validation#CourseValidationRule](~/samples/snippets/csharp/VS_Snippets_Wpf/datagrid_validation/cs/mainwindow.xaml.cs#coursevalidationrule)]
     [!code-vb[DataGrid_Validation#CourseValidationRule](~/samples/snippets/visualbasic/VS_Snippets_Wpf/datagrid_validation/vb/mainwindow.xaml.vb#coursevalidationrule)]  
  
2. <xref:System.Windows.Controls.DataGrid.RowValidationRules%2A?displayProperty=nameWithType> コレクションに検証規則を追加します。 <xref:System.Windows.Controls.DataGrid.RowValidationRules%2A> プロパティを使うと、コントロールによって使用されるすべてのバインドをグループ化する <xref:System.Windows.Data.BindingGroup> インスタンスの <xref:System.Windows.Data.BindingGroup.ValidationRules%2A> プロパティに直接アクセスできます。  
  
     次の例では、XAML で <xref:System.Windows.Controls.DataGrid.RowValidationRules%2A> プロパティを設定しています。 バインドされたデータ オブジェクトが更新された後でのみ検証が行われるように、<xref:System.Windows.Controls.ValidationRule.ValidationStep%2A> プロパティは <xref:System.Windows.Controls.ValidationStep.UpdatedValue> に設定されています。  
  
     [!code-xaml[DataGrid_Validation#RowValidationRulesXaml](~/samples/snippets/csharp/VS_Snippets_Wpf/datagrid_validation/cs/mainwindow.xaml#rowvalidationrulesxaml)]  
  
     ユーザーが開始日より前の終了日を指定すると、行ヘッダーに赤い感嘆符 (!) が表示されます。 次の手順で説明するようにして、この既定の検証フィードバックを変更できます。  
  
### <a name="to-customize-row-validation-feedback"></a>行の検証のフィードバックをカスタマイズするには  
  
- <xref:System.Windows.Controls.DataGrid.RowValidationErrorTemplate%2A?displayProperty=nameWithType> プロパティを設定します。 このプロパティを使うと、個々の <xref:System.Windows.Controls.DataGrid> コントロールに対する行の検証フィードバックをカスタマイズできます。 また、暗黙的な行スタイルを使用して <xref:System.Windows.Controls.DataGridRow.ValidationErrorTemplate%2A?displayProperty=nameWithType> プロパティを設定することにより、複数のコントロールに影響を与えることもできます。  
  
     次の例では、行の検証に関する既定のフィードバックを、よりわかりやすいインジケーターに置き換えています。 ユーザーが無効な値を入力すると、白い感嘆符が含まれる赤い円が、行ヘッダーに表示されます。 これは、行とセルの両方の検証エラーに対して発生します。 ツールヒントには関連するエラー メッセージが表示されます。  
  
     [!code-xaml[DataGrid_Validation#RowValidationFeedbackXaml](~/samples/snippets/csharp/VS_Snippets_Wpf/datagrid_validation/cs/mainwindow.xaml#rowvalidationfeedbackxaml)]  
  
## <a name="example"></a>例  
 次の例では、セルと行の検証の完全なデモを示します。 `Course` クラスでは、トランザクションをサポートするための <xref:System.ComponentModel.IEditableObject> を実装するサンプル データ オブジェクトが提供されます。 ユーザーが Esc キーを押して変更を元に戻すことができるように、<xref:System.Windows.Controls.DataGrid> コントロールと <xref:System.ComponentModel.IEditableObject> の間でやり取りが行われます。  
  
> [!NOTE]
> Visual Basic を使用する場合は、MainWindow.xaml の最初の行の `x:Class="DataGridValidation.MainWindow"` を `x:Class="MainWindow"` に置き換えます。  
  
 検証をテストするには、次のようにしてみます。  
  
- [Course ID] 列に、整数以外の値を入力します。  
  
- [End Date] 列に、[Start Date] より前の日付を入力します。  
  
- [Course ID]、[Start Date]、または [End Date] の値を削除します。  
  
- 無効なセルの値を元に戻すには、セルにカーソルを戻し、Esc キーを押します。  
  
- 現在のセルが編集モードのときに行全体の変更を元に戻すには、Esc キーを 2 回押します。  
  
- 検証エラーが発生したら、行ヘッダーのインジケーターをマウスでポイントし、関連付けられているエラー メッセージを表示します。  
  
 [!code-csharp[DataGrid_Validation#FullCode](~/samples/snippets/csharp/VS_Snippets_Wpf/datagrid_validation/cs/mainwindow.xaml.cs#fullcode)]
 [!code-vb[DataGrid_Validation#FullCode](~/samples/snippets/visualbasic/VS_Snippets_Wpf/datagrid_validation/vb/mainwindow.xaml.vb#fullcode)]  
  
 [!code-xaml[DataGrid_Validation#FullXaml](~/samples/snippets/csharp/VS_Snippets_Wpf/datagrid_validation/cs/mainwindow.xaml#fullxaml)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Controls.DataGrid>
- [DataGrid](datagrid.md)
- [データ バインディング](../../../desktop-wpf/data/data-binding-overview.md)
- [バインディングの検証の実装](../data/how-to-implement-binding-validation.md)
- [カスタム オブジェクトに検証ロジックを実装する](../data/how-to-implement-validation-logic-on-custom-objects.md)
