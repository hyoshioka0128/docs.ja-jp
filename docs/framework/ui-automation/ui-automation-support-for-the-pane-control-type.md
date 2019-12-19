---
title: UI オートメーションによる Pane コントロール型のサポート
ms.date: 03/30/2017
helpviewer_keywords:
- UI Automation, Pane control type
- Pane control type
- control types, Pane
ms.assetid: 79761191-4449-4630-899c-9cbdb8867d3f
ms.openlocfilehash: fcba014a1ff13204688ce176a5efcb5fecb58b8f
ms.sourcegitcommit: 32a575bf4adccc901f00e264f92b759ced633379
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/04/2019
ms.locfileid: "74800347"
---
# <a name="ui-automation-support-for-the-pane-control-type"></a>UI オートメーションによる Pane コントロール型のサポート
> [!NOTE]
> このドキュメントは、[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 名前空間で定義されているマネージド <xref:System.Windows.Automation> クラスを使用する .NET Framework 開発者を対象としています。 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]の最新情報については、「 [Windows Automation API: UI Automation (Windows のオートメーション API: UI オートメーション)](/windows/win32/winauto/entry-uiauto-win32)」を参照してください。  
  
 このトピックでは、Pane コントロール型の [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] サポートについて説明します。 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]でのコントロール型とは、コントロールが <xref:System.Windows.Automation.AutomationElement.ControlTypeProperty> プロパティを使用するために満たす必要がある一連の条件のことです。 これらの条件には、 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] ツリー構造、 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] のプロパティ値、およびコントロール パターンに関する特定のガイドラインが含まれます。  
  
 Pane コントロール型は、フレームまたはドキュメント ウィンドウ内のオブジェクトを表すために使用します。 ユーザーはペイン コントロール間や現在のペインの内容の中を移動することができますが、異なるペインの項目間を移動することはできません。 そのため、ペイン コントロールは、ウィンドウやドキュメントより下で、個々のコントロールより上のグループ化のレベルを表します。 ユーザーは、状況に応じて、TAB、F6、または CTRL + TAB キーを押すことによって、ペイン間を移動します。 Pane コントロール型には、特定のキーボード ナビゲーションは必要ありません。  
  
 以降のセクションでは、Pane コントロール型に必要な [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] ツリー構造、プロパティ、コントロール パターン、およびイベントを定義します。 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] の各要件は、 [!INCLUDE[TLA#tla_winclient](../../../includes/tlasharptla-winclient-md.md)]、 [!INCLUDE[TLA#tla_win32](../../../includes/tlasharptla-win32-md.md)]、 [!INCLUDE[TLA#tla_winforms](../../../includes/tlasharptla-winforms-md.md)]のいずれの場合でも、すべてのリスト コントロールに当てはまります。  
  
<a name="Required_UI_Automation_Tree_Structure"></a>   
## <a name="required-ui-automation-tree-structure"></a>必須の UI オートメーション ツリー構造  
 次の表に、ペイン コントロールに関連する [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] ツリーのコントロール ビューとコンテンツ ビューを示し、それぞれのビューに含めることができる内容について説明します。 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]ツリーの詳細については、[UI Automation Tree Overview](ui-automation-tree-overview.md)をご覧ください。  
  
|コントロール ビュー|コンテンツ ビュー|  
|------------------|------------------|  
|ペイン|ペイン|  
  
<a name="Required_UI_Automation_Properties"></a>   
## <a name="required-ui-automation-properties"></a>必須の UI オートメーション プロパティ  
 次の表に、ペイン コントロールに特に関連する値や定義を持つ [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] プロパティを示します。 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] のプロパティの詳細については、「[クライアントの UI オートメーションのプロパティ](ui-automation-properties-for-clients.md)」を参照してください。  
  
|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] プロパティ|Value|メモ|  
|------------------------------------------------------------------------------------|-----------|-----------|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationIdProperty>|「ノート」をご覧ください。|このプロパティの値は、アプリケーション内のすべてのコントロールで一意である必要があります。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty>|「ノート」をご覧ください。|コントロール全体を格納する最も外側の四角形。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsKeyboardFocusableProperty>|「ノート」をご覧ください。|コントロールがキーボード フォーカスを受け取ることができる場合は、このプロパティをサポートする必要があります。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.NameProperty>|「ノート」をご覧ください。|このプロパティの値は、必ず明確で簡潔でわかりやすいタイトルにする必要があります。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ClickablePointProperty>|「ノート」をご覧ください。|このプロパティは、クリックされた場合にペインにフォーカスが移動する、ペイン コントロールのクリック可能なポイントを公開します。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LabeledByProperty>|「ノート」をご覧ください。|通常、ペイン コントロールに静的ラベルはありません。 静的なテキスト ラベルが存在する場合は、このプロパティを介して公開する必要があります。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ControlTypeProperty>|ペイン|この値は、すべての [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] フレームワークで同じです。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LocalizedControlTypeProperty>|"pane"|Pane コントロール型に対応する、ローカライズされた文字列。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsContentElementProperty>|True|ペイン コントロールは、常に [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] ツリーのコンテンツ ビューに組み込まれます。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsControlElementProperty>|True|ペイン コントロールは、常に [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] ツリーのコントロール ビューに組み込まれます。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.HelpTextProperty>|""|ペイン コントロールのヘルプ テキストで、各フレームの用途とフレーム間の関係を説明する必要があります。 フレームの目的や関係が `NameProperty`の値からわからない場合は、説明が必要です。 "|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AccessKeyProperty>|「ノート」をご覧ください。|特定のキーの組み合わせによってペインにフォーカスが移動する場合は、このプロパティを介してその情報を公開する必要があります。|  
  
<a name="Required_UI_Automation_Control_Patterns"></a>   
## <a name="required-ui-automation-control-patterns"></a>必須の UI オートメーション コントロール パターン  
 次の表に、すべてのペイン コントロールでサポートされなければならない [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] コントロール パターンを示します。 コントロール パターンの詳細については、「 [UI Automation Control Patterns Overview](ui-automation-control-patterns-overview.md)」を参照してください。  
  
|コントロール パターン|でのサポート|メモ|  
|---------------------|-------------|-----------|  
|<xref:System.Windows.Automation.Provider.ITransformProvider>|状況に依存|画面上でのペイン コントロールの移動、サイズ変更、または回転が可能な場合は、このコントロール パターンを実装します。|  
|<xref:System.Windows.Automation.Provider.IWindowProvider>|使用しない|このコントロール パターンを実装する必要がある場合は、コントロールが <xref:System.Windows.Automation.ControlType.Window> コントロール型に基づいている必要があります。|  
|<xref:System.Windows.Automation.Provider.IDockProvider>|状況に依存|ペイン コントロールがドッキング可能な場合は、このコントロール パターンを実装します。|  
|<xref:System.Windows.Automation.Provider.IScrollProvider>|状況に依存|ペイン コントロールがスクロール可能な場合は、このコントロール パターンを実装します。|  
  
<a name="Required_UI_Automation_Events"></a>   
## <a name="required-ui-automation-events"></a>必須の UI オートメーション イベント  
 次の表に、すべてのペイン コントロールでサポートされなければならない [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] イベントを示します。 イベントについて詳しくは、「 [UI Automation Events Overview](ui-automation-events-overview.md)」をご覧ください。  
  
|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] イベント|サポート/値|メモ|  
|---------------------------------------------------------------------------------|--------------------|-----------|  
|<xref:System.Windows.Automation.WindowPatternIdentifiers.WindowClosedEvent>|使用しない|[なし]|  
|<xref:System.Windows.Automation.WindowPatternIdentifiers.WindowOpenedEvent>|使用しない|[なし]|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AsyncContentLoadedEvent>|必須|[なし]|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty> プロパティ変更イベント。|必須|[なし]|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsOffscreenProperty> プロパティ変更イベント。|必須|[なし]|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty> プロパティ変更イベント。|必須|[なし]|  
|<xref:System.Windows.Automation.ScrollPatternIdentifiers.HorizontallyScrollableProperty> プロパティ変更イベント。|状況に依存|[なし]|  
|<xref:System.Windows.Automation.ScrollPatternIdentifiers.HorizontalScrollPercentProperty> プロパティ変更イベント。|状況に依存|[なし]|  
|<xref:System.Windows.Automation.ScrollPatternIdentifiers.HorizontalViewSizeProperty> プロパティ変更イベント。|状況に依存|[なし]|  
|<xref:System.Windows.Automation.ScrollPatternIdentifiers.VerticalScrollPercentProperty> プロパティ変更イベント。|状況に依存|[なし]|  
|<xref:System.Windows.Automation.ScrollPatternIdentifiers.VerticallyScrollableProperty> プロパティ変更イベント。|状況に依存|[なし]|  
|<xref:System.Windows.Automation.ScrollPatternIdentifiers.VerticalViewSizeProperty> プロパティ変更イベント。|状況に依存|[なし]|  
|<xref:System.Windows.Automation.WindowPatternIdentifiers.WindowVisualStateProperty> プロパティ変更イベント。|使用しない|[なし]|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationFocusChangedEvent>|必須|[なし]|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.StructureChangedEvent>|必須|[なし]|  
  
<a name="Pane_Control_Type_Example"></a>   
## <a name="pane-control-type-example"></a>Pane コントロール型の例  
 次の図に、Pane コントロール型を実装するコントロールを示します。  
  
 ![2つのペインがあるアプレットウィンドウのスクリーンショット](./media/uiauto-pane.GIF "uiauto_pane")  
  
|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] ツリー - コントロール ビュー|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] ツリー - コンテンツ ビュー|  
|------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------|  
|<ul><li>ペイン</li><li>ツリー (スクロール パターン)<br /><br /> <ul><li>TreeItem</li><li>ペイン</li><li>編集 (スクロール パターン)</li></ul></li></ul>|-ウィンドウ<br />-Tree (スクロールパターン)<br />-TreeItem<br />- ...枠内<br />-編集<br />-(スクロールパターン)|  
  
## <a name="see-also"></a>参照

- <xref:System.Windows.Automation.ControlType.Pane>
- [UI オートメーション コントロール型の概要](ui-automation-control-types-overview.md)
- [UI オートメーションの概要](ui-automation-overview.md)
