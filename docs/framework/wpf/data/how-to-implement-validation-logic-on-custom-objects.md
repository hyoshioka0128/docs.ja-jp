---
title: '方法: カスタム オブジェクトに検証ロジックを実装する'
ms.date: 08/02/2018
dev_langs:
- csharp
- vb
helpviewer_keywords:
- checking for validation errors [WPF]
- validation errors [WPF], checking for
- implementing validation logic on custom objects [WPF]
- custom objects [WPF], implementing validation logic on
ms.assetid: 751fda9b-44f9-4d63-b4f2-1df07ac41e0f
ms.openlocfilehash: 8520504757e9e9ec9557b84ca2608b4cb99daf62
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61931399"
---
# <a name="how-to-implement-validation-logic-on-custom-objects"></a>方法: カスタム オブジェクトに検証ロジックを実装する
この例では、カスタム オブジェクトに検証ロジックを実装し、それにバインドする方法を示します。  
  
## <a name="example"></a>例  
 ソース オブジェクトで <xref:System.ComponentModel.IDataErrorInfo> が実装されている場合、ビジネス レイヤーで検証ロジックを提供できます。次に示す例では、<xref:System.ComponentModel.IDataErrorInfo> を実装する `Person` オブジェクトが定義されています、  
  
 [!code-csharp[BusinessLayerValidation#IDataErrorInfo](~/samples/snippets/csharp/VS_Snippets_Wpf/BusinessLayerValidation/CSharp/Data.cs#idataerrorinfo)]
 [!code-vb[BusinessLayerValidation#IDataErrorInfo](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BusinessLayerValidation/VisualBasic/Data.vb#idataerrorinfo)]  
  
 次の例では、テキスト ボックスのテキスト プロパティが、`Person.Age` プロパティにバインドされています。このプロパティは、`x:Key` `data` が指定されているリソースによって、バインドに使用できるようになっています。 <xref:System.Windows.Controls.DataErrorValidationRule> では、<xref:System.ComponentModel.IDataErrorInfo> の実装によって発生する検証エラーがチェックされます。  
  
 [!code-xaml[BusinessLayerValidation#BoundTextBox](~/samples/snippets/csharp/VS_Snippets_Wpf/BusinessLayerValidation/CSharp/Window1.xaml?highlight=8,11-19,25-42)]  
  
 または、<xref:System.Windows.Controls.DataErrorValidationRule> を使用する代わりに、<xref:System.Windows.Data.Binding.ValidatesOnDataErrors%2A> プロパティを `true` に設定してもかまいません。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Controls.ExceptionValidationRule>
- [バインディングの検証の実装](how-to-implement-binding-validation.md)
- [方法トピック](data-binding-how-to-topics.md)
