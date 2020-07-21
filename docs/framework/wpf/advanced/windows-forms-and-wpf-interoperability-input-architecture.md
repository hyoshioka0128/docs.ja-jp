---
title: Windows フォームと WPF 相互運用性入力アーキテクチャ
titleSuffix: ''
ms.date: 03/30/2017
helpviewer_keywords:
- input architecture [WPF interoperability]
- messages [WPF]
- Windows Forms [WPF], interoperability with
- Windows Forms [WPF], WPF interoperation
- interoperability [WPF], Windows Forms
- modeless forms [WPF]
- ElementHost keyboard and messages [WPF]
- keyboard interoperation [WPF]
- WindowsFormsHost keyboard and messages [WPF]
- modeless dialog boxes [WPF]
ms.assetid: 0eb6f137-f088-4c5e-9e37-f96afd28f235
ms.openlocfilehash: 1c7027947d24c847ee298022344e02ce0bbff764
ms.sourcegitcommit: 13e79efdbd589cad6b1de634f5d6b1262b12ab01
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/28/2020
ms.locfileid: "76794090"
---
# <a name="windows-forms-and-wpf-interoperability-input-architecture"></a>Windows フォームと WPF の相互運用性入力アーキテクチャ
[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] と Windows フォーム間の相互運用には、両方のテクノロジに適切なキーボード入力処理が必要です。 このトピックでは、これらのテクノロジでどのようにキーボードおよびメッセージ処理を実装し、ハイブリッド アプリケーションでスムーズな相互運用を可能にする方法について説明します。  
  
 このトピックは、次の内容で構成されています。  
  
- モードレス フォームとダイアログ ボックス  
  
- WindowsFormsHost のキーボードとメッセージの処理  
  
- ElementHost のキーボードとメッセージの処理  
  
## <a name="modeless-forms-and-dialog-boxes"></a>モードレス フォームとダイアログ ボックス  
 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 要素に対して <xref:System.Windows.Forms.Integration.WindowsFormsHost.EnableWindowsFormsInterop%2A> メソッドを呼び出して、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] ベースのアプリケーションからモードレス フォームまたはダイアログ ボックスを開きます。  
  
 <xref:System.Windows.Forms.Integration.ElementHost> コントロールに対して <xref:System.Windows.Forms.Integration.ElementHost.EnableModelessKeyboardInterop%2A> メソッドを呼び出して、Windows フォーム ベースのアプリケーションでモードレス [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] ページを開きます。  
  
## <a name="windowsformshost-keyboard-and-message-processing"></a>WindowsFormsHost のキーボードとメッセージの処理  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] ベースのアプリケーションでホストされている場合、Windows フォームのキーボードとメッセージの処理は以下で構成されます。  
  
- <xref:System.Windows.Forms.Integration.WindowsFormsHost> クラスでは、<xref:System.Windows.Interop.ComponentDispatcher> クラスによって実装されている [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] メッセージ ループからメッセージを取得します。  
  
- <xref:System.Windows.Forms.Integration.WindowsFormsHost> クラスでは、サロゲート Windows フォーム メッセージ ループを作成し、通常の Windows フォーム キーボード処理が確実に行われるようにします。  
  
- <xref:System.Windows.Forms.Integration.WindowsFormsHost> クラスでは、<xref:System.Windows.Interop.IKeyboardInputSink> インターフェイスを実装し、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] を使用してフォーカス管理を調整します。  
  
- <xref:System.Windows.Forms.Integration.WindowsFormsHost> コントロールでは、自身を登録し、メッセージ ループを開始します。  
  
 以下のセクションでは、プロセスのこれらの部分について詳しく説明します。  
  
### <a name="acquiring-messages-from-the-wpf-message-loop"></a>WPF メッセージ ループからのメッセージの取得  
 <xref:System.Windows.Interop.ComponentDispatcher> クラスでは、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] のメッセージ ループ マネージャーを実装します。 <xref:System.Windows.Interop.ComponentDispatcher> クラスには、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] による処理前に外部クライアントでメッセージをフィルター処理できるようになるフックが用意されています。  
  
 相互運用の実装では <xref:System.Windows.Interop.ComponentDispatcher.ThreadFilterMessage?displayProperty=nameWithType> イベントを処理します。これにより、Windows フォーム コントロールで [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] コントロールの前にメッセージを処理できるようになります。  
  
### <a name="surrogate-windows-forms-message-loop"></a>サロゲート Windows フォーム メッセージ ループ  
 既定で、<xref:System.Windows.Forms.Application?displayProperty=nameWithType> クラスには Windows フォーム アプリケーションのプライマリ メッセージ ループが含まれています。 相互運用中、Windows フォーム メッセージ ループによってメッセージは処理されません。 そのため、このロジックを再現する必要があります。 <xref:System.Windows.Interop.ComponentDispatcher.ThreadFilterMessage?displayProperty=nameWithType> イベントのハンドラーでは、以下の手順が実行されます。  
  
1. <xref:System.Windows.Forms.IMessageFilter> インターフェイスを使用してメッセージをフィルター処理します。  
  
2. <xref:System.Windows.Forms.Control.PreProcessMessage%2A?displayProperty=nameWithType> メソッドを呼び出します。  
  
3. 必要に応じて、メッセージを変換してディスパッチします。  
  
4. 他のコントロールでメッセージが処理されない場合、メッセージをホスティング コントロールに渡します。  
  
### <a name="ikeyboardinputsink-implementation"></a>IKeyboardInputSink の実装  
 サロゲート メッセージ ループでは、キーボード管理を処理します。 そのため、<xref:System.Windows.Interop.IKeyboardInputSink.TabInto%2A?displayProperty=nameWithType> メソッドは、<xref:System.Windows.Forms.Integration.WindowsFormsHost> クラスでの実装を必要とする唯一の <xref:System.Windows.Interop.IKeyboardInputSink> メンバーです。  
  
 既定では、<xref:System.Windows.Interop.HwndHost> クラスから、その <xref:System.Windows.Interop.HwndHost.System%23Windows%23Interop%23IKeyboardInputSink%23TabInto%2A> 実装に対して `false` が返されます。 これにより、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] コントロールから Windows フォーム コントロールにタブ移動できなくなります。  
  
 <xref:System.Windows.Interop.IKeyboardInputSink.TabInto%2A?displayProperty=nameWithType> メソッドの <xref:System.Windows.Forms.Integration.WindowsFormsHost> の実装では、次の手順を実行します。  
  
1. <xref:System.Windows.Forms.Integration.WindowsFormsHost> コントロールに含まれ、フォーカスを受け取ることができる最初または最後の Windows フォーム コントロールを見つけます。 コントロールの選択は、走査情報によって変わります。  
  
2. コントロールにフォーカスを設定し、`true` を返します。  
  
3. コントロールがフォーカスを受け取ることができない場合は、`false` を返します。  
  
### <a name="windowsformshost-registration"></a>WindowsFormsHost の登録  
 <xref:System.Windows.Forms.Integration.WindowsFormsHost> コントロールへのウィンドウ ハンドルが作成されると、<xref:System.Windows.Forms.Integration.WindowsFormsHost> コントロールから、メッセージ ループの存在を登録する内部静的メソッドが呼び出されます。  
  
 登録時に、<xref:System.Windows.Forms.Integration.WindowsFormsHost> コントロールによってメッセージ ループが調べられます。 メッセージ ループが開始されていない場合は、<xref:System.Windows.Interop.ComponentDispatcher.ThreadFilterMessage?displayProperty=nameWithType> イベント ハンドラーが作成されます。 メッセージ ループは、<xref:System.Windows.Interop.ComponentDispatcher.ThreadFilterMessage?displayProperty=nameWithType> イベント ハンドラーがアタッチされているときに実行されていると見なされます。  
  
 ウィンドウ ハンドルが破棄されると、<xref:System.Windows.Forms.Integration.WindowsFormsHost> コントロールが登録から削除されます。  
  
## <a name="elementhost-keyboard-and-message-processing"></a>ElementHost のキーボードとメッセージの処理  
 Windows フォーム アプリケーションでホストされている場合、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] キーボードとメッセージの処理は以下で構成されます。  
  
- <xref:System.Windows.Interop.HwndSource>、<xref:System.Windows.Interop.IKeyboardInputSink>、および <xref:System.Windows.Interop.IKeyboardInputSite> インターフェイスの実装。  
  
- タブ移動と方向キー  
  
- コマンド キーとダイアログ ボックスのキー。  
  
- Windows フォーム アクセラレータ処理。  
  
 以下のセクションでは、これらの部分について詳しく説明します。  
  
### <a name="interface-implementations"></a>インターフェイスの実装  
 Windows フォームでは、キーボード メッセージはフォーカスのあるコントロールのウィンドウ ハンドルにルーティングされます。 <xref:System.Windows.Forms.Integration.ElementHost> コントロールでは、これらのメッセージはホストされている要素にルーティングされます。 これを実現するために、<xref:System.Windows.Forms.Integration.ElementHost> コントロールには <xref:System.Windows.Interop.HwndSource> インスタンスが用意されています。 <xref:System.Windows.Forms.Integration.ElementHost> コントロールにフォーカスがある場合、<xref:System.Windows.Interop.HwndSource> インスタンスによってほとんどのキーボード入力がルーティングされ、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] <xref:System.Windows.Input.InputManager> クラスで処理できるようになります。  
  
 <xref:System.Windows.Interop.HwndSource> クラスには、<xref:System.Windows.Interop.IKeyboardInputSink> および <xref:System.Windows.Interop.IKeyboardInputSite> インターフェイスが実装されています。  
  
 キーボードの相互運用は、ホストされている要素からフォーカスを移動する Tab キーと方向キーの入力を処理する <xref:System.Windows.Interop.IKeyboardInputSite.OnNoMoreTabStops%2A> メソッドの実装に依存しています。  
  
### <a name="tabbing-and-arrow-keys"></a>タブ移動と方向キー  
 Windows フォーム選択ロジックは、Tab キーと方向キーのナビゲーションを実装するために、<xref:System.Windows.Interop.HwndSource.System%23Windows%23Interop%23IKeyboardInputSink%23TabInto%2A> および <xref:System.Windows.Interop.IKeyboardInputSite.OnNoMoreTabStops%2A> メソッドにマップされます。 <xref:System.Windows.Forms.Integration.ElementHost.Select%2A> メソッドをオーバーライドすると、このマッピングが行われます。  
  
### <a name="command-keys-and-dialog-box-keys"></a>コマンド キーとダイアログ ボックス キー。  
 コマンド キーとダイアログ キーを処理する最初の機会を [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] に与えるために、Windows フォーム コマンドの前処理は <xref:System.Windows.Interop.IKeyboardInputSink.TranslateAccelerator%2A> メソッドに接続されています。 <xref:System.Windows.Forms.Control.ProcessCmdKey%2A?displayProperty=nameWithType> メソッドをオーバーライドすると、2 つのテクノロジが接続されます。  
  
 <xref:System.Windows.Interop.IKeyboardInputSink.TranslateAccelerator%2A> メソッドを使用すると、ホストされている要素では、WM_KEYDOWN、WM_KEYUP、WM_SYSKEYDOWN、WM_SYSKEYUP などの任意のキー メッセージ (Tab キー、Enter キー、Esc キー、方向キーなどのコマンド キーを含む) を処理できます。 キー メッセージが処理されない場合は、処理のために Windows フォームの先祖階層が送信されます。  
  
### <a name="accelerator-processing"></a>アクセラレータの処理  
 アクセラレータを正しく処理するには、Windows フォーム アクセラレータ処理を [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] <xref:System.Windows.Input.AccessKeyManager> クラスに接続する必要があります。 さらに、すべての WM_CHAR メッセージは、ホストされている要素に正しくルーティングされる必要があります。  
  
 <xref:System.Windows.Interop.IKeyboardInputSink.TranslateChar%2A> メソッドの既定の <xref:System.Windows.Interop.HwndSource> 実装からは `false` が返されるため、WM_CHAR メッセージは次のロジックを使用して処理されます。  
  
- すべての WM_CHAR メッセージがホストされる要素に確実に転送されるように、<xref:System.Windows.Forms.Control.IsInputChar%2A?displayProperty=nameWithType> メソッドはオーバーライドされます。  
  
- Alt キーが押された場合、メッセージは WM_SYSCHAR です。 Windows フォームでは、<xref:System.Windows.Forms.Control.IsInputChar%2A> メソッドを通じてこのメッセージが前処理されません。 そのため、<xref:System.Windows.Forms.Control.ProcessMnemonic%2A> メソッドは、登録されたアクセラレータの [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] <xref:System.Windows.Input.AccessKeyManager> のクエリを実行するためにオーバーライドされます。 登録されているアクセラレータが見つかった場合、<xref:System.Windows.Input.AccessKeyManager> によってそれが処理されます。  
  
- Alt キーが押されていない場合、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] <xref:System.Windows.Input.InputManager> クラスによって未処理の入力が処理されます。 入力がアクセラレータである場合、<xref:System.Windows.Input.AccessKeyManager> によって処理されます。 <xref:System.Windows.Input.InputManager.PostProcessInput> イベントは、処理されなかった WM_CHAR メッセージに対して処理されます。  
  
 ユーザーが Alt キーを押すと、フォーム全体にアクセラレータの視覚的な合図が表示されます。 この動作をサポートするために、アクティブなフォームのすべての <xref:System.Windows.Forms.Integration.ElementHost> コントロールは、フォーカスのあるコントロールに関係なく、WM_SYSKEYDOWN メッセージを受け取ります。  
  
 メッセージはアクティブ フォームの <xref:System.Windows.Forms.Integration.ElementHost> コントロールにのみ送信されます。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Forms.Integration.WindowsFormsHost.EnableWindowsFormsInterop%2A>
- <xref:System.Windows.Forms.Integration.ElementHost.EnableModelessKeyboardInterop%2A>
- <xref:System.Windows.Forms.Integration.ElementHost>
- <xref:System.Windows.Forms.Integration.WindowsFormsHost>
- [チュートリアル: WPF での Windows フォーム複合コントロールのホスト](walkthrough-hosting-a-windows-forms-composite-control-in-wpf.md)
- [チュートリアル: Windows フォームでの WPF 複合コントロールのホスト](walkthrough-hosting-a-wpf-composite-control-in-windows-forms.md)
- [WPF と Win32 の相互運用性](wpf-and-win32-interoperation.md)
