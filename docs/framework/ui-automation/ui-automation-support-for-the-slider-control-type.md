---
title: UI オートメーションによる Slider コントロール型のサポート
ms.date: 03/30/2017
helpviewer_keywords:
- control types, Slider
- UI Automation, Slider control type
- Slider control type
ms.assetid: 045ea62f-7b50-46cf-a5a9-8eb97704355f
ms.openlocfilehash: e59b46b3e159ae95ae15835e9b000e7db71c4ad9
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79179605"
---
# <a name="ui-automation-support-for-the-slider-control-type"></a>UI オートメーションによる Slider コントロール型のサポート
> [!NOTE]
> このドキュメントは、[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 名前空間で定義されているマネージド <xref:System.Windows.Automation> クラスを使用する .NET Framework 開発者を対象としています。 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]の最新情報については、「 [Windows Automation API: UI オートメーション](/windows/win32/winauto/entry-uiauto-win32)」をご覧ください。  
  
 このトピックでは、スライダー コントロール型の [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] サポートについて説明します。 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]でのコントロール型とは、コントロールが <xref:System.Windows.Automation.AutomationElement.ControlTypeProperty> プロパティを使用するために満たす必要がある一連の条件のことです。 条件には、 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] ツリー構造、 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] プロパティの値、コントロールの種類に関する特定のガイドラインが含まれます。  
  
 スライダー コントロールは、ボタンを使用した複合コントロールであり、ユーザーはこれらのボタンを使用して、マウスで数値の範囲を設定したり、項目のセットから選択したりできます。  
  
 以降のセクションで、スライダー コントロール型に必要な [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] ツリー構造、プロパティ、コントロール パターン、およびイベントを定義します。 要件[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]は、Win32 または[!INCLUDE[TLA#tla_winclient](../../../includes/tlasharptla-winclient-md.md)]Windows フォームのいずれでも、すべてのスライダー コントロールに適用されます。  
  
<a name="Required_UI_Automation_Tree_Structure"></a>
## <a name="required-ui-automation-tree-structure"></a>必須の UI オートメーション ツリー構造  
 次の表に、コントロール ビューと、スライダー コントロールに関連する [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] ツリーのコンテンツ ビューを示し、それぞれのビューに含めることができる内容について説明します。 ツリーの詳細については、「 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] UI[オートメーション ツリーの概要](ui-automation-tree-overview.md)」を参照してください。  
  
|コントロール ビュー|コンテンツ ビュー|  
|------------------|------------------|  
|スライダー<br /><br /> - ボタン (2 または 4)<br />- 親指(1つだけ)<br />- リストアイテム(0以上)|スライダー<br /><br /> - リストアイテム(0以上)|  
  
<a name="Required_UI_Automation_Properties"></a>
## <a name="required-ui-automation-properties"></a>必須の UI オートメーション プロパティ  
 次の表に、スライダー コントロール型に特に関連する値または定義を持つ [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] プロパティを示します。 プロパティの[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]詳細については、「[クライアントの UI オートメーション プロパティ 」](ui-automation-properties-for-clients.md)を参照してください。  
  
|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] プロパティ|Value|Notes|  
|------------------------------------------------------------------------------------|-----------|-----------|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationIdProperty>|「ノート」を参照してください。|このプロパティの値は、アプリケーション内のすべてのコントロールで一意である必要があります。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty>|「ノート」を参照してください。|コントロール全体を格納する最も外側の四角形。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ClickablePointProperty>|メモを参照|スライダー コントロールの四角形領域全体が子コントロールで占有されるため、スライダー コントロールの大多数は、 <xref:System.Windows.Automation.NoClickablePointException> を生成する必要があります。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsKeyboardFocusableProperty>|「ノート」を参照してください。|コントロールがキーボード フォーカスを受け取ることができる場合は、このプロパティをサポートする必要があります。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.NameProperty>|「ノート」を参照してください。|編集コントロールの名前は、通常、静的なテキスト ラベルから生成されます。 静的なテキスト ラベルがない場合は、アプリケーション開発者が `Name` のプロパティ値を割り当てる必要があります。 `Name` プロパティには、編集コントロールのテキスト コンテンツを含めることができません。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LabeledByProperty>|「ノート」を参照してください。|コントロールに関連付けられた静的なテキスト ラベルが存在する場合、このプロパティはそのコントロールへの参照を公開する必要があります。 テキスト コントロールが別のコントロールのサブコンポーネントの場合、 `LabeledBy` プロパティは設定されません。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ControlTypeProperty>|スライダー|この値は、すべての [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] フレームワークで同じです。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LocalizedControlTypeProperty>|「スライダー」|編集コントロール型に対応する、ローカライズされた文字列。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsContentElementProperty>|True|編集コントロールは、常に [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] ツリーのコンテンツ ビューに含まれます。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsControlElementProperty>|True|編集コントロールは、常に [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] ツリーのコントロール ビューに含まれます。|  
  
<a name="Required_UI_Automation_Control_Patterns"></a>
## <a name="required-ui-automation-control-patterns"></a>必須の UI オートメーション コントロール パターン  
 次の表に、すべてのスライダー コントロールでサポートされなければならない [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] コントロール パターンを示します。 コントロール パターンの詳細については、「 [UI Automation Control Patterns Overview](ui-automation-control-patterns-overview.md)」を参照してください。  
  
|コントロール パターン|サポート|Notes|  
|---------------------|-------------|-----------|  
|<xref:System.Windows.Automation.Provider.ISelectionProvider>|依存|コンテンツが個別のオプション セットのうちの 1 つの値を表す場合、スライダーは Selection コントロール パターンをサポートする必要があります。 Selection コントロール パターンがサポートされている場合、対応する選択を、スライダーの 1 つまたは複数の子リスト項目として公開する必要があります。|  
|<xref:System.Windows.Automation.Provider.IRangeValueProvider>|依存|コンテンツを数値の範囲内の値に設定できる場合、スライダーは RangeValue コントロール パターンをサポートする必要があります。|  
|<xref:System.Windows.Automation.Provider.IValueProvider>|依存|コンテンツが個別のオプション セットのうちの 1 つの値を表す場合、スライダーは Value コントロール パターンをサポートする必要があります。|  
  
<a name="Required_UI_Automation_Events"></a>
## <a name="required-ui-automation-events"></a>必須の UI オートメーション イベント  
 次の表に、すべてのスライダー コントロールでサポートされなければならない [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] イベントを示します。  
  
 イベントの詳細については、「 [UI Automation Events Overview](ui-automation-events-overview.md)」を参照してください。  
  
|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] イベント|サポート|Notes|  
|---------------------------------------------------------------------------------|-------------|-----------|  
|<xref:System.Windows.Automation.SelectionPatternIdentifiers.InvalidatedEvent>|依存|なし|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty> プロパティ変更イベント|Required|なし|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsOffscreenProperty> プロパティ変更イベント|Required|なし|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty> プロパティ変更イベント|Required|なし|  
|<xref:System.Windows.Automation.RangeValuePatternIdentifiers.ValueProperty> プロパティ変更イベント|依存|なし|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationFocusChangedEvent>|Required|なし|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.StructureChangedEvent>|Required|なし|  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Automation.ControlType.Slider>
- [UI オートメーション コントロール型の概要](ui-automation-control-types-overview.md)
- [UI オートメーションの概要](ui-automation-overview.md)
