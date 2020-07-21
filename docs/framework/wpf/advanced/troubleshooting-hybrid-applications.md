---
title: ハイブリッド アプリケーションのトラブルシューティング
ms.date: 03/30/2017
helpviewer_keywords:
- overlapping controls [WPF]
- Windows Forms [WPF], interoperability with
- Windows Forms [WPF], WPF interoperation
- interoperability [WPF], Windows Forms
- hybrid applications [WPF interoperability]
- message loops [WPF]
ms.assetid: f440c23f-fa5d-4d5a-852f-ba61150e6405
ms.openlocfilehash: b85a607d2e44d6253359a81118f90e6ee05d2d3f
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79187323"
---
# <a name="troubleshooting-hybrid-applications"></a>ハイブリッド アプリケーションのトラブルシューティング
<a name="introduction"></a> このトピックでは、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] と Windows フォームの両方のテクノロジを使用してハイブリッド アプリケーションを作成するときに発生する可能性がある一般的な問題について説明します。  

<a name="overlapping_controls"></a>
## <a name="overlapping-controls"></a>コントロールの重複  
 コントロールが、意図したとおりに重ならない場合があります。 Windows フォームでは、コントロールごとに個別の HWND が使用されます。 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] では、ページ上のすべてのコンテンツに対して 1 つの HWND が使用されます。 この実装の違いにより、予期しない重ね合わせ動作が発生します。  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] でホストされている Windows フォーム コントロールは、常に [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] コンテンツの上に表示されます。  
  
 <xref:System.Windows.Forms.Integration.ElementHost> コントロールでホストされている [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] コンテンツは、<xref:System.Windows.Forms.Integration.ElementHost> コントロールの Z オーダーで表示されます。 <xref:System.Windows.Forms.Integration.ElementHost> コントロールを重ねることはできますが、ホストされている [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] コンテンツの結合または対話は行われません。  
  
<a name="child_property"></a>
## <a name="child-property"></a>子プロパティ  
 <xref:System.Windows.Forms.Integration.WindowsFormsHost> クラスと <xref:System.Windows.Forms.Integration.ElementHost> クラスでホストできる子コントロールまたは要素は、1 つだけです。 複数のコントロールまたは要素をホストするには、子コンテンツとしてコンテナーを使用する必要があります。 たとえば、Windows フォームのボタンとチェック ボックス コントロールを <xref:System.Windows.Forms.Panel?displayProperty=nameWithType> コントロールに追加した後、パネルを <xref:System.Windows.Forms.Integration.WindowsFormsHost> コントロールの <xref:System.Windows.Forms.Integration.WindowsFormsHost.Child%2A> プロパティに割り当てます。 ただし、ボタンとチェック ボックス コントロールを、同じ <xref:System.Windows.Forms.Integration.WindowsFormsHost> コントロールに個別に追加することはできません。  
  
<a name="scaling"></a>
## <a name="scaling"></a>スケーリング  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] と Windows フォームではスケーリング モデルが異なります。 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] のスケーリング変換には、Windows フォーム コントロールにとって意味があるものもあれば、そうでないものもあります。 たとえば、Windows フォーム コントロールのスケーリングを 0 に設定した場合は機能しますが、同じコントロールを 0 以外の値にスケーリングして戻そうとしても、コントロールのサイズは 0 のままになります。 詳細については、「[WindowsFormsHost 要素のレイアウトに関する考慮事項](layout-considerations-for-the-windowsformshost-element.md)」を参照してください。  
  
<a name="adapter"></a>
## <a name="adapter"></a>アダプター  
 <xref:System.Windows.Forms.Integration.WindowsFormsHost> クラスと <xref:System.Windows.Forms.Integration.ElementHost> クラスを操作するときは、非表示のコンテナーが含まれているため、混乱が生じる可能性があります。 <xref:System.Windows.Forms.Integration.WindowsFormsHost> クラスと <xref:System.Windows.Forms.Integration.ElementHost> クラスには "*アダプター*" と呼ばれる非表示のコンテナーがあり、コンテンツをホストするために使用されます。 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 要素の場合、アダプターは <xref:System.Windows.Forms.ContainerControl?displayProperty=nameWithType> クラスから派生します。 <xref:System.Windows.Forms.Integration.ElementHost> コントロールの場合、アダプターは <xref:System.Windows.Controls.DockPanel> 要素から派生します。 他の相互運用のトピックでアダプターへの参照が示されている場合は、このコンテナーについて説明されています。  
  
<a name="nesting"></a>
## <a name="nesting"></a>入れ子  
 <xref:System.Windows.Forms.Integration.ElementHost> コントロールの内部に <xref:System.Windows.Forms.Integration.WindowsFormsHost> 要素を入れ子にすることは、サポートされていません。 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 要素の内部に <xref:System.Windows.Forms.Integration.ElementHost> コントロールを入れ子にすることも、サポートされていません。  
  
<a name="focus"></a>
## <a name="focus"></a>フォーカス  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] と Windows フォームではフォーカスの動作が異なるため、ハイブリッド アプリケーションでフォーカスの問題が発生する可能性があります。 たとえば、<xref:System.Windows.Forms.Integration.WindowsFormsHost> 要素の内部にフォーカスがある場合に、ページを最小化してから元に戻したり、モーダル ダイアログ ボックスを表示したりすると、<xref:System.Windows.Forms.Integration.WindowsFormsHost> 要素内のフォーカスが失われる可能性があります。 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 要素にはまだフォーカスがありますが、その中のコントロールにはフォーカスがない可能性があります。  
  
 データの検証も、フォーカスによって影響を受けます。 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 要素内では検証は機能しますが、Tab キーを使用して <xref:System.Windows.Forms.Integration.WindowsFormsHost> 要素の外に移動したり、2 つの異なる <xref:System.Windows.Forms.Integration.WindowsFormsHost> 要素間で移動したりすると、検証は機能しません。  
  
<a name="property_mapping"></a>
## <a name="property-mapping"></a>プロパティ マッピング  
 一部のプロパティ マッピングでは、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] と Windows フォームのテクノロジの間で異なる実装をブリッジするために広範な解釈が必要です。 プロパティ マッピングを使用すると、フォント、色、その他のプロパティの変更にコードで対応することができます。 一般に、プロパティ マッピングは、*Property*Changed イベントまたは On*Property*Changed の呼び出しをリッスンし、子コントロールまたはそのアダプターで適切なプロパティを設定することによって機能します。 詳細については、「[Windows フォームと WPF のプロパティ マッピング](windows-forms-and-wpf-property-mapping.md)」を参照してください。  
  
<a name="layoutrelated_properties_on_hosted_content"></a>
## <a name="layout-related-properties-on-hosted-content"></a>ホストされているコンテンツでのレイアウト関連のプロパティ  
 <xref:System.Windows.Forms.Integration.WindowsFormsHost.Child%2A?displayProperty=nameWithType> プロパティまたは <xref:System.Windows.Forms.Integration.ElementHost.Child%2A?displayProperty=nameWithType> プロパティを割り当てると、ホストされているコンテンツでいくつかのレイアウト関連のプロパティが自動的に設定されます。 これらのコンテンツ プロパティを変更すると、予期しないレイアウト動作が発生する可能性があります。  
  
 ホストされているコンテンツは、<xref:System.Windows.Forms.Integration.WindowsFormsHost> と <xref:System.Windows.Forms.Integration.ElementHost> の親を埋めるようにドッキングされます。 この埋め込み動作を有効にするため、子プロパティを設定すると、いくつかのプロパティが設定されます。 次の表に、<xref:System.Windows.Forms.Integration.ElementHost> クラスと <xref:System.Windows.Forms.Integration.WindowsFormsHost> クラスによって設定されるコンテンツ プロパティを示します。  
  
|ホスト クラス|コンテンツ プロパティ|  
|----------------|------------------------|  
|<xref:System.Windows.Forms.Integration.ElementHost>|<xref:System.Windows.FrameworkElement.Height%2A><br /><br /> <xref:System.Windows.FrameworkElement.Width%2A><br /><br /> <xref:System.Windows.FrameworkElement.Margin%2A><br /><br /> <xref:System.Windows.FrameworkElement.VerticalAlignment%2A><br /><br /> <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A>|  
|<xref:System.Windows.Forms.Integration.WindowsFormsHost>|<xref:System.Windows.Forms.Control.Margin%2A><br /><br /> <xref:System.Windows.Forms.Control.Dock%2A><br /><br /> <xref:System.Windows.Forms.Control.AutoSize%2A><br /><br /> <xref:System.Windows.Forms.Control.Location%2A><br /><br /> <xref:System.Windows.Forms.Control.MaximumSize%2A>|  
  
 ホストされているコンテンツでこれらのプロパティを直接設定しないでください。 詳細については、「[WindowsFormsHost 要素のレイアウトに関する考慮事項](layout-considerations-for-the-windowsformshost-element.md)」を参照してください。  
  
<a name="navigation_applications"></a>
## <a name="navigation-applications"></a>ナビゲーション アプリケーション  
 ナビゲーション アプリケーションでは、ユーザーの状態が維持されない場合があります。 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 要素がナビゲーション アプリケーションで使用されると、要素のコントロールが再作成されます。 子コントロールの再作成は、ユーザーが <xref:System.Windows.Forms.Integration.WindowsFormsHost> 要素をホストしているページから移動し、後でそれに戻ると行われます。 ユーザーによって入力された内容はすべて失われます。  
  
<a name="message_loop_interoperation"></a>
## <a name="message-loop-interoperation"></a>メッセージループの相互動作  
 Windows フォーム メッセージのループを使用すると、メッセージが意図したとおりに処理されない可能性があります。 <xref:System.Windows.Forms.Integration.WindowsFormsHost.EnableWindowsFormsInterop%2A> メソッドは、<xref:System.Windows.Forms.Integration.WindowsFormsHost> コンストラクターによって呼び出されます。 このメソッドにより、メッセージ フィルターが [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] メッセージ ループに追加されます。 メッセージのターゲットになっていた <xref:System.Windows.Forms.Control?displayProperty=nameWithType> によってメッセージが変換およびディスパッチされる場合、このフィルターでは <xref:System.Windows.Forms.Control.PreProcessMessage%2A?displayProperty=nameWithType> メソッドが呼び出されます。  
  
 <xref:System.Windows.Forms.Application.Run%2A?displayProperty=nameWithType> が設定された Windows フォーム メッセージ ループで <xref:System.Windows.Window> が表示される場合、<xref:System.Windows.Forms.Integration.ElementHost.EnableModelessKeyboardInterop%2A> メソッドを呼び出さないと、何も入力できません。 <xref:System.Windows.Forms.Integration.ElementHost.EnableModelessKeyboardInterop%2A> メソッドは、<xref:System.Windows.Window> を受け取り、<xref:System.Windows.Forms.IMessageFilter?displayProperty=nameWithType> を追加します。これにより、キー関連のメッセージが [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] メッセージ ループに再ルーティングされます。 詳細については、「[Windows フォームと WPF の相互運用性入力アーキテクチャ](windows-forms-and-wpf-interoperability-input-architecture.md)」を参照してください。  
  
<a name="opacity_and_layering"></a>
## <a name="opacity-and-layering"></a>不透明度とレイヤー化  
 <xref:System.Windows.Interop.HwndHost> クラスでは、レイヤー化はサポートされていません。 つまり、<xref:System.Windows.Forms.Integration.WindowsFormsHost> 要素で <xref:System.Windows.UIElement.Opacity%2A> プロパティを設定しても何も効果はなく、<xref:System.Windows.Window.AllowsTransparency%2A> が `true` に設定されている他の [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] ウィンドウとのブレンドは行われません。  
  
<a name="dispose"></a>
## <a name="dispose"></a>Dispose  
 クラスを正しく破棄しないと、リソースがリークする可能性があります。 ハイブリッド アプリケーションでは、<xref:System.Windows.Forms.Integration.WindowsFormsHost> クラスと <xref:System.Windows.Forms.Integration.ElementHost> クラスを破棄する必要があります。そうしないと、リソースがリークする可能性があります。 Windows フォームの <xref:System.Windows.Forms.Integration.ElementHost> コントロールは、その非モーダルの親 <xref:System.Windows.Forms.Form> が閉じると破棄されます。 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] では、アプリケーションがシャットダウンされると <xref:System.Windows.Forms.Integration.WindowsFormsHost> 要素が破棄されます。 Windows フォームのメッセージ ループ内で <xref:System.Windows.Window> の <xref:System.Windows.Forms.Integration.WindowsFormsHost> 要素を表示することができます。 この場合、アプリケーションがシャットダウンしているという通知をコードで受信できないことがあります。  
  
<a name="enabling_visual_styles"></a>
## <a name="enabling-visual-styles"></a>視覚スタイルを有効にする  
 Windows フォーム コントロールの Microsoft Windows XP ビジュアル スタイルが有効にされない可能性があります。 Windows フォーム アプリケーションのテンプレートでは、<xref:System.Windows.Forms.Application.EnableVisualStyles%2A?displayProperty=nameWithType> メソッドが呼び出されます。 このメソッドは既定では呼び出されませんが、Visual Studio を使用してプロジェクトを作成した場合で、Comctl32.dll のバージョン 6.0 が使用可能な場合は、Microsoft Windows XP ビジュアル スタイルのコントロールが表示されます。 スレッドでハンドルが作成される前に、<xref:System.Windows.Forms.Application.EnableVisualStyles%2A> メソッドを呼び出す必要があります。 詳細については、「[方法: ハイブリッド アプリケーションで視覚スタイルを有効にする](how-to-enable-visual-styles-in-a-hybrid-application.md)」を参照してください。  
  
<a name="licensed_controls"></a>
## <a name="licensed-controls"></a>ライセンスされたコントロール  
 ライセンスされた Windows フォーム コントロールで、ユーザーに対してメッセージ ボックスにライセンス情報が表示されると、ハイブリッド アプリケーションで予期しない動作が発生する可能性があります。 一部のライセンスされたコントロールでは、ハンドルの作成に対してダイアログ ボックスが表示されます。 たとえば、ライセンスされたコントロールでは、ライセンスが必要である、またはユーザーが使用できる試用版コントロールがあと 3 つである、といったことがユーザーに通知される場合があります。  
  
 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 要素は <xref:System.Windows.Interop.HwndHost> クラスから派生し、子コントロールのハンドルは <xref:System.Windows.Forms.Integration.WindowsFormsHost.BuildWindowCore%2A> メソッド内で作成されます。 <xref:System.Windows.Interop.HwndHost> クラスでは、<xref:System.Windows.Forms.Integration.WindowsFormsHost.BuildWindowCore%2A> メソッドでメッセージを処理することはできませんが、ダイアログ ボックスを表示するとメッセージが送信されます。 このライセンス シナリオを有効にするには、コントロールで <xref:System.Windows.Forms.Control.CreateControl%2A?displayProperty=nameWithType> メソッドを呼び出してから、そのコントロールを <xref:System.Windows.Forms.Integration.WindowsFormsHost> 要素の子として割り当てます。  
  
<a name="wpf_designer"></a>
## <a name="wpf-designer"></a>WPF デザイナー  
 WPF コンテンツをデザインするには、Visual Studio 用の WPF デザイナーを使用します。 次のセクションでは、WPF デザイナーを使用してハイブリッド アプリケーションを作成するときに発生する可能性がある一般的な問題について説明します。  
  
### <a name="backcolortransparent-is-ignored-at-design-time"></a>BackColorTransparent がデザイン時には無視される  
 <xref:System.Windows.Forms.Integration.ElementHost.BackColorTransparent%2A> プロパティは、デザイン時に予期したとおりに動作しない可能性があります。  
  
 WPF コントロールが表示される親の上にない場合、WPF ランタイムでは <xref:System.Windows.Forms.Integration.ElementHost.BackColorTransparent%2A> の値が無視されます。 <xref:System.Windows.Forms.Integration.ElementHost.BackColorTransparent%2A> が無視される可能性がある理由は、<xref:System.Windows.Forms.Integration.ElementHost> オブジェクトが別の <xref:System.AppDomain> に作成されるためです。 ただし、アプリケーションを実行すると、<xref:System.Windows.Forms.Integration.ElementHost.BackColorTransparent%2A> は想定どおりに動作します。  
  
### <a name="design-time-error-list-appears-when-the-obj-folder-is-deleted"></a>obj フォルダーが削除されるとデザイン時のエラー一覧が表示される  
 obj フォルダーが削除されると、デザイン時のエラー一覧が表示されます。  
  
 <xref:System.Windows.Forms.Integration.ElementHost> を使用してデザインするとき、Windows フォーム デザイナーでは、プロジェクトの obj フォルダー内の Debug フォルダーまたは Release フォルダーに生成されたファイルが使用されます。 これらのファイルを削除すると、デザイン時のエラー一覧が表示されます。 この問題を解決するには、プロジェクトをリビルドします。 詳細については、「[Windows フォーム デザイナーでのデザイン時エラー](../../winforms/controls/design-time-errors-in-the-windows-forms-designer.md)」を参照してください。  
  
<a name="elementhost_and_ime"></a>
## <a name="elementhost-and-ime"></a>ElementHost と IME  
 現在、<xref:System.Windows.Forms.Integration.ElementHost> でホストされている WPF コントロールでは、<xref:System.Windows.Forms.Control.ImeMode%2A> プロパティはサポートされていません。 <xref:System.Windows.Forms.Control.ImeMode%2A> に対する変更は、ホストされているコントロールによって無視されます。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Forms.Integration.ElementHost>
- <xref:System.Windows.Forms.Integration.WindowsFormsHost>
- [WPF デザイナーでの相互運用性](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/bb628658(v=vs.100))
- [Windows フォームと WPF の相互運用性入力アーキテクチャ](windows-forms-and-wpf-interoperability-input-architecture.md)
- [方法: ハイブリッド アプリケーションで視覚スタイルを有効にする](how-to-enable-visual-styles-in-a-hybrid-application.md)
- [WindowsFormsHost 要素のレイアウトに関する考慮事項](layout-considerations-for-the-windowsformshost-element.md)
- [Windows フォームと WPF プロパティの割り当て](windows-forms-and-wpf-property-mapping.md)
- [Windows フォーム デザイナーでのデザイン時エラー](../../winforms/controls/design-time-errors-in-the-windows-forms-designer.md)
- [移行と相互運用性](migration-and-interoperability.md)
