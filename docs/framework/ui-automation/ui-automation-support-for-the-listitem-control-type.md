---
title: UI オートメーションによる ListItem コントロール型のサポート
ms.date: 03/30/2017
helpviewer_keywords:
- control types, List
- List Item control type
- UI Automation, List Item control type
ms.assetid: 34f533bf-fc14-4e78-8fee-fb7107345fab
ms.openlocfilehash: 245f9030897d54a2f1c95d5ce6369b67d23cb319
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79179701"
---
# <a name="ui-automation-support-for-the-listitem-control-type"></a>UI オートメーションによる ListItem コントロール型のサポート
> [!NOTE]
> このドキュメントは、[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 名前空間で定義されているマネージド <xref:System.Windows.Automation> クラスを使用する .NET Framework 開発者を対象としています。 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]の最新情報については、「 [Windows Automation API: UI オートメーション](/windows/win32/winauto/entry-uiauto-win32)」をご覧ください。  
  
 このトピックでは、 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] コントロール型に対する <xref:System.Windows.Automation.ControlType.ListItem> のサポートについて説明します。 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]でのコントロール型とは、コントロールが <xref:System.Windows.Automation.AutomationElement.ControlTypeProperty> プロパティを使用するために満たす必要がある一連の条件のことです。 これらの条件には、 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] ツリー構造、 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] のプロパティ値、およびコントロール パターンに関する特定のガイドラインが含まれます。  
  
 ListItem コントロール型を実装するコントロールの例として、リスト項目コントロールなどがあります。  
  
 以下の各セクションで、ListItem コントロール型に必要な [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] ツリー構造、プロパティ、コントロール パターン、およびイベントを定義します。 要件[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]は、Win32 または[!INCLUDE[TLA#tla_winclient](../../../includes/tlasharptla-winclient-md.md)]Windows フォームのいずれでも、すべてのリスト コントロールに適用されます。  
  
<a name="Required_UI_Automation_Tree_Structure"></a>
## <a name="required-ui-automation-tree-structure"></a>必須の UI オートメーション ツリー構造  
 次の表では、リスト項目コントロールに関連する [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] ツリーのコントロール ビューとコンテンツ ビューを示し、それぞれのビューに含めることができる内容について説明します。 ツリーの詳細については、「 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] UI[オートメーション ツリーの概要](ui-automation-tree-overview.md)」を参照してください。  
  
|コントロール ビュー|コンテンツ ビュー|  
|------------------|------------------|  
|ListItem<br /><br /> - 画像 (0 以上)<br />- テキスト (0 以上)<br />- 編集 (0 以上)|ListItem|  
  
 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] ツリーのコンテンツ ビュー内のリスト項目コントロールの子は、常に "0" である必要があります。 コントロールの構造がリスト項目の下に他の項目が含まれるような場合は[、TreeItem コントロール型コントロール](ui-automation-support-for-the-treeitem-control-type.md)の UI オートメーション サポートの要件に従う必要があります。  
  
<a name="Required_UI_Automation_Properties"></a>
## <a name="required-ui-automation-properties"></a>必須の UI オートメーション プロパティ  
 次の表に、リスト項目コントロールに特に関連する値または定義を持つ [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] プロパティを示します。 プロパティの[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]詳細については、「[クライアントの UI オートメーション プロパティ 」](ui-automation-properties-for-clients.md)を参照してください。  
  
|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] プロパティ|Value|Notes|  
|------------------------------------------------------------------------------------|-----------|-----------|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationIdProperty>|「ノート」を参照してください。|このプロパティの値は、アプリケーション内のすべてのコントロールで一意である必要があります。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty>|「ノート」を参照してください。|このプロパティのこの値には、リスト項目のイメージおよびテキスト コンテンツの領域を含める必要があります。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ClickablePointProperty>|依存|リスト コントロールにクリック可能なポイント (クリックするとリストがフォーカスを受け取るポイント) がある場合、このプロパティでそのポイントを公開する必要があります。 リスト コントロールが子孫のリスト項目に完全に覆われている場合は、クリック可能なポイントがないかリスト コントロール内の項目を調べる必要があることをクライアントに示すために、 <xref:System.Windows.Automation.NoClickablePointException> を生成します。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.NameProperty>|「ノート」を参照してください。|リスト項目コントロールの名前プロパティの値は、その項目のテキスト コンテンツから取得されます。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LabeledByProperty>|「ノート」を参照してください。|静的なテキスト ラベルがある場合、このプロパティは対象のコントロールへの参照を公開する必要があります。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ControlTypeProperty>|ListItem|この値は、すべての UI フレームワークで同じです。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LocalizedControlTypeProperty>|"リスト項目"|ListItem コントロール型に対応するローカライズされた文字列。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsContentElementProperty>|True|リスト コントロールは、常に [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] ツリーのコンテンツ ビューに含まれます。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsControlElementProperty>|True|リスト コントロールは、常に [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] ツリーのコントロール ビューに含まれます。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsKeyboardFocusableProperty>|True|コンテナーがキーボード入力を受け取ることができる場合、このプロパティ値は true である必要があります。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.HelpTextProperty>|""|リスト コントロールのヘルプ テキストは、オプションのリストから選択することをユーザーに求める理由を説明するものでなければなりません。一般には、ツールヒントに表示する情報と同様の内容になります。 たとえば、「項目を選択してモニターのディスプレイ解像度を設定してください」などです。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ItemTypeProperty>|依存|このプロパティは、基になるオブジェクトを表しているリスト項目コントロールに対して公開される必要があります。 そのようなリスト項目コントロールには、通常、ユーザーが基になるオブジェクトと関連付けたコントロールに関連付けられたアイコンがあります。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsOffscreenProperty>|依存|このプロパティは、そのリスト項目が現在、スクロール コントロール パターンを実装した親コンテナー内でスクロールして表示されているかどうかを示す値を返す必要があります。|  
  
<a name="Required_UI_Automation_Control_Patterns"></a>
## <a name="required-ui-automation-control-patterns"></a>必須の UI オートメーション コントロール パターン  
 次の表に、リスト項目コントロールでサポートされなければならない [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] コントロール パターンを示します。 コントロール パターンの詳細については、「 [UI Automation Control Patterns Overview](ui-automation-control-patterns-overview.md)」を参照してください。  
  
|コントロール パターン|サポート|Notes|  
|---------------------|-------------|-----------|  
|<xref:System.Windows.Automation.Provider.ISelectionItemProvider>|はい|リスト項目コントロールには、このコントロール パターンを実装する必要があります。 これにより、リスト項目コントロールは、選択されたことを伝達できます。|  
|<xref:System.Windows.Automation.Provider.IScrollItemProvider>|依存|このリスト項目がスクロール可能なコンテナーに格納されている場合には、このコントロール パターンを実装する必要があります。|  
|<xref:System.Windows.Automation.Provider.IToggleProvider>|依存|このリスト項目がチェック可能で、アクションによって選択状態の変更が実行されない場合には、このコントロール パターンを実装する必要があります。|  
|<xref:System.Windows.Automation.Provider.IExpandCollapseProvider>|依存|この項目を操作して情報を表示または非表示にできる場合は、このコントロール パターンを実装する必要があります。|  
|<xref:System.Windows.Automation.Provider.IValueProvider>|依存|この項目が編集可能である場合は、このコントロール パターンを実装する必要があります。 このリスト項目コントロールを変更すると、 <xref:System.Windows.Automation.AutomationElementIdentifiers.NameProperty>および <xref:System.Windows.Automation.Provider.IValueProvider.Value%2A>の値が変更されます。|  
|<xref:System.Windows.Automation.Provider.IGridItemProvider>|依存|リスト コンテナー内で項目間の空間的移動がサポートされており、コンテナーが行と列に配置されている場合は、グリッド項目コントロール パターンを実装する必要があります。|  
|<xref:System.Windows.Automation.Provider.IInvokeProvider>|依存|この項目に、この項目自体に対して実行できる選択以外のコマンドがある場合には、このパターンを実装する必要があります。 これは通常、リスト項目コントロールのダブルクリックに関連付けられたアクションです。 たとえば、エクスプローラからドキュメントを起動したり、Windows メディア プレーヤーで音楽ファイルを再生したりします。|  
  
<a name="Required_UI_Automation_Events"></a>
## <a name="required-ui-automation-events"></a>必須の UI オートメーション イベント  
 次の表に、すべてのリスト項目コントロールでサポートされなければならない [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] イベントを示します。 イベントの詳細については、「 [UI Automation Events Overview](ui-automation-events-overview.md)」を参照してください。  
  
|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] イベント|サポート|Notes|  
|---------------------------------------------------------------------------------|-------------|-----------|  
|<xref:System.Windows.Automation.InvokePatternIdentifiers.InvokedEvent>|依存|なし|  
|<xref:System.Windows.Automation.SelectionItemPatternIdentifiers.ElementAddedToSelectionEvent>|Required|なし|  
|<xref:System.Windows.Automation.SelectionItemPatternIdentifiers.ElementRemovedFromSelectionEvent>|Required|なし|  
|<xref:System.Windows.Automation.SelectionItemPatternIdentifiers.ElementSelectedEvent>|Required|なし|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty> プロパティ変更イベント。|Required|なし|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsOffscreenProperty> プロパティ変更イベント。|Required|なし|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty> プロパティ変更イベント。|Required|なし|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.NameProperty>|Required|なし|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ItemStatusProperty> プロパティ変更イベント。|依存|なし|  
|<xref:System.Windows.Automation.ExpandCollapsePatternIdentifiers.ExpandCollapseStateProperty> プロパティ変更イベント。|依存|なし|  
|<xref:System.Windows.Automation.ValuePatternIdentifiers.ValueProperty> プロパティ変更イベント。|依存|なし|  
|<xref:System.Windows.Automation.TogglePatternIdentifiers.ToggleStateProperty> プロパティ変更イベント。|依存|なし|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationFocusChangedEvent>|Required|なし|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.StructureChangedEvent>|Required|なし|  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Automation.ControlType.ListItem>
- [UI オートメーション コントロール型の概要](ui-automation-control-types-overview.md)
- [UI オートメーションの概要](ui-automation-overview.md)
