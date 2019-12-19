---
title: UI オートメーションによる Window コントロール型のサポート
ms.date: 03/30/2017
helpviewer_keywords:
- UI Automation, Window control type
- Window control type
- control types, Window
ms.assetid: 53be78a6-cdcc-4af3-a464-5927d19c54e8
ms.openlocfilehash: b8e5a55de2c8e4e2bc0f4ce0427d79483b9b3288
ms.sourcegitcommit: 32a575bf4adccc901f00e264f92b759ced633379
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/04/2019
ms.locfileid: "74801397"
---
# <a name="ui-automation-support-for-the-window-control-type"></a>UI オートメーションによる Window コントロール型のサポート
> [!NOTE]
> このドキュメントは、[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 名前空間で定義されているマネージド <xref:System.Windows.Automation> クラスを使用する .NET Framework 開発者を対象としています。 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]の最新情報については、「 [Windows Automation API: UI Automation (Windows のオートメーション API: UI オートメーション)](/windows/win32/winauto/entry-uiauto-win32)」を参照してください。  
  
 このトピックでは、Window コントロール型の [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] サポートについて説明します。 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]でのコントロール型とは、コントロールが <xref:System.Windows.Automation.AutomationElement.ControlTypeProperty> プロパティを使用するために満たす必要がある一連の条件のことです。 条件には、 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] ツリー構造、 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] プロパティの値、およびコントロール パターンに関する特定のガイドラインが含まれます。  
  
 ウィンドウ コントロールは、子オブジェクト (タイトル バー、クライアント、その他のオブジェクトなど) が含まれているウィンドウ フレームで構成されます。  
  
 以下のセクションの [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] の要件は、 [!INCLUDE[TLA#tla_winclient](../../../includes/tlasharptla-winclient-md.md)]、 [!INCLUDE[TLA#tla_win32](../../../includes/tlasharptla-win32-md.md)]、 [!INCLUDE[TLA#tla_winforms](../../../includes/tlasharptla-winforms-md.md)]のいずれの場合でも、Window コントロール型を実装するすべてのコントロールに適用されます。  
  
## <a name="required-ui-automation-tree-structure"></a>必須の UI オートメーション ツリー構造  
 次の表に、ウィンドウ コントロールに関連する [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] ツリーのコントロール ビューとコンテンツ ビューを示し、それぞれのビューに含めることができる内容について説明します。 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]ツリーの詳細については、[UI Automation Tree Overview](ui-automation-tree-overview.md)をご覧ください。  
  
|コントロール ビュー|コンテンツ ビュー|  
|------------------|------------------|  
|[Window]|[Window]|  
  
## <a name="required-ui-automation-properties"></a>必須の UI オートメーション プロパティ  
 次の表に、ウィンドウ コントロールに特に関連する値または定義を持つ [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] プロパティを示します。 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]プロパティの詳細については[クライアントの UI オートメーション プロパティ](ui-automation-properties-for-clients.md)をご覧ください。  
  
|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] プロパティ|Value|メモ|  
|------------------------------------------------------------------------------------|-----------|-----------|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationIdProperty>|「ノート」をご覧ください。|このプロパティの値は、アプリケーション内のすべてのコントロールで一意である必要があります。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty>|「ノート」をご覧ください。|コントロール全体を格納する最も外側の四角形。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ClickablePointProperty>|「ノート」をご覧ください。|ウィンドウ コントロールにはクリック可能なポイントがなければならず、これをクリックすることによってウィンドウが選択、または選択解除された状態になります。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ControlTypeProperty>|[Window]|この値は、すべての UI フレームワークで同じです。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsContentElementProperty>|True|ウィンドウ コントロールは、常にコンテンツである必要があります。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsControlElementProperty>|True|ウィンドウ コントロールは、常にコントロールである必要があります。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsKeyboardFocusableProperty>|「ノート」をご覧ください。|コントロールがキーボード フォーカスを受け取ることができる場合は、このプロパティをサポートする必要があります。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LabeledByProperty>|`null`|ウィンドウ コントロールには、静的な Window ラベルがありません。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LocalizedControlTypeProperty>|"window"|Window コントロール型に対応する、ローカライズされた文字列。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.NameProperty>|「ノート」をご覧ください。|ウィンドウ コントロールには、主要なウィンドウ要素が常に含まれています。この要素は、ユーザーがその項目の最もセマンティックな識別子として関連付けるであろうものに関連しています。|  
  
## <a name="required-ui-automation-control-patterns"></a>必須の UI オートメーション コントロール パターン  
 次の表に、ウィンドウ コントロールでサポートする必要がある [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] コントロール パターンの一覧を示します。 コントロール パターンの詳細については、「 [UI Automation Control Patterns Overview](ui-automation-control-patterns-overview.md)」を参照してください。  
  
|コントロール パターン|でのサポート|メモ|  
|---------------------|-------------|-----------|  
|<xref:System.Windows.Automation.Provider.IDockProvider>|条件|ウィンドウがドッキングできる場合は、サポートする必要があります。|  
|<xref:System.Windows.Automation.Provider.ITransformProvider>|必須|ウィンドウが画面上で移動、サイズ変更、または回転できるようにします。|  
|<xref:System.Windows.Automation.Provider.IWindowProvider>|必須|ウィンドウで特定の操作ができるようにします。|  
  
## <a name="required-ui-automation-events"></a>必須の UI オートメーション イベント  
 次の表に、すべてのウィンドウ コントロールでサポートする必要がある [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] イベントを示します。 イベントについて詳しくは、「 [UI Automation Events Overview](ui-automation-events-overview.md)」をご覧ください。  
  
|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] イベント|でのサポート|メモ|  
|---------------------------------------------------------------------------------|-------------|-----------|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AsyncContentLoadedEvent>|必須|[なし]|  
|<xref:System.Windows.Automation.AutomationElement.AutomationFocusChangedEvent>|必須|[なし]|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty> プロパティ変更イベント。|必須|[なし]|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty> プロパティ変更イベント。|必須|[なし]|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsOffscreenProperty> プロパティ変更イベント。|必須|[なし]|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LayoutInvalidatedEvent>|必須|[なし]|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.NameProperty> プロパティ変更イベント。|必須|[なし]|  
|<xref:System.Windows.Automation.AutomationElement.StructureChangedEvent>|必須|[なし]|  
|<xref:System.Windows.Automation.ScrollPatternIdentifiers.HorizontallyScrollableProperty> プロパティ変更イベント。|状況に依存|[なし]|  
|<xref:System.Windows.Automation.ScrollPatternIdentifiers.HorizontalScrollPercentProperty> プロパティ変更イベント。|状況に依存|[なし]|  
|<xref:System.Windows.Automation.ScrollPatternIdentifiers.HorizontalViewSizeProperty> プロパティ変更イベント。|状況に依存|[なし]|  
|<xref:System.Windows.Automation.ScrollPatternIdentifiers.VerticalScrollPercentProperty> プロパティ変更イベント。|状況に依存|[なし]|  
|<xref:System.Windows.Automation.ScrollPatternIdentifiers.VerticallyScrollableProperty> プロパティ変更イベント。|状況に依存|[なし]|  
|<xref:System.Windows.Automation.ScrollPatternIdentifiers.VerticalViewSizeProperty> プロパティ変更イベント。|状況に依存|[なし]|  
|<xref:System.Windows.Automation.WindowPatternIdentifiers.WindowClosedEvent>|必須|[なし]|  
|<xref:System.Windows.Automation.WindowPatternIdentifiers.WindowOpenedEvent>|必須|[なし]|  
|<xref:System.Windows.Automation.WindowPatternIdentifiers.WindowVisualStateProperty> プロパティ変更イベント。|状況に依存|[なし]|  
  
## <a name="see-also"></a>参照

- <xref:System.Windows.Automation.ControlType.Window>
- [UI オートメーション コントロール型の概要](ui-automation-control-types-overview.md)
- [UI オートメーションの概要](ui-automation-overview.md)
