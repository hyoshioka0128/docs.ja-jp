---
title: '方法: ListBox にデータをバインドする'
ms.date: 03/30/2017
helpviewer_keywords:
- ListBox controls [WPF], binding data to
- data binding [WPF], ListBox control
- binding data [WPF], to ListBox control
ms.assetid: de93a907-709a-44a7-84bf-578b846a3d8b
ms.openlocfilehash: 4dea53a524247d18628b3e7e7b2c06906dced53d
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61911158"
---
# <a name="how-to-bind-a-listbox-to-data"></a>方法: ListBox にデータをバインドする
アプリケーションの開発者は、各 <xref:System.Windows.Controls.ListBoxItem> のコンテンツを別々に指定せず、<xref:System.Windows.Controls.ListBox> コントロールを作成できます。 データ バインディングを使用し、データを個々の項目にバインドできます。  
  
 次の例では、*Colors* という名称のデータ ソースにデータ バインディングすることで <xref:System.Windows.Controls.ListBoxItem> 要素にデータを入力する <xref:System.Windows.Controls.ListBox> を作成する方法を示します。 この場合、<xref:System.Windows.Controls.ListBoxItem> タグを使用し、各項目のコンテンツを指定する必要はありません。  
  
## <a name="example"></a>例  
 [!code-xaml[ListBoxEvent#7](~/samples/snippets/csharp/VS_Snippets_Wpf/ListBoxEvent/CSharp/Pane1.xaml#7)]  
[!code-xaml[ListBoxEvent#3](~/samples/snippets/csharp/VS_Snippets_Wpf/ListBoxEvent/CSharp/Pane1.xaml#3)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Controls.ListBox>
- <xref:System.Windows.Controls.ListBoxItem>
- [コントロール](../advanced/optimizing-performance-controls.md)
