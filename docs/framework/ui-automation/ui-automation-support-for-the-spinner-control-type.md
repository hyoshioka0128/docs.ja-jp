---
title: UI オートメーションによる Spinner コントロール型のサポート
ms.date: 03/30/2017
helpviewer_keywords:
- UI Automation, Spinner control type
- Spinner control type
- control types, Spinner
ms.assetid: 3a29d185-65d8-42e3-bcc3-7f43e96f40c5
ms.openlocfilehash: d3cf972afdaaffaf1c0943c9cc11348bee23345d
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79179581"
---
# <a name="ui-automation-support-for-the-spinner-control-type"></a>UI オートメーションによる Spinner コントロール型のサポート
> [!NOTE]
> このドキュメントは、[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 名前空間で定義されているマネージド <xref:System.Windows.Automation> クラスを使用する .NET Framework 開発者を対象としています。 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]の最新情報については、「 [Windows Automation API: UI オートメーション](/windows/win32/winauto/entry-uiauto-win32)」をご覧ください。  
  
 このトピックでは、Spinner コントロール型の [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] サポートについて説明します。 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]でのコントロール型とは、コントロールが <xref:System.Windows.Automation.AutomationElement.ControlTypeProperty> プロパティを使用するために満たす必要がある一連の条件のことです。 これらの条件には、 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] ツリー構造、 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] のプロパティ値、およびコントロール パターンに関する特定のガイドラインが含まれます。  
  
 スピン ボタン コントロールは、ある範囲の項目や数字から選択するために使用します。  
  
 以降のセクションでは、Spinner コントロール型に必要な [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] ツリー構造、プロパティ、コントロール パターン、およびイベントを定義します。 要件[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]は、すべてのスピン コントロール 、Win32、または Windows フォームに[!INCLUDE[TLA#tla_winclient](../../../includes/tlasharptla-winclient-md.md)]適用されます。  
  
<a name="Required_UI_Automation_Tree_Structure"></a>
## <a name="required-ui-automation-tree-structure"></a>必須の UI オートメーション ツリー構造  
 次の表に、Range Value、Value、および Selection の各コントロール パターンをサポートするスピン ボタン コントロールに関連する [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] ツリーのコントロール ビューとコンテンツ ビューを示し、各ビューに格納できるものについて説明します。 ツリーの詳細については、「 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] UI[オートメーション ツリーの概要](ui-automation-tree-overview.md)」を参照してください。  
  
 **Range Value コントロール パターンまたは Value コントロール パターン**  
  
|コントロール ビュー|コンテンツ ビュー|  
|------------------|------------------|  
|Spinner<br /><br /> - 編集 (0 または 1)<br />- ボタン (2)|Spinner|  
  
 **Selection コントロール パターン**  
  
|コントロール ビュー|コンテンツ ビュー|  
|------------------|------------------|  
|Spinner<br /><br /> - 編集 (0 または 1)<br />- ボタン (2)<br />- リストアイテム(0以上)|Spinner<br /><br /> - リストアイテム (0 以上)|  
  
 コントロール ビュー サブツリーの 2 つのボタンを自動テスト ツールが区別できるようにするには、必要に応じて `SmallIncrement` または `SmallDecrement` `AutomationId` を割り当てます。 実装によっては、関連付けられたエディット コントロールが Spinner コントロールのピアである場合があります。  
  
<a name="Required_UI_Automation_Properties"></a>
## <a name="required-ui-automation-properties"></a>必須の UI オートメーション プロパティ  
 次の表に、スピン ボタン コントロールに特に関連する値または定義を持つ [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] プロパティを示します。 プロパティの[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]詳細については、「[クライアントの UI オートメーション プロパティ 」](ui-automation-properties-for-clients.md)を参照してください。  
  
|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] プロパティ|Value|Notes|  
|------------------------------------------------------------------------------------|-----------|-----------|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationIdProperty>|「ノート」を参照してください。|このプロパティの値は、アプリケーション内のすべてのコントロールで一意である必要があります。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty>|「ノート」を参照してください。|コントロール全体を格納する最も外側の四角形。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ClickablePointProperty>|「ノート」を参照してください。|スピン ボタン コントロールのクリック可能なポイントは、コントロールの編集部分にフォーカスを設定します。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsKeyboardFocusableProperty>|「ノート」を参照してください。|コントロールがキーボード フォーカスを受け取ることができる場合は、このプロパティをサポートする必要があります。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.NameProperty>|「ノート」を参照してください。|スピン ボタン コントロールは、通常、静的テキスト ラベルからその名前を取得します。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LabeledByProperty>|「ノート」を参照してください。|スピン ボタン コントロールには静的なテキスト ラベルがあります。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ControlTypeProperty>|Spinner|この値は、すべての UI フレームワークで同じです。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LocalizedControlTypeProperty>|"スピン ボタン"|Spinner コントロール型に対応する、ローカライズされた文字列。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsContentElementProperty>|True|スピン ボタン コントロールは、常にコンテンツである必要があります。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsControlElementProperty>|True|Spinner コントロールは、常にコントロールである必要があります。|  
  
<a name="Required_UI_Automation_Control_Patterns_and_Properties"></a>
## <a name="required-ui-automation-control-patterns-and-properties"></a>必須の UI オートメーション コントロール パターンおよびプロパティ  
 次の表に、スピン ボタン コントロールでサポートする必要がある [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] コントロール パターンを示します。 コントロール パターンについて詳しくは、「 [UI Automation Control Patterns Overview](ui-automation-control-patterns-overview.md)」をご覧ください。  
  
|コントロール パターン/パターン プロパティ|サポート/値|Notes|  
|---------------------------------------|--------------------|-----------|  
|<xref:System.Windows.Automation.Provider.ISelectionProvider>|依存|選択する項目のリストを持つスピン ボタン コントロールは、このパターンをサポートする必要があります。|  
|<xref:System.Windows.Automation.Provider.ISelectionProvider.CanSelectMultiple%2A>|False|スピン ボタン コントロールは、常に単一選択コンテナーです。|  
|<xref:System.Windows.Automation.Provider.IRangeValueProvider>|依存|数値の範囲を対象にするスピン ボタン コントロールは、このパターンをサポートできます。|  
|<xref:System.Windows.Automation.Provider.IValueProvider>|依存|個別のオプション セットまたは数値のセットを対象にするスピン ボタン コントロールは、このパターンをサポートできます。|  
  
<a name="Required_UI_Automation_Events"></a>
## <a name="required-ui-automation-events"></a>必須の UI オートメーション イベント  
 次の表に、すべてのスピン ボタン コントロールでサポートする必要がある [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] イベントを示します。 イベントの詳細については、「 [UI Automation Events Overview](ui-automation-events-overview.md)」を参照してください。  
  
|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] イベント|サポート|Notes|  
|---------------------------------------------------------------------------------|-------------|-----------|  
|<xref:System.Windows.Automation.SelectionPatternIdentifiers.InvalidatedEvent>|依存|なし|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty> プロパティ変更イベント。|Required|なし|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsOffscreenProperty> プロパティ変更イベント。|Required|なし|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty> プロパティ変更イベント。|Required|なし|  
|<xref:System.Windows.Automation.ValuePatternIdentifiers.ValueProperty> プロパティ変更イベント。|依存|なし|  
|<xref:System.Windows.Automation.RangeValuePatternIdentifiers.ValueProperty> プロパティ変更イベント。|依存|なし|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationFocusChangedEvent>|Required|なし|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.StructureChangedEvent>|Required|なし|  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Automation.ControlType.Spinner>
- [UI オートメーション コントロール型の概要](ui-automation-control-types-overview.md)
- [UI オートメーションの概要](ui-automation-overview.md)
