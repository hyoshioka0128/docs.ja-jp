---
title: '方法: GroupBox テンプレートを定義する'
ms.date: 03/30/2017
helpviewer_keywords:
- controls [WPF], GroupBox
- GroupBox control [WPF], creating templates
ms.assetid: 85a4d1a7-4753-4f4a-b26d-14fa10c1ddb5
ms.openlocfilehash: dd53af87ec2d12b2ed0dcf2b23374d76e8f631a9
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61910521"
---
# <a name="how-to-define-a-groupbox-template"></a>方法: GroupBox テンプレートを定義する
この例では、<xref:System.Windows.Controls.GroupBox> コントロールのテンプレートを作成する方法を示します。  
  
## <a name="example"></a>例  
 次の例では、レイアウトに <xref:System.Windows.Controls.Grid> コントロールを使用することで <xref:System.Windows.Controls.GroupBox> コントロール テンプレートが定義されています。 境界によって <xref:System.Windows.Controls.HeaderedContentControl.Header%2A> コンテンツが隠されないよう、このテンプレートでは <xref:System.Windows.Controls.BorderGapMaskConverter> を使用して <xref:System.Windows.Controls.GroupBox> の境界が定義されます。  
  
 [!code-xaml[GroupBoxSnippet#GroupBoxTemplate](~/samples/snippets/csharp/VS_Snippets_Wpf/GroupBoxSnippet/CS/Window1.xaml#groupboxtemplate)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Controls.GroupBox>
- [方法: GroupBox を作成する](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms748321(v=vs.90))
