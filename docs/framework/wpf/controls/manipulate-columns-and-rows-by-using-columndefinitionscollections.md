---
title: '方法: ColumnDefinitionsCollections および RowDefinitionsCollections を使用して列と行を操作する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- controls [WPF], Grid class
- Grid control [WPF], ColumnDefinitionCollection class
- Grid control [WPF], RowDefinitionCollection class
ms.assetid: bfc7160a-45f2-4e17-9961-df414dfb13c5
ms.openlocfilehash: f316cced076223edba1d39c9cfb21b9a504b9eee
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62017671"
---
# <a name="how-to-manipulate-columns-and-rows-by-using-columndefinitionscollections-and-rowdefinitionscollections"></a>方法: ColumnDefinitionsCollections および RowDefinitionsCollections を使用して列と行を操作する
この例では、<xref:System.Windows.Controls.ColumnDefinitionCollection> クラスと <xref:System.Windows.Controls.RowDefinitionCollection> クラスのメソッドを使用して、行または列のコンテンツの追加、クリア、カウントなどの操作を実行する方法を示します。 たとえば、<xref:System.Windows.Controls.ColumnDefinition> または <xref:System.Windows.Controls.RowDefinition> に含まれる項目を <xref:System.Windows.Controls.ColumnDefinitionCollection.Add%2A>、<xref:System.Windows.Controls.ColumnDefinitionCollection.Clear%2A>、または <xref:System.Windows.Controls.ColumnDefinitionCollection.Count%2A> できます。  
  
## <a name="example"></a>例  
 次の例では、`grid1` という <xref:System.Windows.FrameworkElement.Name%2A> を持つ <xref:System.Windows.Controls.Grid> 要素を作成します。 <xref:System.Windows.Controls.Grid> には、<xref:System.Windows.Controls.Button> 要素を保持する <xref:System.Windows.Controls.StackPanel> が含まれており、異なるコレクションメソッドによってそれぞれが制御されます。 <xref:System.Windows.Controls.Button> をクリックすると、分離コード ファイル内のメソッド呼び出しがアクティブ化されます。  
  
 [!code-xaml[ColumnDefinitionsGrid#1](~/samples/snippets/csharp/VS_Snippets_Wpf/ColumnDefinitionsGrid/CSharp/Window1.xaml#1)]  
  
 この例では、[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] ファイル内の <xref:System.Windows.Controls.Primitives.ButtonBase.Click> イベントに対応する一連のカスタム メソッドを定義します。 <xref:System.Windows.Controls.Grid> の列と行の数を変更するには、行や列の追加や削除など、いくつかの方法があり、行と列の合計数をカウントすることもできます。 <xref:System.ArgumentOutOfRangeException> と <xref:System.ArgumentException> の例外を回避するには、<xref:System.Windows.Controls.ColumnDefinitionCollection.RemoveRange%2A> メソッドが提供するエラー チェック機能を使用できます。  
  
 [!code-csharp[ColumnDefinitionsGrid#2](~/samples/snippets/csharp/VS_Snippets_Wpf/ColumnDefinitionsGrid/CSharp/Window1.xaml.cs#2)]
 [!code-vb[ColumnDefinitionsGrid#2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ColumnDefinitionsGrid/VisualBasic/Window1.xaml.vb#2)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Controls.Grid>
- <xref:System.Windows.Controls.ColumnDefinitionCollection>
- <xref:System.Windows.Controls.RowDefinitionCollection>
