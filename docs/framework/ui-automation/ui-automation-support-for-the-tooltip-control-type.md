---
title: UI オートメーションによる ToolTip コントロール型のサポート
ms.date: 03/30/2017
helpviewer_keywords:
- UI Automation, ToolTip control type
- ToolTip control type
- control types, ToolTip
ms.assetid: c3779d78-3164-43ae-8dae-bfaeafffdd65
ms.openlocfilehash: 8531270efb5a7bc5896c5d2fa04dd0632547cac7
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79179468"
---
# <a name="ui-automation-support-for-the-tooltip-control-type"></a>UI オートメーションによる ToolTip コントロール型のサポート
> [!NOTE]
> このドキュメントは、[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 名前空間で定義されているマネージド <xref:System.Windows.Automation> クラスを使用する .NET Framework 開発者を対象としています。 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]の最新情報については、「 [Windows Automation API: UI オートメーション](/windows/win32/winauto/entry-uiauto-win32)」をご覧ください。  
  
 このトピックでは、ToolTip コントロール型に対する [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] のサポートについて説明します。 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]でのコントロール型とは、コントロールが <xref:System.Windows.Automation.AutomationElement.ControlTypeProperty> プロパティを使用するために満たす必要がある一連の条件のことです。 これらの条件には、 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] ツリー構造、 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] のプロパティ値、およびコントロール パターンに関する特定のガイドラインが含まれます。  
  
 ツール ヒント コントロールは、テキストを含むポップアップ ウィンドウです。  
  
 以下の各セクションで、ToolTip コントロール型に必要な [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] ツリー構造、プロパティ、コントロール パターン、およびイベントを定義します。 要件[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]は、Win32 または Windows[!INCLUDE[TLA#tla_winclient](../../../includes/tlasharptla-winclient-md.md)]フォームのいずれでも、すべてのツール ヒント コントロールに適用されます。  
  
<a name="Required_UI_Automation_Tree_Structure"></a>
## <a name="required-ui-automation-tree-structure"></a>必須の UI オートメーション ツリー構造  
 次の表に、ツール ヒント コントロールに関連する [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] ツリーのコントロール ビューとコンテンツ ビューを示し、それぞれのビューに含めることができる内容について説明します。 ツリーの詳細については、「 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] UI[オートメーション ツリーの概要](ui-automation-tree-overview.md)」を参照してください。  
  
|コントロール ビュー|コンテンツ ビュー|  
|------------------|------------------|  
|ヒント<br /><br /> - テキスト (0 以上)<br />- 画像 (0 以上)|ヒント|  
  
 ツール ヒント コントロールは、キーボード フォーカスを受け取ることができる場合は、 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] ツリーのコンテンツ ビューにのみ表示されます。 それ以外の場合、ツール ヒントの情報はすべて、ツール ヒントが参照している `HelpTextProperty` 要素の [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] から取得できます。  
  
 ツール ヒントは、その情報が参照しているコントロールの下に表示されます。 クライアントは、ツール ヒントに含まれる情報を常に取得できるよう、 `ToolTipOpenedEvent` をリッスンする必要があります。  
  
<a name="Required_UI_Automation_Properties"></a>
## <a name="required-ui-automation-properties"></a>必須の UI オートメーション プロパティ  
 次の表に、ツール ヒント コントロールに特に関連する値または定義を持つ [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] プロパティを示します。 プロパティの詳細[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]については、「[クライアントの UI オートメーション プロパティ 」](ui-automation-properties-for-clients.md)を参照してください。  
  
|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] プロパティ|Value|Notes|  
|------------------------------------------------------------------------------------|-----------|-----------|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationIdProperty>|「ノート」を参照してください。|このプロパティの値は、アプリケーション内のすべてのコントロールで一意である必要があります。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty>|「ノート」を参照してください。|コントロール全体を格納する最も外側の四角形。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ClickablePointProperty>|「ノート」を参照してください。|クリック可能なポイントは、コントロールを閉じるツール ヒントの部分である必要があります。 一部のツール ヒントには、この機能がありません。その場合、クリック可能なポイントを持ちません。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsKeyboardFocusableProperty>|「ノート」を参照してください。|コントロールがキーボード フォーカスを受け取ることができる場合は、このプロパティをサポートする必要があります。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.NameProperty>|「ノート」を参照してください。|ツール ヒント内に表示されるテキストがツール ヒント コントロールの名前になります。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LabeledByProperty>|`Null`|ツール ヒント コントロールは、常にそのコンテンツで自己ラベル付けを行います。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ControlTypeProperty>|ヒント|この値は、すべての UI フレームワークで同じです。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LocalizedControlTypeProperty>|"ツール ヒント"|ToolTip コントロール型に対応する、ローカライズされた文字列。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsContentElementProperty>|依存|ツール ヒント コントロールがキーボード フォーカスを受け取ることができる場合、ツリーのコンテンツ ビューにのみ表示される必要があります。 テキストのみである場合は、生成元のコントロールの HelpTextProperty として取得できます。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsControlElementProperty>|True|ツール ヒント コントロールは、常にコントロールである必要があります。|  
  
<a name="Required_UI_Automation_Control_Patterns"></a>
## <a name="required-ui-automation-control-patterns"></a>必須の UI オートメーション コントロール パターン  
 次の表に、ツール ヒント コントロールでサポートされなければならない [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] コントロール パターンを示します。 コントロール パターンの詳細については、「 [UI Automation Control Patterns Overview](ui-automation-control-patterns-overview.md)」を参照してください。  
  
|コントロール パターン|サポート|Notes|  
|---------------------|-------------|-----------|  
|<xref:System.Windows.Automation.Provider.IWindowProvider>|依存|UI 項目をクリックして閉じることができるツール ヒントは、自動的に閉じるように、WindowPattern をサポートする必要があります。|  
|<xref:System.Windows.Automation.Provider.ITextProvider>|依存|アクセシビリティを向上させるために、ツール ヒント コントロールでは Text コントロール パターンをサポートできますが、必須ではありません。 テキストにさまざまなスタイルや属性 (たとえば、色、太字、斜体など) がある場合、Text コントロール パターンの使用をお勧めします。|  
  
<a name="Required_UI_Automation_Events"></a>
## <a name="required-ui-automation-events"></a>必須の UI オートメーション イベント  
 ツール ヒント コントロールは、画面に表示された場合に `ToolTipOpenedEvent` を生成する必要があります。 イベントにツール ヒント自体の [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 要素への参照が組み込まれます。  
  
 次の表に、すべてのツール ヒント コントロールでサポートされなければならない [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] イベントを示します。 イベントの詳細については、「 [UI Automation Events Overview](ui-automation-events-overview.md)」を参照してください。  
  
|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] イベント|サポート|Notes|  
|---------------------------------------------------------------------------------|-------------|-----------|  
|<xref:System.Windows.Automation.TextPatternIdentifiers.TextSelectionChangedEvent>|依存|なし|  
|<xref:System.Windows.Automation.TextPatternIdentifiers.TextChangedEvent>|依存|なし|  
|<xref:System.Windows.Automation.WindowPatternIdentifiers.WindowClosedEvent>|依存|なし|  
|<xref:System.Windows.Automation.WindowPatternIdentifiers.WindowOpenedEvent>|依存|なし|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ToolTipOpenedEvent>|Required|なし|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ToolTipClosedEvent>|Required|なし|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty> プロパティ変更イベント。|Required|なし|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsOffscreenProperty> プロパティ変更イベント。|Required|なし|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty> プロパティ変更イベント。|Required|なし|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.NameProperty> プロパティ変更イベント。|Required|なし|  
|<xref:System.Windows.Automation.WindowPatternIdentifiers.WindowVisualStateProperty> プロパティ変更イベント。|依存|なし|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationFocusChangedEvent>|Required|なし|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.StructureChangedEvent>|Required|なし|  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Automation.ControlType.ToolTip>
- [UI オートメーション コントロール型の概要](ui-automation-control-types-overview.md)
- [UI オートメーションの概要](ui-automation-overview.md)
