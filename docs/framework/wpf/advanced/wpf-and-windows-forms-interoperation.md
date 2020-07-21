---
title: WPF と Windows フォームの相互運用性
titleSuffix: ''
ms.date: 03/30/2017
helpviewer_keywords:
- Windows Forms [WPF], interoperability with
- nester interoperation [WPF]
- Windows Forms [WPF], WPF interoperation
- interoperability [WPF], Windows Forms
- hybrid control [WPF interoperability]
ms.assetid: 9e8aa6b6-112c-4579-98d1-c974917df499
ms.openlocfilehash: 76d1e97c92946267aa1217f52c93594fb63d20de
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79187150"
---
# <a name="wpf-and-windows-forms-interoperation"></a>WPF と Windows フォームの相互運用性
[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] と Windows フォームでは、アプリケーション インターフェイスの作成に対して 2 つの異なるアーキテクチャが提供されています。 <xref:System.Windows.Forms.Integration?displayProperty=nameWithType> 名前空間では、一般的な相互運用シナリオを可能にするクラスが提供されています。 相互運用機能を実装する 2 つの主要なクラスは、<xref:System.Windows.Forms.Integration.WindowsFormsHost> と <xref:System.Windows.Forms.Integration.ElementHost> です。 このトピックでは、サポートされている相互運用シナリオとサポートされていないシナリオについて説明します。  
  
> [!NOTE]
> "*ハイブリッド コントロール*" のシナリオについては、特別な考慮事項があります。 ハイブリッド コントロールでは、あるテクノロジのコントロールが他のテクノロジのコントロールに入れ子になっています。 これは、"*入れ子になった相互運用*" とも呼ばれます。 "*マルチレベル ハイブリッド コントロール*" では、複数のレベルのハイブリッド コントロールが入れ子になっています。 マルチレベルの入れ子になった相互運用の例は、Windows フォーム コントロールに [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] コントロールが含まれ、それに別の Windows フォーム コントロールが含まれているような場合です。 マルチレベル ハイブリッド コントロールはサポートされていません。  

<a name="Windows_Presentation_Foundation_Application_Hosting"></a>
## <a name="hosting-windows-forms-controls-in-wpf"></a>WPF での Windows フォーム コントロールのホスティング  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] コントロールで Windows フォーム コントロールがホストされている場合は、次の相互運用シナリオがサポートされます。  
  
- [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] コントロールでは、XAML を使用して 1 つ以上の Windows フォーム コントロールをホストできます。  
  
- コード を使用して 1 つ以上の Windows フォーム コントロールをホストできます。  
  
- 他の Windows フォーム コントロールが含まれる Windows フォーム コンテナー コントロールをホストできます。  
  
- [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] をマスター、Windows フォームを詳細にして、マスターと詳細フォームをホストできます。  
  
- Windows フォームをマスター、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] を詳細にして、マスターと詳細フォームをホストできます。  
  
- 1 つ以上の ActiveX コントロールをホストできます。  
  
- 1 つ以上の複合コントロールをホストできます。  
  
- [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] を使用してハイブリッド コントロールをホストできます。  
  
- コードを使用してハイブリッド コントロールをホストできます。  
  
### <a name="layout-support"></a>レイアウトのサポート  
 次の一覧では、<xref:System.Windows.Forms.Integration.WindowsFormsHost> 要素を使用して、ホストされている Windows フォーム コントロールを [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] レイアウト システムに統合しようとした場合の、既知の制限事項について説明します。  
  
- 場合によっては、Windows フォーム コントロールのサイズを変更できません。または、特定のサイズにしか限定できません。 たとえば、Windows フォームの <xref:System.Windows.Forms.ComboBox> コントロールでは、コントロールのフォント サイズによって定義される 1 つの高さのみがサポートされます。 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] の動的レイアウトでは、要素を垂直方向に伸縮できるものと想定されていますが、ホストされている <xref:System.Windows.Forms.ComboBox> コントロールは想定したとおりに伸縮されません。  
  
- Windows フォーム コントロールを回転または傾斜させることはできません。 たとえば、ユーザー インターフェイスを 90 度回転させても、ホストされている Windows フォーム コントロールは縦向きのままになります。  
  
- ほとんどの場合、Windows フォーム コントロールでは比率を維持したスケーリングはサポートされていません。 コントロール全体の寸法はスケーリングされますが、コントロールの子コントロールとコンポーネント要素は、想定したとおりにサイズ変更されない可能性があります。 この制限は、各 Windows フォーム コントロールでスケーリングがどの程度サポートされているかによって異なります。  
  
- [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] のユーザー インターフェイスでは、要素の Z オーダーを変更して、重なり具合を制御できます。 ホストされている Windows フォーム コントロールは別の HWND で描画されるため、常に [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 要素の上に描画されます。  
  
- Windows フォーム コントロールでは、フォント サイズに基づく自動スケーリングがサポートされています。 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] のユーザー インターフェイスでは、フォント サイズを変更してもレイアウト全体のサイズは変更されませんが、個々の要素のサイズは動的に変更される可能性があります。  
  
### <a name="ambient-properties"></a>アンビエント プロパティ  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] のコントロールの一部のアンビエント プロパティには、Windows フォームにそれに対応するものがあります。 これらのアンビエント プロパティは、ホストされている Windows フォーム コントロールに反映され、<xref:System.Windows.Forms.Integration.WindowsFormsHost> コントロールのパブリック プロパティとして公開されます。 <xref:System.Windows.Forms.Integration.WindowsFormsHost> コントロールでは、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] の各アンビエント プロパティが Windows フォームでのそれと同等のプロパティに変換されます。  
  
 詳細については、「[Windows フォームと WPF のプロパティ マッピング](windows-forms-and-wpf-property-mapping.md)」を参照してください。  
  
### <a name="behavior"></a>動作  
 次の表では、相互運用動作について説明します。  
  
|動作|サポート状況|サポートなし|  
|--------------|---------------|-------------------|  
|[透明度]|Windows フォーム コントロールのレンダリングでは、透明度がサポートされています。 親の [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] コントロールの背景を、ホストされている Windows フォーム コントロールの背景にすることができます。|一部の Windows フォーム コントロールでは、透明度がサポートされていません。 たとえば、<xref:System.Windows.Forms.TextBox> コントロールや <xref:System.Windows.Forms.ComboBox> コントロールは、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] でホストされているときは透明になりません。|  
|タブ移動|ホストされている Windows フォーム コントロールのタブ オーダーは、それらのコントロールが Windows フォーム ベースのアプリケーションでホストされている場合と同じです。<br /><br /> Tab キーと Shift + Tab キーによる [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] コントロールから Windows フォーム コントロールへの Tab 移動は、通常どおりに動作します。<br /><br /> <xref:System.Windows.Forms.Control.TabStop%2A> プロパティの値が `false` である Windows フォーム コントロールは、ユーザーがコントロールをタブ移動したときにフォーカスを受け取りません。<br /><br /> - 各 <xref:System.Windows.Forms.Integration.WindowsFormsHost> コントロールには <xref:System.Windows.Forms.Integration.WindowsFormsHost.TabIndex%2A> 値があり、それによって <xref:System.Windows.Forms.Integration.WindowsFormsHost> コントロールがいつフォーカスを受け取るかが決定されます。<br />- <xref:System.Windows.Forms.Integration.WindowsFormsHost> コンテナー内に含まれる Windows フォーム コントロールは、<xref:System.Windows.Forms.Control.TabIndex%2A> プロパティによって指定されている順序に従います。 最後のタブ インデックスからタブ移動すると、次の [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] コントロールにフォーカスが移動します (存在する場合)。 フォーカスを設定できる [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] コントロールが他に存在しない場合は、タブ オーダーで先頭の Windows フォーム コントロールに戻ります。<br />-   <xref:System.Windows.Forms.Integration.WindowsFormsHost> の内部にあるコントロールの <xref:System.Windows.Forms.Integration.WindowsFormsHost.TabIndex%2A> の値は、<xref:System.Windows.Forms.Integration.WindowsFormsHost> コントロールに含まれる兄弟 Windows フォーム コントロールに対して相対的です。<br />- タブ移動よりコントロール固有の動作が優先されます。 たとえば、<xref:System.Windows.Forms.TextBoxBase.AcceptsTab%2A> プロパティの値が `true` である <xref:System.Windows.Forms.TextBox> コントロールで Tab キーを押すと、フォーカスが移動するのではなく、テキスト ボックス内にタブが入ります。|該当なし。|  
|方向キーによるナビゲーション|- <xref:System.Windows.Forms.Integration.WindowsFormsHost> コントロールでの方向キーによるナビゲーションは、通常の Windows フォーム コンテナー コントロールと同じです。上方向キーと左方向キーでは前のコントロールが選択され、下方向キーと右方向キーでは次のコントロールが選択されます。<br />- <xref:System.Windows.Forms.Integration.WindowsFormsHost> コントロールに含まれる最初のコントロールで上方向キーまたは左方向キーを押すと、Shift + Tab キーボード ショートカットと同じ操作が実行されます。 フォーカスを設定できる [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] コントロールがある場合、フォーカスは <xref:System.Windows.Forms.Integration.WindowsFormsHost> コントロールの外に移動します。 この動作は、最後のコントロールへのラップが行われないという点で、<xref:System.Windows.Forms.ContainerControl> の標準動作とは異なります。 フォーカスを設定できる [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] コントロールが他に存在しない場合は、タブ オーダーで最後の Windows フォーム コントロールにフォーカスが戻ります。<br />- <xref:System.Windows.Forms.Integration.WindowsFormsHost> コントロールに含まれる最後のコントロールで下方向キーまたは右方向キーを押すと、Tab キーと同じ操作が実行されます。 フォーカスを設定できる [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] コントロールがある場合、フォーカスは <xref:System.Windows.Forms.Integration.WindowsFormsHost> コントロールの外に移動します。 この動作は、最初のコントロールへのラップが行われないという点で、<xref:System.Windows.Forms.ContainerControl> の標準動作とは異なります。 フォーカスを設定できる [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] コントロールが他に存在しない場合は、タブ オーダーで最初の Windows フォーム コントロールにフォーカスが戻ります。|該当なし。|  
|アクセラレータ|アクセラレータは、"サポートされていない" 列に記載されていることを除き、通常どおりに動作します。|テクノロジをまたぐ重複するアクセラレータは、通常の重複するアクセラレータと同じようには機能しません。 テクノロジをまたいでアクセラレータが重複すると (少なくとも 1 つが Windows フォーム コントロール上にあり、他が [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] コントロール上にある場合)、Windows フォーム コントロールが常にアクセラレータを受け取ります。 重複するアクセラレータが押された場合、コントロールの間でフォーカスが切り替えられることはありません。|  
|ショートカット キー|ショートカット キーは、"サポートされていない" 列に記載されていることを除き、通常どおりに動作します。|- 前処理ステージで処理される Windows フォームのショートカット キーは、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] のショートカット キーより常に優先されます。 たとえば、Ctrl + S ショートカット キーが定義されている <xref:System.Windows.Forms.ToolStrip> コントロールがあり、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] に Ctrl + S にバインドされたコマンドがある場合、フォーカスに関係なく、<xref:System.Windows.Forms.ToolStrip> コントロールのハンドラーが常に最初に呼び出されます。<br />- <xref:System.Windows.Forms.Control.KeyDown> イベントによって処理される Windows フォームのショートカット キーは、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] で最後に処理されます。 Windows フォーム コントロールの <xref:System.Windows.Forms.Control.IsInputKey%2A> メソッドをオーバーライドするか、<xref:System.Windows.Forms.Control.PreviewKeyDown> イベントを処理することで、この動作を回避できます。 <xref:System.Windows.Forms.Control.IsInputKey%2A> メソッドから `true` を返すか、または <xref:System.Windows.Forms.Control.PreviewKeyDown> のイベント ハンドラーで <xref:System.Windows.Forms.PreviewKeyDownEventArgs.IsInputKey%2A?displayProperty=nameWithType> プロパティの値を `true` に設定します。|  
|AcceptsReturn、AcceptsTab、およびその他のコントロール固有の動作|Windows フォーム コントロールで <xref:System.Windows.Forms.Control.IsInputKey%2A> メソッドが `true` を返すようにオーバーライドされていれば、既定のキーボード動作を変更するプロパティは通常どおり動作します。|<xref:System.Windows.Forms.Control.KeyDown> イベントを処理することによって既定のキーボード動作を変更する Windows フォーム コントロールは、ホスト [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] コントロールで最後に処理されます。 これらのコントロールは最後に処理されるため、予期しない動作が発生する可能性があります。|  
|Enter イベントと Leave イベント|外側の <xref:System.Windows.Forms.Integration.ElementHost> コントロールにフォーカスが移動しない場合、1 つの <xref:System.Windows.Forms.Integration.WindowsFormsHost> コントロール内でフォーカスが変化すると、Enter イベントと Leave イベントが通常どおりに発生します。|次のようなフォーカスの変化が発生すると、Enter イベントと Leave イベントは発生しません。<br /><br /> - <xref:System.Windows.Forms.Integration.WindowsFormsHost> コントロールの内側から外側へ。<br />- <xref:System.Windows.Forms.Integration.WindowsFormsHost> コントロールの外側から内側へ。<br />- <xref:System.Windows.Forms.Integration.WindowsFormsHost> コントロールの外側。<br />- <xref:System.Windows.Forms.Integration.WindowsFormsHost> コントロールでホストされている Windows フォーム コントロールから、同じ <xref:System.Windows.Forms.Integration.WindowsFormsHost> の内側でホストされている <xref:System.Windows.Forms.Integration.ElementHost> コントロールへ。|  
|マルチスレッド|マルチスレッドのすべてのバリエーションがサポートされています。|Windows フォームと [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] の両方のテクノロジで、シングルスレッドのコンカレンシー モデルが想定されています。 デバッグ中に、他のスレッドからフレームワーク オブジェクトを呼び出すと、例外が発生し、この要件が適用されます。|  
|セキュリティ|すべての相互運用シナリオでは、完全な信頼が必要です。|部分的な信頼では、相互運用シナリオは許可されません。|  
|ユーザー補助|すべてのアクセシビリティ シナリオがサポートされています。 支援技術製品は、Windows フォームと [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] の両方のコントロールを含むハイブリッド アプリケーションで使用されたときも、正しく機能します。|該当なし。|  
|クリップボードのトピック|すべてのクリップボード操作は通常どおりに動作します。 これには、Windows フォーム コントロールと [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] コントロールの間でのカット アンド ペーストが含まれます。|該当なし。|  
|ドラッグ アンド ドロップ機能|すべてのドラッグ アンド ドロップ操作は通常どおりに動作します。 これには、Windows フォーム コントロールと [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] コントロールの間での操作が含まれます。|該当なし。|  
  
<a name="Windows_Forms_Application_Hosting_Windows"></a>
## <a name="hosting-wpf-controls-in-windows-forms"></a>Windows フォームでの WPF コントロールのホスト  
 Windows フォーム コントロールで [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] コントロールがホストされている場合は、次の相互運用シナリオがサポートされます。  
  
- コードを使用した 1 つ以上の [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] コントロールのホスト。  
  
- プロパティ シートと 1 つ以上のホストされている [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] コントロールの関連付け。  
  
- フォームでの 1 つ以上の [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] ページのホスト。  
  
- [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] ウィンドウの開始。  
  
- Windows フォームをマスター、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] を詳細とする、マスターと詳細フォームのホスト。  
  
- [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] をマスター、Windows フォームを詳細とする、マスターと詳細フォームのホスト。  
  
- カスタム [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] コントロールのホスト。  
  
- ハイブリッド コントロールのホスト。  
  
### <a name="ambient-properties"></a>アンビエント プロパティ  
 Windows フォーム コントロールの一部のアンビエント プロパティには、対応するものが [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] にあります。 これらのアンビエント プロパティは、ホストされている [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] コントロールに反映され、<xref:System.Windows.Forms.Integration.ElementHost> コントロールのパブリック プロパティとして公開されます。 <xref:System.Windows.Forms.Integration.ElementHost> コントロールでは、Windows フォームの各アンビエント プロパティが [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] でのそれと同等のプロパティに変換されます。  
  
 詳細については、「[Windows フォームと WPF のプロパティ マッピング](windows-forms-and-wpf-property-mapping.md)」を参照してください。  
  
### <a name="behavior"></a>動作  
 次の表では、相互運用動作について説明します。  
  
|動作|サポート状況|サポートなし|  
|--------------|---------------|-------------------|  
|[透明度]|[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] コントロールのレンダリングでは、透明度がサポートされています。 親の Windows フォーム コントロールの背景を、ホストされている [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] コントロールの背景にすることができます。|該当なし。|  
|マルチスレッド|マルチスレッドのすべてのバリエーションがサポートされています。|Windows フォームと [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] の両方のテクノロジで、シングルスレッドのコンカレンシー モデルが想定されています。 デバッグ中に、他のスレッドからフレームワーク オブジェクトを呼び出すと、例外が発生し、この要件が適用されます。|  
|セキュリティ|すべての相互運用シナリオでは、完全な信頼が必要です。|部分的な信頼では、相互運用シナリオは許可されません。|  
|ユーザー補助|すべてのアクセシビリティ シナリオがサポートされています。 支援技術製品は、Windows フォームと [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] の両方のコントロールを含むハイブリッド アプリケーションで使用されたときも、正しく機能します。|該当なし。|  
|クリップボードのトピック|すべてのクリップボード操作は通常どおりに動作します。 これには、Windows フォーム コントロールと [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] コントロールの間でのカット アンド ペーストが含まれます。|該当なし。|  
|ドラッグ アンド ドロップ機能|すべてのドラッグ アンド ドロップ操作は通常どおりに動作します。 これには、Windows フォーム コントロールと [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] コントロールの間での操作が含まれます。|該当なし。|  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Forms.Integration.ElementHost>
- <xref:System.Windows.Forms.Integration.WindowsFormsHost>
- [チュートリアル: WPF での Windows フォーム コントロールのホスト](walkthrough-hosting-a-windows-forms-control-in-wpf.md)
- [チュートリアル: WPF での Windows フォーム複合コントロールのホスト](walkthrough-hosting-a-windows-forms-composite-control-in-wpf.md)
- [チュートリアル: Windows フォームでの WPF 複合コントロールのホスト](walkthrough-hosting-a-wpf-composite-control-in-windows-forms.md)
- [Windows フォームと WPF プロパティの割り当て](windows-forms-and-wpf-property-mapping.md)
