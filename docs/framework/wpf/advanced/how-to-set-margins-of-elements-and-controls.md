---
title: '方法: 要素およびコントロールのマージンを設定する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- setting [WPF], Margin property
- properties [WPF], Margin property
- Margin property [WPF], setting
ms.assetid: 70ebee01-6f87-4352-8dd4-402c65eaaed6
ms.openlocfilehash: 3263810806b6b4bbec15eadfd1f1da3a57d12698
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62052366"
---
# <a name="how-to-set-margins-of-elements-and-controls"></a>方法: 要素およびコントロールのマージンを設定する
この例では、分離コードのマージンにプロパティ値があればそれを変更することで <xref:System.Windows.FrameworkElement.Margin%2A> プロパティを設定する方法を示します。 <xref:System.Windows.FrameworkElement.Margin%2A> プロパティは <xref:System.Windows.FrameworkElement> 基本要素のプロパティであり、そのため、さまざまなコントロールやその他の要素で継承されます。  
  
 この例は [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] で記述されており、分離コード ファイルは [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] で参照されます。 分離コードは C# と Microsoft Visual Basic の両方のバージョンで表示されます。  
  
## <a name="example"></a>例  
 [!code-xaml[FEMarginProgrammatic#XAML](~/samples/snippets/csharp/VS_Snippets_Wpf/FEMarginProgrammatic/CSharp/default.xaml#xaml)]  
  
 [!code-csharp[FEMarginProgrammatic#Handler](~/samples/snippets/csharp/VS_Snippets_Wpf/FEMarginProgrammatic/CSharp/default.xaml.cs#handler)]
 [!code-vb[FEMarginProgrammatic#Handler](~/samples/snippets/visualbasic/VS_Snippets_Wpf/FEMarginProgrammatic/VisualBasic/default.xaml.vb#handler)]
