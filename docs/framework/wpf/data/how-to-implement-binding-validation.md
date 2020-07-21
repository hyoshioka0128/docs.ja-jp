---
title: '方法: バインディングの検証の実装'
description: Windows Presentation Foundation (WPF) で、無効な値が入力されたときにバインディングの検証を使用してユーザーに視覚的フィードバックを提供する方法について説明します。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- validation of binding [WPF]
- data binding [WPF], validation of binding
- binding [WPF], validation of
ms.assetid: eb98b33d-9866-49ae-b981-bc5ff20d607a
ms.openlocfilehash: 0813be9f79a83a9dae26db1dadb58b5e973339fd
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85617883"
---
# <a name="how-to-implement-binding-validation"></a>方法: バインディングの検証の実装

この例では、<xref:System.Windows.Controls.Validation.ErrorTemplate%2A> とスタイル トリガーを使用して、カスタム検証規則に基づき無効な値が入力されたことをユーザーに通知するための視覚的フィードバックを提供する方法を示します。

## <a name="example"></a>例

次の例で使用されている <xref:System.Windows.Controls.TextBox> のテキストの内容は、`ods` という名前のバインディング ソース オブジェクトの `Age` プロパティ (int 型) にバインドされています。 バインディングは、`AgeRangeRule` という名前の検証規則を使用するよう設定されているため、ユーザーが数字以外の文字、または 21 から 130 の範囲外の値を入力すると、テキスト ボックスの横に赤の感嘆符が表示され、ユーザーがテキスト ボックス上にマウスを置くとエラー メッセージを含んだツール ヒントが示されます。

[!code-xaml[BindValidation#2](~/samples/snippets/csharp/VS_Snippets_Wpf/BindValidation/CSharp/Window1.xaml#2)]

次の例では、`AgeRangeRule` が継承され、<xref:System.Windows.Controls.ValidationRule> メソッドがオーバーライドされている、<xref:System.Windows.Controls.ValidationRule.Validate%2A> の実装を示します。 `Int32.Parse` メソッドは、値に無効な文字が含まれていないことを確認するために、値に対して呼び出されます。 <xref:System.Windows.Controls.ValidationRule.Validate%2A> メソッドでは、解析中に例外が発生したかどうか、および年齢値が範囲外にあるかどうかに基づいて、値が有効かどうかを示す <xref:System.Windows.Controls.ValidationResult> が返されます。

[!code-csharp[BindValidation#3](~/samples/snippets/csharp/VS_Snippets_Wpf/BindValidation/CSharp/AgeRangeRule.cs#3)]
[!code-vb[BindValidation#3](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BindValidation/VisualBasic/AgeRangeRule.vb#3)]

次の例では、検証エラーをユーザーに通知する赤い感嘆符を作成するための、カスタム <xref:System.Windows.Controls.ControlTemplate> `validationTemplate` を示します。 コントロール テンプレートは、コントロールの外観を再定義するために使用されます。

[!code-xaml[BindValidation#4](~/samples/snippets/csharp/VS_Snippets_Wpf/BindValidation/CSharp/Window1.xaml#4)]

次の例に示すように、エラー メッセージを表示する <xref:System.Windows.Controls.ToolTip> は、`textBoxInError` という名前のスタイルを使用して作成されます。 <xref:System.Windows.Controls.Validation.HasError%2A> の値が `true` である場合、トリガーによって現在の <xref:System.Windows.Controls.TextBox> のツール ヒントに、最初の検証エラーが設定されます。 <xref:System.Windows.Data.Binding.RelativeSource%2A> には、現在の要素を参照している <xref:System.Windows.Data.RelativeSourceMode.Self> が設定されます。

[!code-xaml[BindValidation#5](~/samples/snippets/csharp/VS_Snippets_Wpf/BindValidation/CSharp/Window1.xaml#5)]

完全な例については、[バインド検証のサンプル](https://github.com/Microsoft/WPF-Samples/tree/master/Data%20Binding/BindValidation)をご覧ください。
  
カスタム <xref:System.Windows.Controls.Validation.ErrorTemplate%2A> を提供しない場合、検証エラーがあったときにユーザーに視覚的にフィードバックするために、既定のエラー テンプレートが表示されることに注意してください。 詳しくは、「[データ バインドの概要](../../../desktop-wpf/data/data-binding-overview.md)」の「データの検証」をご覧ください。 さらに [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] は、バインディング ソース プロパティの更新中にスローされる例外をキャッチするための、組み込みの検証規則を提供します。 詳細については、「<xref:System.Windows.Controls.ExceptionValidationRule>」を参照してください。

## <a name="see-also"></a>関連項目

- [データ バインディングの概要](../../../desktop-wpf/data/data-binding-overview.md)
- [方法トピック](data-binding-how-to-topics.md)
