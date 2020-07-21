---
title: UI オートメーションによる List コントロール型のサポート
ms.date: 03/30/2017
helpviewer_keywords:
- control types, List
- List control type
- UI Automation, List control type
ms.assetid: 0e959fcb-50f2-413b-948d-7167d279bc11
ms.openlocfilehash: 2926e06cfbe065ad8a5bccdb7ebaf16596721def
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79179705"
---
# <a name="ui-automation-support-for-the-list-control-type"></a>UI オートメーションによる List コントロール型のサポート
> [!NOTE]
> このドキュメントは、[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 名前空間で定義されているマネージド <xref:System.Windows.Automation> クラスを使用する .NET Framework 開発者を対象としています。 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]の最新情報については、「 [Windows Automation API: UI オートメーション](/windows/win32/winauto/entry-uiauto-win32)」をご覧ください。  
  
 このトピックでは、List コントロール型に対する [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] のサポートについて説明します。 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]でのコントロール型とは、コントロールが <xref:System.Windows.Automation.AutomationElement.ControlTypeProperty> プロパティを使用するために満たす必要がある一連の条件のことです。 これらの条件には、 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] ツリー構造、 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] のプロパティ値、およびコントロール パターンに関する特定のガイドラインが含まれます。  
  
 List コントロール型を使用すると、項目のフラットなグループを編成して、ユーザーにそれらの項目から 1 つ以上選択させることができます。 List コントロール型には、含めることができる子要素の型に関する緩い制限があります。 これにより、UI オートメーション プロバイダーは選択コンテナーの既知の要素をサポートできます。  
  
 次[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]のセクションの要件は、リスト コントロールの種類を実装するすべてのコントロール[!INCLUDE[TLA#tla_winclient](../../../includes/tlasharptla-winclient-md.md)]に適用されます。 List コントロール型を実装するコントロールの例として、リスト コンテナー コントロールなどがあります。  
  
<a name="Required_UI_Automation_Tree_Structure"></a>
## <a name="required-ui-automation-tree-structure"></a>必須の UI オートメーション ツリー構造  
 次の表に、リスト コントロールに関連する [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] ツリーの 2 つのビューを示し、それぞれのビューに含めることができる内容について説明します。 コントロール ビューでは、コントロールである要素のみが表示されます。また、コンテンツ ビューでは、冗長な情報がツリーから除外されます。 たとえば、コンボ ボックスのラベルに使用されるテキスト コントロールは、 `ComboBox NameProperty`として公開されます。 このテキスト コントロールは、このようにコントロール ビューを介して既に公開されているため、2 回公開する必要はありません。したがって、コンテンツ ビューからは除外されます。 ツリーの詳細については、「 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] UI[オートメーション ツリーの概要](ui-automation-tree-overview.md)」を参照してください。  
  
|コントロール ビュー|コンテンツ ビュー|  
|------------------|------------------|  
|コントロールに対応する要素が含まれています。|支援技術がエンド ユーザーにとって意味のある最小限の情報を使用できるように、ツリーから冗長な情報を除外します。|  
|List<br /><br /> - データアイテム (0 以上)<br />- リストアイテム (0 以上)<br />- グループ (0 以上)<br />- スクロールバー (0、1 または 2)|List<br /><br /> - データアイテム (0 以上)<br />- リストアイテム (0 以上)<br />- グループ (0 以上)|  
  
 List コントロール型 (リスト コントロールなど) を実装するコントロールのコントロール ビューは以下で構成されます。  
  
- リスト コントロール内の 0 個以上の項目 (項目は、リスト 項目またはデータ項目コントロールの種類に基づいて指定できます)。
  
- リスト コントロール内の 0 個以上のグループ コントロール。
  
- 0、1、または 2 つのスクロール バー コントロール。
  
List コントロール型 (リスト コントロールなど) を実装するコントロールのコンテンツ ビューは以下で構成されます。  
  
- リスト コントロール内の 0 個以上の項目 (項目は、リスト 項目またはデータ項目コントロールの種類に基づいて指定できます)。
  
- リスト コントロール内の 0 個以上のグループ。

リスト コントロールには、一緒にグループ化されていない階層リレーションシップを持つ項目を含めることはできません。 項目が [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] ツリー内に子を持つ場合、リスト コンテナーは Tree コントロール型に基づく必要があります。  
  
 リスト コントロール内の選択可能項目は、リスト コントロールの [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] ツリーの子孫から取得できます。 リスト コントロール内のすべての項目は、同じ選択グループに属している必要があります。 リスト内の選択可能項目は ListItem (DataItem ではなく) コントロール型として公開する必要があります。  
  
<a name="Required_UI_Automation_Properties"></a>
## <a name="required-ui-automation-properties"></a>必須の UI オートメーション プロパティ  
 次の表に、リスト コントロールに特に関連する値または定義を持つ [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] プロパティを示します。 プロパティの[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]詳細については、「[クライアントの UI オートメーション プロパティ 」](ui-automation-properties-for-clients.md)を参照してください。  
  
|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] プロパティ|Value|Notes|  
|------------------------------------------------------------------------------------|-----------|-----------|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationIdProperty>|「ノート」を参照してください。|このプロパティの値は、アプリケーション内のすべてのコントロールで一意である必要があります。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty>|「ノート」を参照してください。|コントロール全体を格納する最も外側の四角形。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ClickablePointProperty>|「ノート」を参照してください。|リスト コントロールにクリック可能なポイント (クリックするとリストがフォーカスを受け取るポイント) がある場合、このプロパティでそのポイントを公開する必要があります。<br /><br /> `IsOffScreen`プロパティの値が true の場合は、<xref:System.Windows.Automation.NoClickablePointException>が発生します。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsKeyboardFocusableProperty>|「ノート」を参照してください。|コントロールがキーボード フォーカスを受け取ることができる場合は、このプロパティをサポートする必要があります。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.NameProperty>|「ノート」を参照してください。|リスト コントロールの Name プロパティ値は、ユーザーに選択を求めるオプションのカテゴリを表すものでなければなりません。 このプロパティの名前は、通常、静的なテキスト ラベルから取得されます。 静的なテキスト ラベルがない場合は、アプリケーション開発者が Name プロパティの値を公開する必要があります。<br /><br /> リスト コントロールでこのプロパティが不要になるのは、別のコントロールのサブツリー内でコントロールが使用される場合のみです。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LabeledByProperty>|「ノート」を参照してください。|静的なテキスト ラベルがある場合、このプロパティは対象のコントロールへの参照を公開する必要があります。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ControlTypeProperty>|List|この値は、すべての UI フレームワークで同じです。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LocalizedControlTypeProperty>|"リスト"|List コントロール型に対応する、ローカライズされた文字列。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsContentElementProperty>|True|リスト コントロールは、常に [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] ツリーのコンテンツ ビューに含まれます。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsControlElementProperty>|True|リスト コントロールは、常に [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] ツリーのコントロール ビューに含まれます。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsKeyboardFocusableProperty>|True|コンテナーがキーボード入力を受け取ることができる場合、このプロパティ値は true である必要があります。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.HelpTextProperty>|「ノート」を参照してください。|リスト コントロールのヘルプ テキストは、オプションのリストから選択することをユーザーに求める理由を説明するものでなければなりません。 たとえば、「項目を選択してモニターのディスプレイ解像度を設定してください」などです。|  
  
<a name="Required_UI_Automation_Control_Patterns"></a>
## <a name="required-ui-automation-control-patterns-and-properties"></a>必須の UI オートメーション コントロール パターンおよびプロパティ  
 次の表に、リスト コントロールでサポートされなければならない [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] コントロール パターンを示します。 コントロール パターンの詳細については、「 [UI Automation Control Patterns Overview](ui-automation-control-patterns-overview.md)」を参照してください。  
  
|コントロール パターン/パターン プロパティ|サポート/値|Notes|  
|---------------------------------------|--------------------|-----------|  
|<xref:System.Windows.Automation.Provider.ISelectionProvider>|Required|List コントロール型をサポートするすべてのコントロールは、コントロールに含まれている項目の間で選択状態が維持される場合に、 `ISelectionProvider` を実装する必要があります。 コンテナー内の項目が選択可能でない場合は、Group コントロール型を使用する必要があります。|  
|<xref:System.Windows.Automation.Provider.ISelectionProvider.IsSelectionRequired%2A>|依存|リスト コントロールでは、常に項目を選択する必要があるわけではありません。|  
|<xref:System.Windows.Automation.Provider.ISelectionProvider.CanSelectMultiple%2A>|依存|リスト コントロールでは、コンテナーを 1 つまたは複数選択できます。|  
|<xref:System.Windows.Automation.Provider.IScrollProvider>|依存|コンテナー内の項目がスクロール可能な場合は、このコントロール パターンを実装します。|  
|<xref:System.Windows.Automation.Provider.IGridProvider>|依存|グリッド ナビゲーションを項目ごとに使用可能にする必要がある場合は、このパターンを実装します。|  
|<xref:System.Windows.Automation.Provider.IMultipleViewProvider>|依存|コントロールがコンテナー内の項目の複数のビューをサポートできる場合は、このコントロール パターンを実装します。|  
|<xref:System.Windows.Automation.Provider.ITableProvider>|なし|`ITableProvider` は List コントロール型をサポートしません。 コントロールがこのコントロール パターンをサポートする必要がある場合、コントロールは Data Grid コントロール型に基づく必要があります。|  
  
<a name="Required_UI_Automation_Events"></a>
## <a name="required-ui-automation-events"></a>必須の UI オートメーション イベント  
 次の表に、すべてのリスト コントロールでサポートされなければならない [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] イベントを示します。 イベントの詳細については、「 [UI Automation Events Overview](ui-automation-events-overview.md)」を参照してください。  
  
|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] イベント|サポート/値|Notes|  
|---------------------------------------------------------------------------------|--------------------|-----------|  
|<xref:System.Windows.Automation.SelectionPatternIdentifiers.InvalidatedEvent>|依存|なし|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LayoutInvalidatedEvent>|依存|なし|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty> プロパティ変更イベント。|Required|なし|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsOffscreenProperty> プロパティ変更イベント。|Required|なし|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty> プロパティ変更イベント。|Required|なし|  
|<xref:System.Windows.Automation.MultipleViewPatternIdentifiers.CurrentViewProperty> プロパティ変更イベント。|依存|なし|  
|<xref:System.Windows.Automation.ScrollPatternIdentifiers.HorizontallyScrollableProperty> プロパティ変更イベント。|依存|なし|  
|<xref:System.Windows.Automation.ScrollPatternIdentifiers.HorizontalScrollPercentProperty> プロパティ変更イベント。|依存|なし|  
|<xref:System.Windows.Automation.ScrollPatternIdentifiers.HorizontalViewSizeProperty> プロパティ変更イベント。|依存|なし|  
|<xref:System.Windows.Automation.ScrollPatternIdentifiers.VerticalScrollPercentProperty> プロパティ変更イベント。|依存|なし|  
|<xref:System.Windows.Automation.ScrollPatternIdentifiers.VerticallyScrollableProperty> プロパティ変更イベント。|依存|なし|  
|<xref:System.Windows.Automation.ScrollPatternIdentifiers.VerticalViewSizeProperty> プロパティ変更イベント。|依存|なし|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationFocusChangedEvent>|Required|なし|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.StructureChangedEvent>|Required|なし|  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Automation.ControlType.List>
- [UI オートメーション コントロール型の概要](ui-automation-control-types-overview.md)
- [UI オートメーションの概要](ui-automation-overview.md)
