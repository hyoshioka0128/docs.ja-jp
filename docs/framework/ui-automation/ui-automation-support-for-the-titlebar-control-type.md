---
title: UI オートメーションによる TitleBar コントロール型のサポート
ms.date: 03/30/2017
helpviewer_keywords:
- control types, Title Bar
- Title Bar control type
- UI Automation, Title Bar control type
ms.assetid: 3b7a4e13-0305-45d5-bc33-1f4133c50782
ms.openlocfilehash: 19c203151956ae17dbcf608c135e7fe97a2b4389
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79179476"
---
# <a name="ui-automation-support-for-the-titlebar-control-type"></a>UI オートメーションによる TitleBar コントロール型のサポート
> [!NOTE]
> このドキュメントは、[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 名前空間で定義されているマネージド <xref:System.Windows.Automation> クラスを使用する .NET Framework 開発者を対象としています。 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]の最新情報については、「 [Windows Automation API: UI オートメーション](/windows/win32/winauto/entry-uiauto-win32)」をご覧ください。  
  
 このトピックでは、TitleBar コントロール型に対する [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] のサポートについて説明します。 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]でのコントロール型とは、コントロールが <xref:System.Windows.Automation.AutomationElement.ControlTypeProperty> プロパティを使用するために満たす必要がある一連の条件のことです。 これらの条件には、 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] ツリー構造、 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] のプロパティ値、およびコントロール パターンに関する特定のガイドラインが含まれます。  
  
 タイトル バー コントロールは、ウィンドウ内のタイトルまたはキャプション バーを表します。  
  
 以下の各セクションで、TitleBar コントロール型に必要な [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] ツリー構造、プロパティ、コントロール パターン、およびイベントを定義します。 要件[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]は、Win32 または Windows[!INCLUDE[TLA#tla_winclient](../../../includes/tlasharptla-winclient-md.md)]フォームのいずれでも、すべてのタイトル バー コントロールに適用されます。  
  
<a name="Required_UI_Automation_Tree_Structure"></a>
## <a name="required-ui-automation-tree-structure"></a>必須の UI オートメーション ツリー構造  
 次の表に、タイトル バー コントロールに関連する [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] ツリーのコントロール ビューとコンテンツ ビューを示し、それぞれのビューに含まれる可能性のある内容について説明します。 ツリーの詳細については、「 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] UI[オートメーション ツリーの概要](ui-automation-tree-overview.md)」を参照してください。  
  
|コントロール ビュー|コンテンツ ビュー|  
|------------------|------------------|  
|TitleBar<br /><br /> - メニュー(0または1)<br />- ボタン (0 以上)|適用不可。 (タイトル バー コントロールにはコンテンツはありません。)|  
  
<a name="Required_UI_Automation_Properties"></a>
## <a name="required-ui-automation-properties"></a>必須の UI オートメーション プロパティ  
 次の表に、TitleBar コントロールに特に関連する値または定義を持つ [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] プロパティを示します。 プロパティの詳細[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]については、「[クライアントの UI オートメーション プロパティ 」](ui-automation-properties-for-clients.md)を参照してください。  
  
|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] プロパティ|Value|Notes|  
|------------------------------------------------------------------------------------|-----------|-----------|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationIdProperty>|「ノート」を参照してください。|このプロパティの値は、アプリケーション内のすべてのコントロールで一意である必要があります。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty>|「ノート」を参照してください。|タイトル バーの四角形領域は、タイトル バー コントロールに含まれるコントロールをすべて囲んでいる必要があります。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ClickablePointProperty>|「ノート」を参照してください。|四角形領域が存在する場合にサポートされます。 四角形領域内にクリック不可能な点が存在し、特別なヒット テストを実行する場合は、オーバーライドしてクリック可能な点を提供します。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsKeyboardFocusableProperty>|False|タイトル バーで、キーボード フォーカスを持つことはありません。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.NameProperty>|""|タイトル バーはコンテンツではありません。タイトル バーのテキスト情報は、親ウィンドウで公開されます。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LabeledByProperty>|「ノート」を参照してください。|通常、タイトル バー コントロールにラベルはありません。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ControlTypeProperty>|TitleBar|この値は、すべての UI フレームワークで同じです。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LocalizedControlTypeProperty>|"タイトル バー"|TitleBar コントロール型に対応する、ローカライズされた文字列。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsContentElementProperty>|False|タイトル バー コントロールはコンテンツではありません。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsControlElementProperty>|True|タイトル バー コントロールは、常にコントロールである必要があります。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsOffscreenProperty>|依存|このコントロールは、タイトル バーが画面上に表示されているかどうかに応じた値を返します。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.HelpTextProperty>|""|ヘルプ テキストを公開する必要はありません。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AcceleratorKeyProperty>|""|タイトル バーで、アクセラレータ キーを持つことはありません。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AccessKeyProperty>|""|タイトル バー コントロールにアクセス キーはありません。|  
  
<a name="Required_UI_Automation_Control_Patterns"></a>
## <a name="required-ui-automation-control-patterns"></a>必須の UI オートメーション コントロール パターン  
 TitleBar コントロール型は、どのコントロール パターンもサポートする必要はありません。 タイトル バーの機能は、Window コントロール上の Window コントロール パターンを通じて公開されます。  
  
## <a name="required-ui-automation-events"></a>必須の UI オートメーション イベント  
 次の表に、すべてのタイトル バー コントロールでサポートする必要がある [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] イベントを示します。 イベントの詳細については、「 [UI Automation Events Overview](ui-automation-events-overview.md)」を参照してください。  
  
|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] イベント|サポート|Notes|  
|---------------------------------------------------------------------------------|-------------|-----------|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty> プロパティ変更イベント。|Required|なし|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsOffscreenProperty> プロパティ変更イベント。|Required|なし|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty> プロパティ変更イベント。|なし|なし|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationFocusChangedEvent>|なし|なし|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.StructureChangedEvent>|Required|なし|  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Automation.ControlType.TitleBar>
- [UI オートメーション コントロール型の概要](ui-automation-control-types-overview.md)
- [UI オートメーションの概要](ui-automation-overview.md)
