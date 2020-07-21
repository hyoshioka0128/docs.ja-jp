---
title: '方法: ハイパーリンクに下線を引くかどうかを指定する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Hyperlink control type [WPF]
ms.assetid: 3996cfe6-1dac-4835-aeb3-c719ce9cfee5
ms.openlocfilehash: 5718912e24a0697f209669b0ab4e7f4df1765ed3
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61943950"
---
# <a name="how-to-specify-whether-a-hyperlink-is-underlined"></a>方法: ハイパーリンクに下線を引くかどうかを指定する
<xref:System.Windows.Documents.Hyperlink> オブジェクトは、フロー コンテンツにハイパーリンクをホストする、インライン レベルのフロー コンテンツ要素です。 <xref:System.Windows.Documents.Hyperlink> は既定で <xref:System.Windows.TextDecoration> オブジェクトを使用して下線を表示します。 特に <xref:System.Windows.Documents.Hyperlink> オブジェクトの数が多い <xref:System.Windows.TextDecoration> オブジェクトのインスタンス化には、大きな負荷がかかります。 <xref:System.Windows.Documents.Hyperlink> 要素を多数使用する場合は、<xref:System.Windows.ContentElement.MouseEnter> イベントなどのイベントがトリガーされるときにのみ下線を表示することを検討してください。  
  
 次の例では、"My MSN" リンクの下線は、<xref:System.Windows.ContentElement.MouseEnter> イベントがトリガーされたときにだけ表示される動的なものです。  
  
  ![TextDecorations を表示するハイパーリンク](./media/how-to-specify-whether-a-hyperlink-is-underlined/text-decorations-hyperlinks.png)  

## <a name="example"></a>例  
 次のマークアップ サンプルでは、下線ありとなしで定義された <xref:System.Windows.Documents.Hyperlink> を示しています。  
  
 [!code-xaml[Performance#PerformanceSnippet11](~/samples/snippets/csharp/VS_Snippets_Wpf/Performance/CSharp/Hyperlink.xaml#performancesnippet11)]  
  
 次のコード サンプルでは、<xref:System.Windows.ContentElement.MouseEnter> イベントで <xref:System.Windows.Documents.Hyperlink> に下線を作成し、<xref:System.Windows.ContentElement.MouseLeave> イベントで削除する方法を示しています。  
  
 [!code-csharp[Performance#PerformanceSnippet15](~/samples/snippets/csharp/VS_Snippets_Wpf/Performance/CSharp/Hyperlink.xaml.cs#performancesnippet15)]
 [!code-vb[Performance#PerformanceSnippet15](~/samples/snippets/visualbasic/VS_Snippets_Wpf/Performance/visualbasic/hyperlink.xaml.vb#performancesnippet15)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.TextDecoration>
- <xref:System.Windows.Documents.Hyperlink>
- [WPF アプリケーションのパフォーマンスの最適化](optimizing-wpf-application-performance.md)
- [文字の装飾を作成する](how-to-create-a-text-decoration.md)
