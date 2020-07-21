---
title: グリフを使用したテキストの描画
ms.date: 03/30/2017
helpviewer_keywords:
- text [WPF], drawing with Glyphs objects
- Glyphs objects [WPF], drawing text
- typography [WPF], Glyphs objects
ms.assetid: 587ab17e-a419-4ad5-b6da-8933a8e83d97
ms.openlocfilehash: 55bbc50de519d6607a843fcd633f2c07db53109f
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62010372"
---
# <a name="draw-text-using-glyphs"></a>グリフを使用したテキストの描画
このトピックでは、低レベルの <xref:System.Windows.Documents.Glyphs> オブジェクトを使用して [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] にテキストを表示する方法について説明します。  
  
## <a name="example"></a>例  
 次の例は、[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] の <xref:System.Windows.Documents.Glyphs> オブジェクトのプロパティを定義する方法を示しています。 <xref:System.Windows.Documents.Glyphs> オブジェクトによって、[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] の <xref:System.Windows.Media.GlyphRun> の出力を表します。 この例では、Arial、Courier New、Times New Roman フォントがローカル コンピューターの C:\WINDOWS\Fonts フォルダーにインストールされていると想定しています。  
  
 [!code-xaml[GlyphsOvwSample1#1](~/samples/snippets/csharp/VS_Snippets_Wpf/GlyphsOvwSample1/CS/default.xaml#1)]  
  
 この例は、[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] の <xref:System.Windows.Documents.Glyphs> オブジェクトの他のプロパティを定義する方法を示しています。  
  
 [!code-xaml[GlyphsOvwSamp2#1](~/samples/snippets/csharp/VS_Snippets_Wpf/GlyphsOvwSamp2/CS/default.xaml#1)]  
  
## <a name="see-also"></a>関連項目

- [WPF のタイポグラフィ](typography-in-wpf.md)
