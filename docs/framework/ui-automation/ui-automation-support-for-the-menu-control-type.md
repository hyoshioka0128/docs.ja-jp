---
title: UI オートメーションによる Menu コントロール型のサポート
ms.date: 03/30/2017
helpviewer_keywords:
- control types, Menu
- UI Automation, Menu control type
- Menu control type
ms.assetid: 016323cb-f800-4938-b77b-2eb25d646090
ms.openlocfilehash: 3e3177f682ad75f4673870a72aee6d86c7b5ab60
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79179683"
---
# <a name="ui-automation-support-for-the-menu-control-type"></a>UI オートメーションによる Menu コントロール型のサポート
> [!NOTE]
> このドキュメントは、[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 名前空間で定義されているマネージド <xref:System.Windows.Automation> クラスを使用する .NET Framework 開発者を対象としています。 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]の最新情報については、「 [Windows Automation API: UI オートメーション](/windows/win32/winauto/entry-uiauto-win32)」をご覧ください。  
  
 このトピックでは、Menu コントロール型の [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] サポートについて説明します。 このコントロールの [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] ツリー構造を説明し、特定のコントロール シナリオでのプロパティとコントロール パターンを示します。  
  
 メニュー コントロールを使用すると、コマンドおよびイベント ハンドラーに関連付けられている要素を階層に編成できます。 一般的な Microsoft Windows アプリケーションでは、メニュー バーに複数のメニュー ボタン **([ファイル]、[****編集**]、[**ウィンドウ**]など) が表示され、各メニュー ボタンにはメニューが表示されます。 メニューには、メニュー項目 ( **[新規]**、 **[開く]**、 **[閉じる]** など) のコレクションが含まれていて、メニュー項目を展開して追加のメニュー項目を表示したり、クリックして特定の操作を実行したりできます。  
  
 以降のセクションで、Menu コントロール型に必要な [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] ツリー構造、プロパティ、コントロール パターン、およびイベントを定義します。 要件[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]は、Win32 または[!INCLUDE[TLA#tla_winclient](../../../includes/tlasharptla-winclient-md.md)]Windows フォームのいずれでも、すべてのリスト コントロールに適用されます。  
  
<a name="Required_UI_Automation_Tree_Structure"></a>
## <a name="required-ui-automation-tree-structure"></a>必須の UI オートメーション ツリー構造  
 次の表に、メニュー コントロールに関連する [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] ツリーのコントロール ビューとコンテンツ ビューを示し、それぞれのビューに含めることができる内容について説明します。 ツリーの詳細については、「 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] UI[オートメーション ツリーの概要](ui-automation-tree-overview.md)」を参照してください。  
  
|コントロール ビュー|コンテンツ ビュー|  
|------------------|------------------|  
|メニュー<br /><br /> - メニュー項目 (1 または複数)|該当なし (メニュー コントロールが、メニュー項目でないオブジェクトの親であるコンテキスト メニューに相当する場合を除く)<br /><br /> - メニュー項目 (1 または複数)|  
  
 メニュー コントロールは、コントロール ビューと [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] ツリーのコンテンツ ビューに常に表示されます。 Menu コントロール型は、その情報が参照しているコントロールの下に表示されます。 UI オートメーション クライアントは、メニュー コントロールによって伝えられる情報を常に取得できるよう、 `MenuOpenedEvent` をリッスンする必要があります。 コンテキスト メニュー コントロールは、特殊なケースです。 これらのコントロールは、デスクトップの子として表示されます。  
  
<a name="Required_UI_Automation_Properties"></a>
## <a name="required-ui-automation-properties"></a>必須の UI オートメーション プロパティ  
 次の表に、Menu コントロール型に特に関連する値または定義を持つ [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] プロパティを示します。 プロパティの[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]詳細については、「[クライアントの UI オートメーション プロパティ 」](ui-automation-properties-for-clients.md)を参照してください。  
  
|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] プロパティ|Value|Notes|  
|------------------------------------------------------------------------------------|-----------|-----------|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.NameProperty>|サポートされていません|メニュー コントロールでは、Name プロパティを設定する必要はありません。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LabeledByProperty>|`Null`|一般的なメニュー コントロールには、ラベルは不要です。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ControlTypeProperty>|メニュー|この値は、すべての UI フレームワークで同じです。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsContentElementProperty>|False|メニュー コントロールは、 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] ツリーのコンテンツ ビューに組み込まれません。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsControlElementProperty>|True|メニュー コントロールは、 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] ツリーのコントロール ビューに常に組み込まれます。|  
  
<a name="Required_UI_Automation_Control_Patterns"></a>
## <a name="required-ui-automation-control-patterns"></a>必須の UI オートメーション コントロール パターン  
 Menu コントロール型に必要なコントロール パターンはありません。  
  
<a name="Required_UI_Automation_Events"></a>
## <a name="required-ui-automation-events"></a>必須の UI オートメーション イベント  
 メニュー コントロールは、画面に表示された場合に `MenuOpenedEvent` を生成する必要があります。 `MenuOpenedEvent` にはコントロールのテキストが含まれます。 メニューが画面から非表示になった場合には、 `MenuClosedEvent` が生成されなければなりません。  
  
 次の表に、すべてのメニュー コントロールでサポートされなければならない [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] イベントを示します。 イベントの詳細については、「 [UI Automation Events Overview](ui-automation-events-overview.md)」を参照してください。  
  
|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] イベント|サポート/値|Notes|  
|---------------------------------------------------------------------------------|--------------------|-----------|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.MenuOpenedEvent>|Required|なし|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.MenuClosedEvent>|Required|なし|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty> プロパティ変更イベント。|Required|なし|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsOffscreenProperty> プロパティ変更イベント。|Required|なし|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty> プロパティ変更イベント。|Required|なし|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationFocusChangedEvent>|Required|なし|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.StructureChangedEvent>|Required|なし|  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Automation.ControlType.Menu>
- [UI Automation Control Patterns Overview](ui-automation-control-patterns-overview.md)
- [UI オートメーション コントロール型の概要](ui-automation-control-types-overview.md)
- [UI オートメーションの概要](ui-automation-overview.md)
