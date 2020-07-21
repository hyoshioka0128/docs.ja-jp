---
title: '方法: SystemParameters を使用する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- classes [WPF], SystemParameters
ms.assetid: 02e7a5de-94eb-4953-b91c-52e6c872ad5b
ms.openlocfilehash: 344fb54b48bcbf188b36a29d8205c21deff713c4
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62001456"
---
# <a name="how-to-use-systemparameters"></a>方法: SystemParameters を使用する
この例では、ボタンのスタイル設定やカスタマイズを行うために、<xref:System.Windows.SystemParameters> のプロパティにアクセスして使用する方法を示します。  
  
## <a name="example"></a>例  
 システム リソースは、システム設定と一貫性のあるビジュアルを作成できるようにするために、いくつかのシステムに基づく設定をリソースとして公開します。 <xref:System.Windows.SystemParameters> は、システム パラメーター値のプロパティ、および値にバインドされるリソース キーの両方を含むクラスです。 たとえば、<xref:System.Windows.SystemParameters.FullPrimaryScreenHeight%2A> は <xref:System.Windows.SystemParameters> プロパティ値であり、<xref:System.Windows.SystemParameters.FullPrimaryScreenHeightKey%2A> は対応するリソース キーです。  
  
 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] では、<xref:System.Windows.SystemParameters> のメンバーを、静的プロパティの使用、または動的リソース参照 (静的プロパティ値をキーとして使用) として使用できます。 アプリケーションの実行時にシステムに基づく値を自動的に更新する場合は、動的リソース参照を使用します。それ以外の場合は、静的参照を使用します。 リソース キーのプロパティ名には、`Key` というサフィックスが付いています。  
  
 次の例では、<xref:System.Windows.SystemParameters> の静的な値にアクセスして使用して、ボタンのスタイル設定またはカスタマイズを行う方法を示します。 このマークアップの例では、ボタンに <xref:System.Windows.SystemParameters> 値を適用して、ボタンのサイズを設定します。  
  
 [!code-xaml[SystemRes_snip#ParameterStaticResources](~/samples/snippets/csharp/VS_Snippets_Wpf/SystemRes_snip/CSharp/Pane1.xaml#parameterstaticresources)]  
  
 コードで <xref:System.Windows.SystemParameters> の値を使用するために、静的参照または動的リソース参照を使用する必要はありません。 代わりに、<xref:System.Windows.SystemParameters> クラスの値を使用します。 キー以外のプロパティは静的プロパティとして定義されますが、システムでホストされた [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] の実行時の動作では、リアルタイムでプロパティが再評価され、ユーザーによるシステム値の変更が正しく反映されます。 次の例では、<xref:System.Windows.SystemParameters> 値を使用して、ボタンの幅と高さを設定する方法を示します。  
  
 [!code-csharp[SystemRes_snip#ParameterResourcesCode](~/samples/snippets/csharp/VS_Snippets_Wpf/SystemRes_snip/CSharp/Pane1.xaml.cs#parameterresourcescode)]
 [!code-vb[SystemRes_snip#ParameterResourcesCode](~/samples/snippets/visualbasic/VS_Snippets_Wpf/SystemRes_snip/VisualBasic/Pane1.xaml.vb#parameterresourcescode)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.SystemParameters>
- [システム ブラシで領域を塗りつぶす](../graphics-multimedia/how-to-paint-an-area-with-a-system-brush.md)
- [SystemFonts を使用する](how-to-use-systemfonts.md)
- [システム パラメーター キーを使用する](how-to-use-system-parameters-keys.md)
- [方法トピック](resources-how-to-topics.md)
