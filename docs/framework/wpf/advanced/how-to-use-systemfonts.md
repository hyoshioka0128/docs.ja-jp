---
title: '方法: SystemFonts を使用する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- system fonts [WPF]
- fonts [WPF], system fonts
- classes [WPF], SystemFonts
ms.assetid: 3f46a4ec-2225-408a-8123-8838a8f7057a
ms.openlocfilehash: 157565ceb9057049aef8b2bf274847d58c6b8dc8
ms.sourcegitcommit: f8c36054eab877de4d40a705aacafa2552ce70e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/31/2019
ms.locfileid: "75559964"
---
# <a name="how-to-use-systemfonts"></a>方法: SystemFonts を使用する
この例は、ボタンのスタイル設定やカスタマイズを行うために <xref:System.Windows.SystemFonts> クラスの静的リソースを使用する方法を示しています。  
  
## <a name="example"></a>例  
 システム リソースは、システム設定と一貫性のあるビジュアルを作成できるようにするために、いくつかのシステムによって決定される値を、リソースおよびプロパティの両方として公開します。 <xref:System.Windows.SystemFonts> は、静的プロパティとしてのシステム フォント値、および実行時にこれらの値に動的にアクセスするために使用できるリソース キーを参照するプロパティの両方を含むクラスです。 たとえば、<xref:System.Windows.SystemFonts.CaptionFontFamily%2A> は <xref:System.Windows.SystemFonts> 値であり、<xref:System.Windows.SystemFonts.CaptionFontFamilyKey%2A> は対応するリソース キーです。  
  
 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] では、<xref:System.Windows.SystemFonts> のメンバーを静的プロパティまたは (静的プロパティ値をキーとして使用する) 動的リソース参照として使用できます。 アプリケーションの実行時にフォント メトリックを自動的に更新する場合は、動的リソース参照を使用します。それ以外の場合は、静的な値参照を使用します。  
  
> [!NOTE]
> リソース キーでは、プロパティ名に"Key"というサフィックスが付いています。  
  
 次の例は、ボタンのスタイル設定またはカスタマイズを行うために静的な値として <xref:System.Windows.SystemFonts> のプロパティにアクセスして使用する方法を示しています。 このマークアップの例では、<xref:System.Windows.SystemFonts> 値をボタンに割り当てます。  
  
 [!code-xaml[SystemRes_snip#FontStaticResources](~/samples/snippets/csharp/VS_Snippets_Wpf/SystemRes_snip/CSharp/Pane1.xaml#fontstaticresources)]  
  
 コードで <xref:System.Windows.SystemFonts> の値を使用するために、静的な値または動的リソース参照を使用する必要はありません。 代わりに、<xref:System.Windows.SystemFonts> クラスの非キー プロパティを使用します。 キー以外のプロパティは、静的プロパティとして定義されますが、システムでホストされた [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] の実行時の動作では、リアルタイムでプロパティが再評価され、ユーザーによるシステム値の変更が正しく反映されます。 次の例では、ボタンのフォント設定を指定する方法を示します。  
  
 [!code-csharp[SystemRes_snip#FontResourcesCode](~/samples/snippets/csharp/VS_Snippets_Wpf/SystemRes_snip/CSharp/Pane1.xaml.cs#fontresourcescode)]
 [!code-vb[SystemRes_snip#FontResourcesCode](~/samples/snippets/visualbasic/VS_Snippets_Wpf/SystemRes_snip/VisualBasic/Pane1.xaml.vb#fontresourcescode)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.SystemFonts>
- [システム ブラシで領域を塗りつぶす](../graphics-multimedia/how-to-paint-an-area-with-a-system-brush.md)
- [SystemParameters を使用する](how-to-use-systemparameters.md)
- [システム フォント キーを使用する](how-to-use-system-fonts-keys.md)
- [方法トピック](resources-how-to-topics.md)
- [x:Static のマークアップ拡張機能](../../../desktop-wpf/xaml-services/xstatic-markup-extension.md)
- [XAML リソース](../../../desktop-wpf/fundamentals/xaml-resources-define.md)
- [DynamicResource マークアップ拡張](dynamicresource-markup-extension.md)
