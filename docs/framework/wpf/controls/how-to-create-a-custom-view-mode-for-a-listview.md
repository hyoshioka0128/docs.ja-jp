---
title: '方法: ListView のカスタム表示モードを作成する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- ListView controls [WPF], creating custom View mode
ms.assetid: 71077349-eeb9-4344-ab29-b5df96df3314
ms.openlocfilehash: 3b9ca17bddcecb1895205fca76f0a489ecf25c4f
ms.sourcegitcommit: 7980a91f90ae5eca859db7e6bfa03e23e76a1a50
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/13/2020
ms.locfileid: "81243220"
---
# <a name="how-to-create-a-custom-view-mode-for-a-listview"></a>方法: ListView のカスタム表示モードを作成する

この例では、<xref:System.Windows.Controls.ListView> コントロールのカスタム <xref:System.Windows.Controls.ListView.View%2A> モードを作成する方法を示します。  
  
## <a name="example"></a>例  
 <xref:System.Windows.Controls.ListView> コントロールのカスタム ビューを作成するときは、<xref:System.Windows.Controls.ViewBase> クラスを使用する必要があります。 次の例では、<xref:System.Windows.Controls.ViewBase> クラスから派生する `PlainView` という名前のビュー モードを示します。  
  
 [!code-csharp[ListViewCustomView#PlainView](~/samples/snippets/csharp/VS_Snippets_Wpf/ListViewCustomView/CSharp/PlainView.cs#plainview)]
 [!code-vb[ListViewCustomView#PlainView](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ListViewCustomView/visualbasic/plainview.vb#plainview)]  
  
 カスタム ビューにスタイルを適用するには、<xref:System.Windows.Style> クラスを使用します。 次の例では、`PlainView` ビュー モードに対する <xref:System.Windows.Style> を定義します。 前の例では、`PlainView` に対して定義されている <xref:System.Windows.Controls.ViewBase.DefaultStyleKey%2A> プロパティの値としてこのスタイルを設定しています。  
  
 [!code-xaml[ListViewCustomView#PlainViewStyle](~/samples/snippets/csharp/VS_Snippets_Wpf/ListViewCustomView/CSharp/Themes/Generic.xaml#plainviewstyle)]  
  
 カスタム ビュー モードでデータのレイアウトを定義するには、<xref:System.Windows.DataTemplate> オブジェクトを定義します。 次の例では、`PlainView` ビュー モードでデータを表示するために使用できる <xref:System.Windows.DataTemplate> を定義します。  
  
 [!code-xaml[ListViewCustomView#PlainViewDataTemplate](~/samples/snippets/csharp/VS_Snippets_Wpf/ListViewCustomView/CSharp/Window1.xaml#plainviewdatatemplate)]  
  
 次の例では、前の例で定義されている <xref:System.Windows.DataTemplate> を使用する `PlainView` ビュー モードに対する <xref:System.Windows.ResourceKey> を定義する方法を示します。  
  
 [!code-xaml[ListViewCustomView#PlainViewtileView](~/samples/snippets/csharp/VS_Snippets_Wpf/ListViewCustomView/CSharp/Window1.xaml#plainviewtileview)]  
  
 <xref:System.Windows.Controls.ListView.View%2A> プロパティにリソース キーを設定すると、<xref:System.Windows.Controls.ListView> コントロールでカスタム ビューを使用できます。 次の例では、<xref:System.Windows.Controls.ListView> に対するビュー モードとして `PlainView` を指定する方法を示します。  
  
 [!code-csharp[ListViewCustomView#ListViewtileViewmode](~/samples/snippets/csharp/VS_Snippets_Wpf/ListViewCustomView/CSharp/Window1.xaml.cs#listviewtileviewmode)]
 [!code-vb[ListViewCustomView#ListViewtileViewmode](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ListViewCustomView/visualbasic/window1.xaml.vb#listviewtileviewmode)]  
  
 完全なサンプルについては、[複数のビューを使用する ListView (C#)](https://github.com/dotnet/docs/tree/master/samples/snippets/csharp/VS_Snippets_Wpf/ListViewCustomView/CSharp) または[複数のビューを使用する ListView (Visual Basic)](https://github.com/dotnet/docs/tree/master/samples/snippets/visualbasic/VS_Snippets_Wpf/ListViewCustomView/visualbasic) を参照してください。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Controls.ListView>
- <xref:System.Windows.Controls.GridView>
- [方法トピック](listview-how-to-topics.md)
- [ListView の概要](listview-overview.md)
- [GridView の概要](gridview-overview.md)
