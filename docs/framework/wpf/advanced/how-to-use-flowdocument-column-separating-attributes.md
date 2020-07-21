---
title: '方法: FlowDocument の列区切り属性を使用する'
ms.date: 03/30/2017
helpviewer_keywords:
- FlowDocument column-separating attributes
- column-separating attributes
- documents [WPF], FlowDocument column-separating attributes
ms.assetid: c7a822f8-aeca-45bd-a258-2852ff28005c
ms.openlocfilehash: 27491b21da587fa198061ba52d8daed5d3f28de3
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62032046"
---
# <a name="how-to-use-flowdocument-column-separating-attributes"></a>方法: FlowDocument の列区切り属性を使用する
この例では、<xref:System.Windows.Documents.FlowDocument> の列区切り機能を使用する方法を示します。  
  
## <a name="example"></a>例  
 次の例では、<xref:System.Windows.Documents.FlowDocument> が定義され、<xref:System.Windows.Documents.FlowDocument.ColumnGap%2A>、<xref:System.Windows.Documents.FlowDocument.ColumnRuleBrush%2A>、<xref:System.Windows.Documents.FlowDocument.ColumnRuleWidth%2A> という属性が設定されます。  <xref:System.Windows.Documents.FlowDocument> には、サンプル コンテンツの段落が 1 つ含まれます。  
  
 [!code-xaml[FlowDocumentSnippets#_FlowDocumentColumnStuffXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/FlowDocumentSnippets/CSharp/Window1.xaml#_flowdocumentcolumnstuffxaml)]  
  
 次の画像では、レンダリングされた <xref:System.Windows.Documents.FlowDocument> での属性 <xref:System.Windows.Documents.FlowDocument.ColumnGap%2A>、<xref:System.Windows.Documents.FlowDocument.ColumnRuleBrush%2A>、<xref:System.Windows.Documents.FlowDocument.ColumnRuleWidth%2A> の効果を示します。  
  
 ![FlowDocument Intra Column 属性を示すスクリーンショット](./media/how-to-use-flowdocument-column-separating-attributes/flowdocument-intra-column.png)
