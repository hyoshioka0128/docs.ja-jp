---
title: UI オートメーションによる MenuBar コントロール型のサポート
ms.date: 03/30/2017
helpviewer_keywords:
- UI Automation, Menu Bar control type
- control types, Menu Bar
- Menu Bar control type
ms.assetid: c1202b21-c1f0-4560-853c-7b99bd73ad97
ms.openlocfilehash: c50c5abb450ae44fcc08507354ea73f3a780afdf
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79179651"
---
# <a name="ui-automation-support-for-the-menubar-control-type"></a>UI オートメーションによる MenuBar コントロール型のサポート
> [!NOTE]
> このドキュメントは、[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 名前空間で定義されているマネージド <xref:System.Windows.Automation> クラスを使用する .NET Framework 開発者を対象としています。 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]の最新情報については、「 [Windows Automation API: UI オートメーション](/windows/win32/winauto/entry-uiauto-win32)」をご覧ください。  
  
 このトピックでは、 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] コントロール型に対する <xref:System.Windows.Automation.ControlType.MenuBar> のサポートについて説明します。 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]でのコントロール型とは、コントロールが <xref:System.Windows.Automation.AutomationElement.ControlTypeProperty> プロパティを使用するために満たす必要がある一連の条件のことです。 これらの条件には、 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] ツリー構造、 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] のプロパティ値、およびコントロール パターンに関する特定のガイドラインが含まれます。  
  
 MenuBar コントロール型を実装するコントロールの例には、メニュー バー コントロールがあります。 メニュー バーは、ユーザーがアプリケーションに含まれるコマンドおよびオプションをアクティブにするための手段を提供します。  
  
 以降のセクションで、MenuBar コントロール型に必要な [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] ツリー構造、プロパティ、コントロール パターン、およびイベントを定義します。 要件[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]は、Win32 または[!INCLUDE[TLA#tla_winclient](../../../includes/tlasharptla-winclient-md.md)]Windows フォームのいずれでも、すべてのリスト コントロールに適用されます。  
  
<a name="Required_UI_Automation_Tree_Structure"></a>
## <a name="required-ui-automation-tree-structure"></a>必須の UI オートメーション ツリー構造  
 次の表に、コントロール ビューと、メニュー バー コントロールに関連する [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] ツリーのコンテンツ ビューを示し、それぞれのビューに含めることができる内容について説明します。 ツリーの詳細については、「 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] UI[オートメーション ツリーの概要](ui-automation-tree-overview.md)」を参照してください。  
  
|コントロール ビュー|コンテンツ ビュー|  
|------------------|------------------|  
|メニュー バー<br /><br /> - メニュー項目 (1 以上)<br />- その他のコントロール (0 または多)|メニュー バー<br /><br /> - メニュー項目 (1 以上)<br />- その他のコントロール (0 または多)|  
  
 メニュー バー コントロールの構造には、エディット コントロールやコンボ ボックスなどの他のコントロールを含めることができます。 これらの追加コントロールは、コントロール ビューおよびコンテンツ ビューに含まれる、上記に一覧した「その他のコントロール」に対応します。  
  
<a name="Required_UI_Automation_Properties"></a>
## <a name="required-ui-automation-properties"></a>必須の UI オートメーション プロパティ  
 次の表に、メニュー バー コントロールに特に関連する値または定義を持つ [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] プロパティを示します。 プロパティの[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]詳細については、「[クライアントの UI オートメーション プロパティ 」](ui-automation-properties-for-clients.md)を参照してください。  
  
|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] プロパティ|Value|Notes|  
|------------------------------------------------------------------------------------|-----------|-----------|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty>|「ノート」を参照してください。|このプロパティで公開する値には、メニュー バー コントロールに含まれるすべてのコントロールを含める必要があります。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.NameProperty>|「ノート」を参照してください。|アプリケーションに複数のメニュー バーがある場合を除き、メニュー バー コントロールに名前は必要ありません。 アプリケーションに複数のメニュー バーがある場合、このプロパティを使用して、「書式設定」や「アウトライン」といった識別名を公開する必要があります|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LabeledByProperty>|`Null`|メニュー バー コントロールには例外なく、ラベルはありません。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ControlTypeProperty>|メニュー バー|この値は、すべての UI フレームワークで同じです。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LocalizedControlTypeProperty>|「メニュー バー」|MenuBar コントロール型に対応する、ローカライズされた文字列。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsContentElementProperty>|True|メニュー バー コントロールは、常に [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] ツリーのコンテンツ ビューに組み込まれます。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsControlElementProperty>|True|メニュー バー コントロールは、常に [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] ツリーのコントロール ビューに組み込まれます。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsOffscreenProperty>|「ノート」を参照してください。|このプロパティの値は、コントロールを画面に表示できるかどうかによって異なります。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.OrientationProperty>|依存|このプロパティは、メニュー バー コントロールが水平または垂直のいずれかであるかを公開します。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsKeyboardFocusableProperty>|True|メニュー バー コントロールに含まれるコントロールはキーボード フォーカスを受け取ることができるため、メニュー バー コントロールはキーボード フォーカスを受け取ることができます。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.HelpTextProperty>|「ノート」を参照してください。|メニュー バー コントロールにヘルプ テキストが必要になるシナリオはありません。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AcceleratorKeyProperty>|`Null`|メニュー バーでアクセラレータ キーを使用することは決してありません。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AccessKeyProperty>|「ALT」|ALT キーを押すと常に、アプリケーション内のメニュー バーにフォーカスが移動します。|  
  
<a name="Required_UI_Automation_Control_Patterns"></a>
## <a name="required-ui-automation-control-patterns"></a>必須の UI オートメーション コントロール パターン  
 次の表に、メニュー バー コントロールでサポートされなければならない [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] コントロール パターンを示します。 コントロール パターンの詳細については、「 [UI Automation Control Patterns Overview](ui-automation-control-patterns-overview.md)」を参照してください。  
  
|コントロール パターン|サポート|Notes|  
|---------------------|-------------|-----------|  
|<xref:System.Windows.Automation.Provider.IExpandCollapseProvider>|依存|コントロールを展開または折りたたむことができる場合は、 <xref:System.Windows.Automation.Provider.IExpandCollapseProvider>を実装します。|  
|<xref:System.Windows.Automation.Provider.IDockProvider>|依存|コントロールを画面のさまざまな部分にドッキングできる場合は、 <xref:System.Windows.Automation.Provider.IDockProvider>を実装します。|  
|<xref:System.Windows.Automation.Provider.ITransformProvider>|依存|コントロールのサイズ変更、回転、移動が可能な場合は、 <xref:System.Windows.Automation.Provider.ITransformProvider>を実装する必要があります。|  
  
<a name="Required_UI_Automation_Events"></a>
## <a name="required-ui-automation-events"></a>必須の UI オートメーション イベント  
 次の表に、すべてのメニュー バー コントロールでサポートされなければならない [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] イベントを示します。 イベントの詳細については、「 [UI Automation Events Overview](ui-automation-events-overview.md)」を参照してください。  
  
|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] イベント|サポート/値|Notes|  
|---------------------------------------------------------------------------------|--------------------|-----------|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty> プロパティ変更イベント。|Required|なし|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsOffscreenProperty> プロパティ変更イベント。|Required|なし|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty> プロパティ変更イベント。|Required|なし|  
|<xref:System.Windows.Automation.ExpandCollapsePatternIdentifiers.ExpandCollapseStateProperty> プロパティ変更イベント。|依存|なし|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationFocusChangedEvent>|Required|なし|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.StructureChangedEvent>|Required|なし|  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Automation.ControlType.MenuBar>
- [UI オートメーション コントロール型の概要](ui-automation-control-types-overview.md)
- [UI オートメーションの概要](ui-automation-overview.md)
