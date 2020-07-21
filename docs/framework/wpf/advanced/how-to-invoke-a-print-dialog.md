---
title: '方法: 印刷ダイアログ ボックスを呼び出す'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- invoking print dialogs [WPF]
- print dialogs [WPF], invoking
ms.assetid: e3a2c84c-74fe-45a4-8501-5813f9dbfed2
ms.openlocfilehash: f7ef3312d876324b44b055d70fd22e3fba075ec6
ms.sourcegitcommit: 011314e0c8eb4cf4a11d92078f58176c8c3efd2d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/09/2020
ms.locfileid: "77095178"
---
# <a name="how-to-invoke-a-print-dialog"></a>方法: 印刷ダイアログ ボックスを呼び出す
アプリケーションから印刷する機能を提供するには、<xref:System.Windows.Controls.PrintDialog> オブジェクトを作成して開くだけで済みます。  
  
## <a name="example"></a>例  
 <xref:System.Windows.Controls.PrintDialog> コントロールには、[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]、構成、および XPS ジョブの送信用に 1 つのエントリ ポイントが用意されています。 このコントロールは使いやすく、[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] マークアップまたはコードを使用してインスタンス化できます。 コードでコントロールをインスタンス化して開く方法と、そこから印刷する方法の例を次に示します。 また、ダイアログで、特定の範囲のページを設定するオプションをユーザーに提供する方法も示します。 このコード例では、C: ドライブのルートに FixedDocumentSequence.xps ファイルがあることを前提としています。  
  
 [!code-csharp[printdialog#1](~/samples/snippets/csharp/VS_Snippets_Wpf/PrintDialog/CSharp/Window1.xaml.cs#1)]
 [!code-vb[printdialog#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/PrintDialog/visualbasic/window1.xaml.vb#1)]  
  
 ダイアログが開くと、ユーザーはコンピューターにインストールされているプリンターから選択できます。 また、[[Microsoft XPS ドキュメント ライター]](/windows/win32/printdocs/microsoft-xps-document-writer) を選択し、印刷するのではなく XML Paper Specification (XPS) ファイルを作成することもできます。  
  
> [!NOTE]
> このトピックで説明されている WPF の <xref:System.Windows.Controls.PrintDialog?displayProperty=nameWithType> コントロールは、Windows フォームの <xref:System.Windows.Forms.PrintDialog?displayProperty=nameWithType> コンポーネントと混同しないでください。  
  
 厳密に言うと、ダイアログを開かなくても <xref:System.Windows.Controls.PrintDialog.PrintDocument%2A> メソッドを使用できます。 その意味で、コントロールは目に見えない印刷コンポーネントとして使用できます。 ただし、パフォーマンス上の理由から、<xref:System.Printing.PrintQueue.AddJob%2A> メソッド、または <xref:System.Windows.Xps.XpsDocumentWriter> の多くの <xref:System.Windows.Xps.XpsDocumentWriter.Write%2A> および <xref:System.Windows.Xps.XpsDocumentWriter.WriteAsync%2A> メソッドのいずれかを使用することをお勧めします。 この詳細については、[プログラムで XPS ファイルを印刷する](how-to-programmatically-print-xps-files.md)方法に関するページを参照してください。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Controls.PrintDialog>
- [WPF のドキュメント](documents-in-wpf.md)
- [印刷の概要](printing-overview.md)
- [Microsoft XPS Document Writer](/windows/win32/printdocs/microsoft-xps-document-writer)
