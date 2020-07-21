---
title: UI オートメーションによる Tree コントロール型のサポート
ms.date: 03/30/2017
helpviewer_keywords:
- control types, Tree
- Tree control type
- UI Automation, Tree control type
ms.assetid: 312dd04d-a86b-4072-8b12-2beeabdff5e3
ms.openlocfilehash: 389506bed91d26288e9fe2ce84c00dfb27e821b2
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79179439"
---
# <a name="ui-automation-support-for-the-tree-control-type"></a>UI オートメーションによる Tree コントロール型のサポート
> [!NOTE]
> このドキュメントは、[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 名前空間で定義されているマネージド <xref:System.Windows.Automation> クラスを使用する .NET Framework 開発者を対象としています。 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]の最新情報については、「 [Windows Automation API: UI オートメーション](/windows/win32/winauto/entry-uiauto-win32)」をご覧ください。  
  
 このトピックでは、Tree コントロール型に対する [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] のサポートについて説明します。 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]でのコントロール型とは、コントロールが <xref:System.Windows.Automation.AutomationElement.ControlTypeProperty> プロパティを使用するために満たす必要がある一連の条件のことです。 これらの条件には、 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] ツリー構造、 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] のプロパティ値、およびコントロール パターンに関する特定のガイドラインが含まれます。  
  
 Tree コントロールの種類は、ファイルやフォルダーが Microsoft Windows エクスプローラーの左側のウィンドウに表示される方法と同様に、ノードの階層として関連性のある内容を持つコンテナーに使用されます。 各ノードに、子ノードと呼ばれる他のノードが含まれている可能性があります。 親ノード (子ノードを含むノード) は、展開した状態または折りたたんだ状態で表示できます。  
  
 以下の各セクションで、Tree コントロール型に必要な [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] ツリー構造、プロパティ、コントロール パターン、およびイベントを定義します。 要件[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]は、Win32 または[!INCLUDE[TLA#tla_winclient](../../../includes/tlasharptla-winclient-md.md)]Windows フォームのいずれでも、すべてのツリー コントロールに適用されます。  
  
<a name="Required_UI_Automation_Tree_Structure"></a>
## <a name="required-ui-automation-tree-structure"></a>必須の UI オートメーション ツリー構造  
 次の表に、ツリー コントロールに関連する [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] ツリーのコントロール ビューとコンテンツ ビューを示し、それぞれのビューに含めることができる内容について説明します。 ツリーの詳細については、「 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] UI[オートメーション ツリーの概要](ui-automation-tree-overview.md)」を参照してください。  
  
|コントロール ビュー|コンテンツ ビュー|  
|------------------|------------------|  
|ツリー<br /><br /> <ul><li>DataItem (0 以上)</li><li>TreeItem (0 以上)<br /><br /> <ul><li>TreeItem (0 以上)•    …</li></ul></li><li>ScrollBar (0、1、2)</li></ul>|ツリー<br /><br /> <ul><li>DataItem (0 以上)</li><li>TreeItem (0 以上)<br /><br /> <ul><li>TreeItem (0 以上)•    …</li></ul></li></ul>|  
  
 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] ツリーのコントロール ビューは、次のものから構成されます。  
  
- コンテナー内の 0 個以上の項目 (項目は、Tree Item コントロール型、Data Item コントロール型、またはその他のコントロール型に基づいて設定できます)。  
  
- 0、1、または 2 個のスクロール バー。  
  
 コンテンツ ビューの [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] ツリーは、コンテナー内の 0 個以上の項目から構成されます (項目は、TreeItem コントロール型、DataItem コントロール型、またはその他のコントロール型に基づいている可能性があります)。  
  
<a name="Required_UI_Automation_Properties"></a>
## <a name="required-ui-automation-properties"></a>必須の UI オートメーション プロパティ  
 次の表に、リスト コントロールに特に関連する値または定義を持つ [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] プロパティを示します。 プロパティの詳細[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]については、「[クライアントの UI オートメーション プロパティ 」](ui-automation-properties-for-clients.md)を参照してください。  
  
|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] プロパティ|Value|Notes|  
|------------------------------------------------------------------------------------|-----------|-----------|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationIdProperty>|「ノート」を参照してください。|このプロパティの値は、アプリケーション内のすべてのコントロールで一意である必要があります。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty>|「ノート」を参照してください。|コントロール全体を格納する最も外側の四角形。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ClickablePointProperty>|「ノート」を参照してください。|ツリー コントロールには、クリックするとツリーまたはツリー コンテナー内の 1 つの項目にフォーカスが設定される、クリック可能なポイントがあります。 ツリーのクリック可能なポイントを取得するのは、項目を 1 つ選択したり項目にフォーカスを設定したりすることなくクリックできる場所がある場合に限られます。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ControlTypeProperty>|ツリー|この値は、すべての UI フレームワークで同じです。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsContentElementProperty>|True|ツリー コントロールは、常に [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] ツリーのコンテンツ ビューに含まれます。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsControlElementProperty>|True|ツリー コントロールは、常に [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] ツリーのコントロール ビューに含まれます。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsKeyboardFocusableProperty>|「ノート」を参照してください。|コントロールがキーボード フォーカスを受け取ることができる場合は、このプロパティをサポートする必要があります。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LabeledByProperty>|「ノート」を参照してください。|ツリー コントロールにラベルが関連付けられている場合、このプロパティはそのラベルの <xref:System.Windows.Automation.AutomationElement> を返します。 それ以外の場合、プロパティは Null`Nothing`参照を返します ( .NET では) 。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LocalizedControlTypeProperty>|"ツリー"|List コントロール型に対応する、ローカライズされた文字列。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.NameProperty>|「ノート」を参照してください。|ツリー コントロールの名前プロパティの値は、通常、コントロールにラベルを付けるテキストから取得されます。 テキスト ラベルが存在しない場合は、アプリケーションの開発者がこのプロパティの値を提供する必要があります。|  
  
<a name="Required_UI_Automation_Control_Patterns"></a>
## <a name="required-ui-automation-control-patterns"></a>必須の UI オートメーション コントロール パターン  
 次の表に、リスト コントロールでサポートされなければならない [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] コントロール パターンを示します。 コントロール パターンの詳細については、「 [UI Automation Control Patterns Overview](ui-automation-control-patterns-overview.md)」を参照してください。  
  
|コントロール パターン/パターン プロパティ|サポート/値|Notes|  
|---------------------------------------|--------------------|-----------|  
|<xref:System.Windows.Automation.Provider.ISelectionProvider>|依存|選択可能な一連の項目を含むツリー コントロールは、このコントロール パターンを実装する必要があります。 項目を選択してもユーザーに意味のある情報が伝達されない場合は、このコントロール パターンを実装する必要はありません。|  
|<xref:System.Windows.Automation.Provider.ISelectionProvider.CanSelectMultiple%2A>|「ノート」を参照してください。|ツリー コントロールが複数選択をサポートする場合、このプロパティを実装します (ほとんどのツリー コントロールは、複数選択をサポートしません)。|  
|<xref:System.Windows.Automation.Provider.ISelectionProvider.IsSelectionRequired%2A>|「ノート」を参照してください。|このプロパティの値は、コントロールで項目が選択される必要がある場合に公開されます。|  
|<xref:System.Windows.Automation.Provider.IScrollProvider>|依存|ツリー コンテナーのコンテンツがスクロールできる場合は、このコントロール パターンを実装します。|  
  
<a name="Required_UI_Automation_Events"></a>
## <a name="required-ui-automation-events"></a>必須の UI オートメーション イベント  
 次の表に、すべてのツリー コントロールでサポートされなければならない [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] イベントを示します。 イベントの詳細については、「 [UI Automation Events Overview](ui-automation-events-overview.md)」を参照してください。  
  
|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] イベント|サポート|Notes|  
|---------------------------------------------------------------------------------|-------------|-----------|  
|<xref:System.Windows.Automation.SelectionPatternIdentifiers.InvalidatedEvent>|依存|なし|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty> プロパティ変更イベント。|Required|なし|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsOffscreenProperty> プロパティ変更イベント。|Required|なし|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty> プロパティ変更イベント。|Required|なし|  
|<xref:System.Windows.Automation.ScrollPatternIdentifiers.HorizontallyScrollableProperty> プロパティ変更イベント。|依存|なし|  
|<xref:System.Windows.Automation.ScrollPatternIdentifiers.HorizontalScrollPercentProperty> プロパティ変更イベント。|依存|なし|  
|<xref:System.Windows.Automation.ScrollPatternIdentifiers.HorizontalViewSizeProperty> プロパティ変更イベント。|依存|なし|  
|<xref:System.Windows.Automation.ScrollPatternIdentifiers.VerticalScrollPercentProperty> プロパティ変更イベント。|依存|なし|  
|<xref:System.Windows.Automation.ScrollPatternIdentifiers.VerticallyScrollableProperty> プロパティ変更イベント。|依存|なし|  
|<xref:System.Windows.Automation.ScrollPatternIdentifiers.VerticalViewSizeProperty> プロパティ変更イベント。|依存|なし|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationFocusChangedEvent>|Required|なし|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.StructureChangedEvent>|Required|なし|  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Automation.ControlType.Tree>
- [UI オートメーション コントロール型の概要](ui-automation-control-types-overview.md)
- [UI オートメーションの概要](ui-automation-overview.md)
