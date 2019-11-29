---
title: UI オートメーションによる Edit コントロール型のサポート
ms.date: 03/30/2017
helpviewer_keywords:
- control types, Edit
- Edit control type
- UI Automation, Edit control type
ms.assetid: 6db9d231-c0a0-4e17-910e-ac80357f774f
ms.openlocfilehash: 500dc450ad171ed50316c8e08d62258d745049cb
ms.sourcegitcommit: 9a39f2a06f110c9c7ca54ba216900d038aa14ef3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/23/2019
ms.locfileid: "74448463"
---
# <a name="ui-automation-support-for-the-edit-control-type"></a>UI オートメーションによる Edit コントロール型のサポート

> [!NOTE]
> このドキュメントは、[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 名前空間で定義されているマネージド <xref:System.Windows.Automation> クラスを使用する .NET Framework 開発者を対象としています。 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]の最新情報については、「 [Windows Automation API: UI オートメーション](/windows/win32/winauto/entry-uiauto-win32)」を参照してください。

このトピックでは、Edit コントロール型に対する [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] のサポートについて説明します。 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]でのコントロール型とは、コントロールが <xref:System.Windows.Automation.AutomationElement.ControlTypeProperty> プロパティを使用するために満たす必要がある一連の条件のことです。 条件には、 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] ツリー構造、 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] プロパティの値、コントロール パターンに関する特定のガイドラインが含まれます。

編集コントロールを使用すると、さまざまな書式設定の機能をサポートしなくてもユーザーは単純なテキスト行を表示、および編集することができます。

以降のセクションで、Edit コントロール型に必要な [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] ツリー構造、プロパティ、コントロール パターン、イベントを定義します。 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] の要件は、 [!INCLUDE[TLA#tla_winclient](../../../includes/tlasharptla-winclient-md.md)]、 [!INCLUDE[TLA#tla_win32](../../../includes/tlasharptla-win32-md.md)]、 [!INCLUDE[TLA#tla_winforms](../../../includes/tlasharptla-winforms-md.md)]のいずれの場合でも、すべての編集コントロールに当てはまります。

<a name="Required_UI_Automation_Tree_Structure"></a>

## <a name="required-ui-automation-tree-structure"></a>必須の UI オートメーション ツリー構造

次の表に、編集コントロールに関連する [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] ツリーのコントロール ビューとコンテンツ ビューを示し、それぞれのビューに含めることができる内容について説明します。 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] ツリーの詳細については、「 [UI オートメーションツリーの概要](ui-automation-tree-overview.md)」を参照してください。

|コントロール ビュー|コンテンツ ビュー|
|------------------|------------------|
|編集|編集|

Edit コントロール型を実装するコントロールは単一行のコントロールであるため、 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] ツリーのコントロール ビューにスクロール バーは表示されません。 1 行のテキストは、一部のレイアウト シナリオでは折り返されることがあります。 Edit コントロール型は、編集可能または選択可能なテキストを少量保持するのに最適です。

<a name="Required_UI_Automation_Properties"></a>

## <a name="required-ui-automation-properties"></a>必須の UI オートメーション プロパティ

次の表に、編集コントロールに特に関連する値または定義を持つ [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] プロパティを示します。 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] のプロパティの詳細については、「[クライアントの UI オートメーションのプロパティ](ui-automation-properties-for-clients.md)」を参照してください。

|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] プロパティ|値|説明|
|------------------------------------------------------------------------------------|-----------|-----------|
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationIdProperty>|「ノート」を参照。|このプロパティの値は、アプリケーションのすべてのコントロールで一意である必要があります。|
|<xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty>|「ノート」を参照。|コントロール全体を格納する最も外側の四角形。|
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ClickablePointProperty>|「ノート」を参照。|編集コントロールには、ユーザーがその場所でマウスをクリックしたときに、コントロールの編集部分に入力フォーカスを設定する、クリック可能なポイントが必要です。|
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsKeyboardFocusableProperty>|「ノート」を参照。|コントロールがキーボード フォーカスを受け取ることができる場合は、このプロパティをサポートする必要があります。|
|<xref:System.Windows.Automation.AutomationElementIdentifiers.NameProperty>|「ノート」を参照。|編集コントロールの名前は、通常、静的なテキスト ラベルから生成されます。 静的なテキスト ラベルがない場合は、アプリケーション開発者が `Name` のプロパティ値を割り当てる必要があります。 `Name` プロパティには、編集コントロールのテキスト コンテンツを含めることができません。|
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LabeledByProperty>|「ノート」を参照。|コントロールに関連付けられた静的なテキスト ラベルが存在する場合、このプロパティはそのコントロールへの参照を公開する必要があります。 テキスト コントロールが別のコントロールのサブコンポーネントである場合、 `LabeledBy` プロパティは設定されません。|
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ControlTypeProperty>|編集|この値はすべての [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] フレームワークで同じです。|
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LocalizedControlTypeProperty>|"エディット"|Edit コントロール型に対応する、ローカライズされた文字列。|
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsContentElementProperty>|True|編集コントロールは、常に [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] ツリーのコンテンツ ビューに含まれます。|
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsControlElementProperty>|True|編集コントロールは、常に [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] ツリーのコントロール ビューに含まれます。|
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsPasswordProperty>|「ノート」を参照。|パスワードが含まれている編集コントロールの場合は true に設定する必要があります。 編集コントロールにパスワードのコンテンツが含まれる場合、スクリーン リーダーはこのプロパティを使用して、ユーザーが入力するキーストロークを読み上げる必要があるかどうかを判別できます。|

<a name="Required_UI_Automation_Control_Patterns"></a>

## <a name="required-ui-automation-control-patterns-and-properties"></a>必須の UI オートメーション コントロール パターンおよびプロパティ

次の表に、すべての編集コントロールでサポートする必要があるコントロール パターンの一覧を示します。 コントロール パターンについて詳しくは、「 [UI Automation Control Patterns Overview](ui-automation-control-patterns-overview.md)」をご覧ください。

|コントロール パターン/コントロール パターン プロパティ|サポート/値|説明|
|-----------------------------------------------|--------------------|-----------|
|<xref:System.Windows.Automation.Provider.ITextProvider>|依存|編集コントロールは、テキスト コントロール パターンをサポートする必要があります。これは、クライアントが常に詳しいテキスト情報を利用できるようにする必要があるためです。|
|<xref:System.Windows.Automation.Provider.IValueProvider>|依存|文字列を受け取るすべての編集コントロールは、Value パターンを公開する必要があります。|
|<xref:System.Windows.Automation.Provider.IValueProvider.IsReadOnly%2A>|「ノート」を参照。|コントロールがプログラムで値を設定できるか、それともユーザーが値を編集できるかを示すために、このプロパティを設定する必要があります。|
|<xref:System.Windows.Automation.Provider.IValueProvider.Value%2A>|「ノート」を参照。|このプロパティは、編集コントロールのテキスト コンテンツを返します。 `IsPasswordProperty` が `true`に設定されている場合、このプロパティは要求されたときに `InvalidOperationException` を発生させる必要があります。|
|<xref:System.Windows.Automation.Provider.IRangeValueProvider>|依存|数値の範囲を受け取るすべての編集コントロールは、Range Value コントロール パターンを公開する必要があります。|
|<xref:System.Windows.Automation.Provider.IRangeValueProvider.Minimum%2A>|「ノート」を参照。|このプロパティは、編集コントロールのコンテンツに対して設定できる最小値にする必要があります。|
|<xref:System.Windows.Automation.Provider.IRangeValueProvider.Maximum%2A>|「ノート」を参照。|このプロパティは、編集コントロールのコンテンツに対して設定できる最大値にする必要があります。|
|<xref:System.Windows.Automation.Provider.IRangeValueProvider.SmallChange%2A>|「ノート」を参照。|このプロパティは、値に対して設定できる小数点以下の桁数を示す必要があります。 エディットが整数のみを受け取る場合は、 `SmallChangeProperty` を 1 にする必要があります。 エディットが 1.0 ～ 2.0 の範囲を受け取る場合は、 `SmallChangeProperty` を 0.1 にする必要があります。 編集コントロールが 1.00 ～ 2.00 の範囲を受け取る場合は、 `SmallChangeProperty` を 0.001 にする必要があります。|
|<xref:System.Windows.Automation.Provider.IRangeValueProvider.LargeChange%2A>|`Null`|このプロパティは、編集コントロールで公開する必要はありません。|
|<xref:System.Windows.Automation.Provider.IRangeValueProvider.Value%2A>|「ノート」を参照。|このプロパティは、編集コントロールの数値コンテンツを示します。 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] および `Minimum` プロパティで指定された範囲内で `Maximum` クライアントによってより精度の高い値が設定された場合、Value プロパティは、受け入れ可能な値に最も近い値に自動的に丸められます。|

<a name="Required_UI_Automation_Events"></a>

## <a name="required-ui-automation-events"></a>必須の UI オートメーション イベント

次の表に、すべての編集コントロールでサポートする必要がある [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] イベントの一覧を示します。 イベントについて詳しくは、「 [UI Automation Events Overview](ui-automation-events-overview.md)」をご覧ください。

|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] イベント|サポート|説明|
|---------------------------------------------------------------------------------|-------------|-----------|
|<xref:System.Windows.Automation.SelectionPatternIdentifiers.InvalidatedEvent>|必須|なし|
|<xref:System.Windows.Automation.TextPatternIdentifiers.TextSelectionChangedEvent>|必須|なし|
|<xref:System.Windows.Automation.TextPatternIdentifiers.TextChangedEvent>|必須|なし|
|<xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty> プロパティ変更イベント。|必須|なし|
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsOffscreenProperty> プロパティ変更イベント。|必須|なし|
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty> プロパティ変更イベント。|必須|なし|
|<xref:System.Windows.Automation.AutomationElementIdentifiers.NameProperty> プロパティ変更イベント。|必須|なし|
|<xref:System.Windows.Automation.ValuePatternIdentifiers.ValueProperty> プロパティ変更イベント。|依存|なし|
|<xref:System.Windows.Automation.ScrollPatternIdentifiers.HorizontallyScrollableProperty> プロパティ変更イベント。|使用しない|なし|
|<xref:System.Windows.Automation.ScrollPatternIdentifiers.HorizontalScrollPercentProperty> プロパティ変更イベント。|使用しない|なし|
|<xref:System.Windows.Automation.ScrollPatternIdentifiers.HorizontalViewSizeProperty> プロパティ変更イベント。|使用しない|なし|
|<xref:System.Windows.Automation.ScrollPatternIdentifiers.VerticalScrollPercentProperty> プロパティ変更イベント。|使用しない|なし|
|<xref:System.Windows.Automation.ScrollPatternIdentifiers.VerticallyScrollableProperty> プロパティ変更イベント。|使用しない|なし|
|<xref:System.Windows.Automation.ScrollPatternIdentifiers.VerticalViewSizeProperty> プロパティ変更イベント。|使用しない|なし|
|<xref:System.Windows.Automation.RangeValuePatternIdentifiers.ValueProperty> プロパティ変更イベント。|依存|コントロールが Range Value コントロール パターンをサポートする場合は、このイベントをサポートする必要があります。|
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationFocusChangedEvent>|必須|なし|
|<xref:System.Windows.Automation.AutomationElementIdentifiers.StructureChangedEvent>|必須|なし|

## <a name="see-also"></a>参照

- <xref:System.Windows.Automation.ControlType.Edit>
- [UI オートメーション コントロール型の概要](ui-automation-control-types-overview.md)
- [UI オートメーションの概要](ui-automation-overview.md)
