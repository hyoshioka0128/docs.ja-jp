---
title: UI オートメーションによる ScrollBar コントロール型のサポート
ms.date: 03/30/2017
helpviewer_keywords:
- UI Automation, Scroll Bar control type
- control types, Scroll Bar
- Scroll Bar control type
ms.assetid: 329891d7-b609-49e6-920a-09ea8a627d07
ms.openlocfilehash: 88a606369103e989b41ecf3569d54247cf3f83fa
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79179615"
---
# <a name="ui-automation-support-for-the-scrollbar-control-type"></a>UI オートメーションによる ScrollBar コントロール型のサポート
> [!NOTE]
> このドキュメントは、[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 名前空間で定義されているマネージド <xref:System.Windows.Automation> クラスを使用する .NET Framework 開発者を対象としています。 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]の最新情報については、「 [Windows Automation API: UI オートメーション](/windows/win32/winauto/entry-uiauto-win32)」をご覧ください。  
  
 このトピックでは、ScrollBar コントロール型に対する [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] のサポートについて説明します。 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]でのコントロール型とは、コントロールが <xref:System.Windows.Automation.AutomationElement.ControlTypeProperty> プロパティを使用するために満たす必要がある一連の条件のことです。 これらの条件には、 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] ツリー構造、 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] のプロパティ値、およびコントロール パターンに関する特定のガイドラインが含まれます。  
  
 スクロール バー コントロールを使用すると、ユーザーは、ウィンドウまたは項目のコンテナー内のコンテンツをスクロールできます。 このコントロールは、ボタンのセットと Thumb コントロールから構成されます。  
  
 以下の各セクションで、ScrollBar コントロール型の必須の [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] ツリー構造、プロパティ、コントロール パターン、およびイベントを示します。 要件[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]は、Win32 または[!INCLUDE[TLA#tla_winclient](../../../includes/tlasharptla-winclient-md.md)]Windows フォームのいずれでも、すべてのリスト コントロールに適用されます。  
  
<a name="Required_UI_Automation_Tree_Structure"></a>
## <a name="required-ui-automation-tree-structure"></a>必須の UI オートメーション ツリー構造  
 次の表では、スクロール バー コントロールに関連する [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] ツリーのコントロール ビューとコンテンツ ビューを示し、それぞれのビューに含めることができる内容について説明します。 ツリーの詳細については、「 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] UI[オートメーション ツリーの概要](ui-automation-tree-overview.md)」を参照してください。  
  
|コントロール ビュー|コンテンツ ビュー|  
|------------------|------------------|  
|ScrollBar<br /><br /> - ボタン (2 または 4)<br />- 親指 (0 または 1)|適用不可。 スクロール バー コントロールは、コンテンツを含みません。|  
  
 スクロール バー コントロールは、常に 3 ～ 5 個の子を持っています。 サブツリーには複数のボタン コントロールが存在するため、各項目に特定の <xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationIdProperty> 値を設定して、それらの項目が自動テスト ツールで検出されるようにする必要があります。  
  
<a name="Required_UI_Automation_Properties"></a>
## <a name="required-ui-automation-properties"></a>必須の UI オートメーション プロパティ  
 次の表に、スクロール バー コントロールに特に関連する値または定義を持つ [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] プロパティを示します。 スクロール バー コントロールはコンテンツを持たないことに注意してください。このコントロールの機能は、スクロールされるコンテナーでサポートされる Scroll コントロール パターンによって公開されます。  
  
 プロパティの詳細[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]については、「[クライアントの UI オートメーション プロパティ 」](ui-automation-properties-for-clients.md)を参照してください。  
  
|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] プロパティ|Value|Notes|  
|------------------------------------------------------------------------------------|-----------|-----------|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationIdProperty>|「ノート」を参照してください。|このプロパティの値は、アプリケーション内のすべてのコントロールで一意である必要があります。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty>|「ノート」を参照してください。|コントロール全体を格納する最も外側の四角形。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsKeyboardFocusableProperty>|「ノート」を参照してください。|コントロールがキーボード フォーカスを受け取ることができる場合は、このプロパティをサポートする必要があります。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.NameProperty>|`Null`|スクロール バー コントロールはコンテンツ要素を持たないため、 `NameProperty` を設定する必要はありません。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ClickablePointProperty>|数値でない値。|スクロール バー コントロールには、クリック可能なポイントはありません。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LabeledByProperty>|`Null`|スクロール バーには、ラベルはありません。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ControlTypeProperty>|ScrollBar|この値は、すべてのフレームワークで同じです。 スライダーとして機能するスクロール バーには、Slider コントロール型を使用する必要があります。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LocalizedControlTypeProperty>|"スクロール バー"|Button コントロール型に対応するローカライズされた文字列。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsContentElementProperty>|False|スクロール バー コントロールは、コンテンツ要素ではありません。 スクロール バーがスタンドアロンのコントロールである場合、そのスクロール バーは、Slider コントロール型の機能を満たし、 `ControlType.Slider` プロパティの `ControlType` を返す必要があります。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsControlElementProperty>|True|スクロール バーは、常にコントロールである必要があります。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.OrientationProperty>|True|スクロール バー コントロールは、水平方向または垂直方向の向きを常に公開する必要があります。|  
  
<a name="Required_UI_Automation_Control_Patterns"></a>
## <a name="required-ui-automation-control-patterns"></a>必須の UI オートメーション コントロール パターン  
 次の表に、スクロール バー コントロールでサポートされなければならない [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] コントロール パターンを示します。 コントロール パターンの詳細については、「 [UI Automation Control Patterns Overview](ui-automation-control-patterns-overview.md)」を参照してください。 スクロール バーをマウス操作専用のコントロールとして使用する場合、スクロール バーはコントロール パターンをサポートしないことに注意してください。 スクロール バーをアプリケーション内のスライダー コントロールとして使用する場合は、Slider コントロール型にする必要があります。  
  
|コントロール パターン|サポート|Notes|  
|---------------------|-------------|-----------|  
|<xref:System.Windows.Automation.Provider.IScrollProvider>|なし|Scroll コントロール パターンは、スクロール バーで直接的にはサポートされていません。|  
|<xref:System.Windows.Automation.Provider.IRangeValueProvider>|依存|この機能は、スクロール バーのあるコンテナーで Scroll コントロール パターンがサポートされない場合に限ってサポートする必要があります。|  
  
<a name="Required_UI_Automation_Events"></a>
## <a name="required-ui-automation-events"></a>必須の UI オートメーション イベント  
 次の表に、すべてのスクロール バー コントロールでサポートされなければならない [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] イベントを示します。 イベントの詳細については、「 [UI Automation Events Overview](ui-automation-events-overview.md)」を参照してください。  
  
|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] イベント|サポート/値|Notes|  
|---------------------------------------------------------------------------------|--------------------|-----------|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty> プロパティ変更イベント。|Required|なし|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsOffscreenProperty> プロパティ変更イベント。|Required|なし|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty> プロパティ変更イベント。|Required|なし|  
|<xref:System.Windows.Automation.ScrollPatternIdentifiers.HorizontallyScrollableProperty> プロパティ変更イベント。|なし|なし|  
|<xref:System.Windows.Automation.ScrollPatternIdentifiers.HorizontalScrollPercentProperty> プロパティ変更イベント。|なし|なし|  
|<xref:System.Windows.Automation.ScrollPatternIdentifiers.HorizontalViewSizeProperty> プロパティ変更イベント。|なし|なし|  
|<xref:System.Windows.Automation.ScrollPatternIdentifiers.VerticalScrollPercentProperty> プロパティ変更イベント。|なし|なし|  
|<xref:System.Windows.Automation.ScrollPatternIdentifiers.VerticallyScrollableProperty> プロパティ変更イベント。|なし|なし|  
|<xref:System.Windows.Automation.ScrollPatternIdentifiers.VerticalViewSizeProperty> プロパティ変更イベント。|なし|なし|  
|<xref:System.Windows.Automation.RangeValuePatternIdentifiers.ValueProperty> プロパティ変更イベント。|依存|なし|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationFocusChangedEvent>|Required|なし|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.StructureChangedEvent>|Required|なし|  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Automation.ControlType.ScrollBar>
- [UI オートメーション コントロール型の概要](ui-automation-control-types-overview.md)
- [UI オートメーションの概要](ui-automation-overview.md)
