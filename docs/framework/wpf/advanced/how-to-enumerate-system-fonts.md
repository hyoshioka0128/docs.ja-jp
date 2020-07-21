---
title: '方法: システム フォントを列挙する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- typography [WPF], enumerating system fonts
- fonts [WPF], enumerating
- system fonts [WPF], enumerating
- enumerating [WPF], system fonts
ms.assetid: 36e37791-55b9-4f01-a496-5cc10335e6a6
ms.openlocfilehash: c7e81b5d1b70ba911a0b505219f7977e019038cf
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62001599"
---
# <a name="how-to-enumerate-system-fonts"></a>方法: システム フォントを列挙する
## <a name="example"></a>例  
 次の例では、システム フォント コレクション内のフォントを列挙する方法を示します。 <xref:System.Windows.Media.Fonts.SystemFontFamilies%2A> 内の各 <xref:System.Windows.Media.FontFamily> のフォント ファミリ名が、項目としてコンボ ボックスに追加されます。  
  
 [!code-csharp[TextOverview#100](~/samples/snippets/csharp/VS_Snippets_Wpf/TextOverview/CSharp/Window1.xaml.cs#100)]
 [!code-vb[TextOverview#100](~/samples/snippets/visualbasic/VS_Snippets_Wpf/TextOverview/visualbasic/window1.xaml.vb#100)]  
  
 同じフォント ファミリの複数のバージョンが同じディレクトリ内に存在する場合、[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] フォント列挙体は、フォントの最新バージョンを返します。 バージョン情報に解決策が用意されていない場合は、最新タイムスタンプが含まれるフォントが返されます。 タイムスタンプ情報が等しい場合は、最初はアルファベット順になっているフォント ファイルが返されます。
