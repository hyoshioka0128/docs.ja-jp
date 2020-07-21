---
title: WindowsFormsHost 要素のレイアウトに関する考慮事項
ms.date: 03/30/2017
helpviewer_keywords:
- Windows Forms [WPF], interoperability with
- Windows Forms [WPF], WPF interoperation
- interoperability [WPF], Windows Forms
- WindowsFormsHost element layout considerations [WPF]
- dynamic layout [WPF interoperability]
- device-independent pixels
ms.assetid: 3c574597-bbde-440f-95cc-01371f1a5d9d
ms.openlocfilehash: 89ed57a787b93a1326b4accd3bb1bc5ff9a825fd
ms.sourcegitcommit: 011314e0c8eb4cf4a11d92078f58176c8c3efd2d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/09/2020
ms.locfileid: "77095152"
---
# <a name="layout-considerations-for-the-windowsformshost-element"></a>WindowsFormsHost 要素のレイアウトに関する考慮事項
このトピックでは、<xref:System.Windows.Forms.Integration.WindowsFormsHost> 要素と [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] レイアウト システムの対話方法について説明します。  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] と Windows フォームは、フォームまたはページ上の要素のサイズ変更と配置について、異なる点はありますが似たロジックをサポートしています。 Windows フォーム コントロールをホストするハイブリッド ユーザー インターフェイス (UI) を [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] で作成すると、<xref:System.Windows.Forms.Integration.WindowsFormsHost> 要素によって 2 つのレイアウト スキームが統合されます。  
  
## <a name="differences-in-layout-between-wpf-and-windows-forms"></a>WPF と Windows フォームのレイアウトの違い  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] には、解像度に依存しないレイアウトが使用されます。 すべての [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] レイアウト寸法は、"*デバイス非依存ピクセル*" を使用して指定されます。 デバイス非依存ピクセルは、サイズが 96 分の 1 インチであり、解像度に依存しません。そのため、レンダリング先が 72 dpi モニターか 19,200 dpi プリンターかに関係なく、同様の結果が得られます。  
  
 また、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] は "*動的レイアウト*" にも基づいています。 つまり、そのコンテンツ、その親レイアウト コンテナー、および使用できる画面サイズに応じて、UI 要素はフォームまたはページ上に自動的に配置されます。 動的レイアウトを使用すると、含まれる文字列の長さが変化したときに、UI 要素のサイズと位置が自動的に調整されるので、ローカリゼーションが容易になります。  
  
 Windows フォームのレイアウトはデバイスに依存し、静的である可能性が高くなります。 通常、Windows フォーム コントロールは、ハードウェア ピクセルで指定された寸法を使用して、フォーム上に絶対配置されます。 ただし、Windows フォームは、次の表に示すように、いくつかの動的レイアウト機能をサポートしています。  
  
|レイアウト機能|説明|  
|--------------------|-----------------|  
|自動サイズ調整|一部の Windows フォーム コントロールは、コンテンツを適切に表示するために自動的にサイズが変更されます。 詳細については、「[AutoSize プロパティの概要](../../winforms/controls/autosize-property-overview.md)」を参照してください。|  
|固定とドッキング|Windows フォーム コントロールは、親コンテナーに基づく配置とサイズ変更をサポートします。 詳細については、次のトピックを参照してください。 <xref:System.Windows.Forms.Control.Anchor%2A?displayProperty=nameWithType> および <xref:System.Windows.Forms.Control.Dock%2A?displayProperty=nameWithType>|  
|自動スケール|コンテナー コントロールでは、出力デバイスの解像度または既定のコンテナー フォントのサイズ (ピクセル単位) に基づいて自身とその子のサイズが変更されます。 詳細については、「[Windows フォームでの自動スケーリング](../../winforms/automatic-scaling-in-windows-forms.md)」を参照してください。|  
|レイアウト コンテナー|<xref:System.Windows.Forms.FlowLayoutPanel> および <xref:System.Windows.Forms.TableLayoutPanel> コントロールでは、その子コントロールが配置され、コンテンツに応じてサイズが変更されます。|  
  
## <a name="layout-limitations"></a>レイアウトの制限事項  
 一般に、Windows フォーム コントロールは、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] で可能な範囲までスケーリングおよび変換することができません。 次の一覧では、<xref:System.Windows.Forms.Integration.WindowsFormsHost> 要素を使用して、ホストされている Windows フォーム コントロールを [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] レイアウト システムに統合しようとした場合の、既知の制限事項について説明します。  
  
- 場合によっては、Windows フォーム コントロールのサイズを変更できません。または、特定のサイズにしか限定できません。 たとえば、Windows フォームの <xref:System.Windows.Forms.ComboBox> コントロールでは、コントロールのフォント サイズによって定義される 1 つの高さのみがサポートされます。 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] の動的レイアウトでは、要素は垂直方向に伸縮できますが、ホストされている <xref:System.Windows.Forms.ComboBox> コントロールは想定どおりに伸縮されません。  
  
- Windows フォーム コントロールを回転または傾斜させることはできません。 傾斜または回転変換を適用すると、<xref:System.Windows.Forms.Integration.WindowsFormsHost> 要素によって <xref:System.Windows.Forms.Integration.WindowsFormsHost.LayoutError> イベントが発生します。 <xref:System.Windows.Forms.Integration.WindowsFormsHost.LayoutError> イベントを処理しない場合、<xref:System.InvalidOperationException> が発生します。  
  
- ほとんどの場合、Windows フォーム コントロールでは比率を維持したスケーリングはサポートされていません。 コントロール全体の寸法はスケーリングされますが、コントロールの子コントロールとコンポーネント要素は、想定したとおりにサイズ変更されない可能性があります。 この制限は、各 Windows フォーム コントロールでスケーリングがどの程度サポートされているかによって異なります。 また、Windows フォーム コントロールのサイズを 0 ピクセルに縮小することはできません。  
  
- Windows フォーム コントロールは、自動スケーリングをサポートしており、フォームとそのコントロールはフォント サイズに基づいて自動的にサイズが変更されます。 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] のユーザー インターフェイスでは、フォント サイズを変更してもレイアウト全体のサイズは変更されませんが、個々の要素のサイズは動的に変更される可能性があります。  
  
### <a name="z-order"></a>z オーダー  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] のユーザー インターフェイスでは、要素の z オーダーを変更して、重なり具合を制御できます。 ホストされている Windows フォーム コントロールは別の HWND で描画されるため、常に [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 要素の上に描画されます。  
  
 ホストされている Windows フォーム コントロールも <xref:System.Windows.Documents.Adorner> 要素の上に描画されます。  
  
## <a name="layout-behavior"></a>レイアウト動作  
 以下のセクションでは、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] で Windows フォーム コントロールをホストするときのレイアウト動作の特定の側面について説明します。  
  
### <a name="scaling-unit-conversion-and-device-independence"></a>スケーリング、単位変換、デバイス非依存  
 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 要素によって [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] および Windows フォームの寸法が関係する操作を実行するときは常に、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 用のデバイス非依存ピクセルと Windows フォーム用のハードウェア ピクセルという 2 つの座標系が関係します。 そのため、一貫したレイアウトを実現するには、適切な単位変換とスケーリング変換を適用する必要があります。  
  
 座標系間の変換は、現在のデバイス解像度と、<xref:System.Windows.Forms.Integration.WindowsFormsHost> 要素またはその先祖に適用されたレイアウトまたはレンダリング変換によって変わります。  
  
 出力デバイスが 96 dpi であり、<xref:System.Windows.Forms.Integration.WindowsFormsHost> 要素にスケーリングが適用されていない場合、1 デバイス非依存ピクルは 1 ハードウェア ピクセルと等しくなります。  
  
 それ以外の場合は、座標系のスケーリングが必要です。 ホストされているコントロールはサイズが変更されません。 代わりに、<xref:System.Windows.Forms.Integration.WindowsFormsHost> 要素では、ホストされているコントロールとそのすべての子コントロールのスケーリングが試行されます。 Windows フォームはスケーリングを完全にはサポートしていないため、<xref:System.Windows.Forms.Integration.WindowsFormsHost> 要素は、特定のコントロールでサポートされる範囲までスケーリングされます。  
  
 ホストされている Windows フォーム コントロールにカスタムのスケーリング動作を提供するように、<xref:System.Windows.Forms.Integration.WindowsFormsHost.ScaleChild%2A> メソッドをオーバーライドします。  
  
 スケーリングに加えて、<xref:System.Windows.Forms.Integration.WindowsFormsHost> 要素では、次の表に示すように、丸めとオーバーフローのケースが処理されます。  
  
|変換の問題|説明|  
|----------------------|-----------------|  
|丸め|[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] のデバイス非依存ピクセルの寸法は `double` として指定されます。また、Windows フォームのハードウェア ピクセルの寸法は `int` として指定されます。 `double`ベースの寸法が `int` ベースの寸法に変換される場合、<xref:System.Windows.Forms.Integration.WindowsFormsHost> 要素には標準の丸めが使用されるため、0.5 未満の小数値は 0 に切り捨てられます。|  
|オーバーフロー|<xref:System.Windows.Forms.Integration.WindowsFormsHost> 要素が `double` 値から `int` 値に変換されると、オーバーフローが発生する可能性があります。 <xref:System.Int32.MaxValue> を超える値は <xref:System.Int32.MaxValue> に設定されます。|  
  
### <a name="layout-related-properties"></a>レイアウト関連のプロパティ  
 Windows フォーム コントロールのレイアウト動作を制御するプロパティと [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 要素は、<xref:System.Windows.Forms.Integration.WindowsFormsHost> 要素によって適切にマップされます。 詳細については、「[Windows フォームと WPF プロパティの割り当て](windows-forms-and-wpf-property-mapping.md)」を参照してください。  
  
### <a name="layout-changes-in-the-hosted-control"></a>ホストされているコントロールのレイアウト変更  
 ホストされている Windows フォーム コントロールのレイアウト変更は、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] に伝達され、レイアウトの更新がトリガーされます。 <xref:System.Windows.Forms.Integration.WindowsFormsHost> に対して <xref:System.Windows.UIElement.InvalidateMeasure%2A> メソッドを実行すると、ホストされているコントロールのレイアウト変更により、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] レイアウト エンジンが実行されます。  
  
### <a name="continuously-sized-windows-forms-controls"></a>継続的にサイズ変更される Windows フォーム コントロール  
 継続的なスケーリングをサポートする Windows フォーム コントロールと [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] レイアウト システムは完全に対話することができます。 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 要素では、通常どおり、<xref:System.Windows.FrameworkElement.MeasureOverride%2A> および <xref:System.Windows.FrameworkElement.ArrangeOverride%2A> メソッドを使用して、ホストされている Windows フォーム コントロールのサイズを変更し、配置します。  
  
### <a name="sizing-algorithm"></a>サイズ変更アルゴリズム  
 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 要素では、次の手順を使用して、ホストされているコントロールのサイズを変更します。  
  
1. <xref:System.Windows.Forms.Integration.WindowsFormsHost> 要素によって、<xref:System.Windows.FrameworkElement.MeasureOverride%2A> および <xref:System.Windows.FrameworkElement.ArrangeOverride%2A> メソッドがオーバーライドされます。  
  
2. ホストされているコントロールのサイズを決定するために、<xref:System.Windows.FrameworkElement.MeasureOverride%2A> メソッドから、<xref:System.Windows.FrameworkElement.MeasureOverride%2A> メソッドに渡された制約から変換された制約を使用して、ホストされているコントロールの <xref:System.Windows.Forms.Control.GetPreferredSize%2A> メソッドが呼び出されます。  
  
3. <xref:System.Windows.FrameworkElement.ArrangeOverride%2A> メソッドを使用すると、ホストされているコントロールの指定されたサイズ制約への設定が試行されます。  
  
4. ホストされているコントロールの <xref:System.Windows.Forms.Control.Size%2A> プロパティが指定された制約と一致する場合、ホストされているコントロールは制約に合わせてサイズが変更されます。  
  
 <xref:System.Windows.Forms.Control.Size%2A> プロパティが指定された制約と一致しない場合、ホストされているコントロールは連続サイズ変更をサポートしません。 たとえば、<xref:System.Windows.Forms.MonthCalendar> コントロールでは個別のサイズのみが許可されています。 このコントロールに許可されるサイズは、高さと幅の両方の整数 (月数を表します) で構成されます。 このような場合、<xref:System.Windows.Forms.Integration.WindowsFormsHost> 要素は次のように動作します。  
  
- <xref:System.Windows.Forms.Control.Size%2A> プロパティから、指定された制約よりも大きいサイズが返される場合、ホストされているコントロールは <xref:System.Windows.Forms.Integration.WindowsFormsHost> 要素によってクリップされます。 高さと幅は個別に処理されるので、どちらの方向でもホストされているコントロールがクリップされる可能性があります。  
  
- <xref:System.Windows.Forms.Control.Size%2A> プロパティから、指定された制約よりも小さいサイズが返される場合、<xref:System.Windows.Forms.Integration.WindowsFormsHost> ではこのサイズ値を受け入れ、その値は [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] レイアウト システムに返されます。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Forms.Integration.ElementHost>
- <xref:System.Windows.Forms.Integration.WindowsFormsHost>
- [チュートリアル: WPF での Windows フォーム コントロールの配置](walkthrough-arranging-windows-forms-controls-in-wpf.md)
- [WPF での Windows フォーム コントロールの配置のサンプル](https://github.com/microsoft/WPF-Samples/tree/master/Migration%20and%20Interoperability/WpfLayoutHostingWfWithXaml)
- [Windows フォームと WPF プロパティの割り当て](windows-forms-and-wpf-property-mapping.md)
- [移行と相互運用性](migration-and-interoperability.md)
