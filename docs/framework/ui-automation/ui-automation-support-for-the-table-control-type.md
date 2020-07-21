---
title: UI オートメーションによる Table コントロール型のサポート
ms.date: 03/30/2017
helpviewer_keywords:
- TableControl type
- control types, Table
- UI Automation, Table control type
ms.assetid: 9050dde5-6469-4c83-abb7-f861c24ff985
ms.openlocfilehash: 8a6d78ce159727ddeff72ec5729c1cc645648b61
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79179531"
---
# <a name="ui-automation-support-for-the-table-control-type"></a>UI オートメーションによる Table コントロール型のサポート
> [!NOTE]
> このドキュメントは、[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 名前空間で定義されているマネージド <xref:System.Windows.Automation> クラスを使用する .NET Framework 開発者を対象としています。 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]の最新情報については、「 [Windows Automation API: UI オートメーション](/windows/win32/winauto/entry-uiauto-win32)」をご覧ください。  
  
 このトピックでは、Table コントロール型の [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] サポートに関する情報を提供します。 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]でのコントロール型とは、コントロールが <xref:System.Windows.Automation.AutomationElement.ControlTypeProperty> プロパティを使用するために満たす必要がある一連の条件のことです。 これらの条件には、 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] ツリー構造、 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] のプロパティ値、およびコントロール パターンに関する特定のガイドラインが含まれます。  
  
 テーブル コントロールは、テキストの行と列、およびオプションで行ヘッダーと列ヘッダーを格納します。  
  
 以降のセクションでは、Table コントロール型に必要な [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] ツリー構造、プロパティ、コントロール パターン、イベントを定義します。 要件[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]は、Win32 または[!INCLUDE[TLA#tla_winclient](../../../includes/tlasharptla-winclient-md.md)]Windows フォームのテーブル コントロールすべてに適用されます。  
  
<a name="Required_UI_Automation_Tree_Structure"></a>
## <a name="required-ui-automation-tree-structure"></a>必須の UI オートメーション ツリー構造  
 次の表に、テーブル コントロールに関連する [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] ツリーのコントロール ビューとコンテンツ ビューを示し、それぞれのビューに含めることができる内容について説明します。 ツリーの詳細については、「 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] UI[オートメーション ツリーの概要](ui-automation-tree-overview.md)」を参照してください。  
  
|コントロール ビュー|コンテンツ ビュー|  
|------------------|------------------|  
|テーブル<br /><br /> - ヘッダー (0 または 1)<br />- テキスト (0 または 1)<br />- 各種コントロール (0 以上)|テーブル<br /><br /> - テキスト (0 以上)<br />- 各種コントロール (0 以上)|  
  
 テーブル コントロールに行ヘッダーまたは列ヘッダーが含まれている場合は、それらを UI オートメーション ツリーのコントロール ビューで公開する必要があります。 コンテンツ ビューは、TablePattern を使用してアクセスできるため、この情報を公開する必要がありません。  
  
<a name="Required_UI_Automation_Properties"></a>
## <a name="required-ui-automation-properties"></a>必須の UI オートメーション プロパティ  
 次の表に、テーブル コントロールに特に関連する値または定義を持つ [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] プロパティを示します。 プロパティの詳細[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]については、「[クライアントの UI オートメーション プロパティ 」](ui-automation-properties-for-clients.md)を参照してください。  
  
|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] プロパティ|Value|Notes|  
|------------------------------------------------------------------------------------|-----------|-----------|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationIdProperty>|「ノート」を参照してください。|このプロパティの値は、アプリケーション内のすべてのコントロールで一意である必要があります。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty>|「ノート」を参照してください。|コントロール全体を格納する最も外側の四角形。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ClickablePointProperty>|「ノート」を参照してください。|四角形領域が存在する場合にサポートされます。 四角形領域内にクリック不可能な点が存在し、特別なヒット テストを実行する場合は、オーバーライドしてクリック可能な点を提供します。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsKeyboardFocusableProperty>|「ノート」を参照してください。|コントロールがキーボード フォーカスを受け取ることができる場合は、このプロパティをサポートする必要があります。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.NameProperty>|「ノート」を参照してください。|通常、テーブル コントロールは、静的テキスト ラベルからその名前を取得します。 静的テキスト ラベルが存在しない場合は、Name プロパティを割り当てる必要があります。このプロパティは、テーブルの目的を説明するために常に利用できる必要があります。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LabeledByProperty>|「ノート」を参照してください。|静的テキスト ラベルが存在する場合、このプロパティは、そのコントロールのオートメーション要素への参照を公開する必要があります。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ControlTypeProperty>|テーブル|この値は、すべての UI フレームワークで同じです。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LocalizedControlTypeProperty>|"table"|Table コントロール型に対応する、ローカライズされた文字列。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.HelpTextProperty>|「ノート」を参照してください。|NameProperty にアクセスするだけではテーブルの目的が十分伝わらない場合は、このプロパティを介してさらに詳しく説明する必要があります。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsContentElementProperty>|True|テーブル コントロールは、常にコンテンツである必要があります。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsControlElementProperty>|True|テーブル コントロールは、常にコントロールである必要があります。|  
  
<a name="Required_UI_Automation_Control_Patterns"></a>
## <a name="required-ui-automation-control-patterns"></a>必須の UI オートメーション コントロール パターン  
 次の表に、テーブル コントロールでサポートする必要がある [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] コントロール パターンを示します。 コントロール パターンの詳細については、「 [UI Automation Control Patterns Overview](ui-automation-control-patterns-overview.md)」を参照してください。  
  
|コントロール パターン|サポート|Notes|  
|---------------------|-------------|-----------|  
|<xref:System.Windows.Automation.Provider.IGridProvider>|はい|テーブルに格納される項目にはグリッドに表示されるデータが含まれるため、テーブル コントロールはこのコントロール パターンを常にサポートします。|  
|<xref:System.Windows.Automation.Provider.IGridItemProvider>|はい (子オブジェクトでは必須)|テーブルの内部オブジェクトは、GridItem と TableItem の両方のコントロール パターンをサポートする必要があります。 テーブル自体では、それが別のテーブルの一部である場合を除いて、GridItem コントロール パターンも TableItem コントロール パターンもサポートする必要がありません。|  
|<xref:System.Windows.Automation.Provider.ITableProvider>|はい|テーブル コントロールは、常に、ヘッダーとコンテンツを関連付けることができます。|  
|<xref:System.Windows.Automation.Provider.ITableItemProvider>|はい (子オブジェクトでは必須)|テーブルの内部オブジェクトは、GridItem と TableItem の両方のコントロール パターンをサポートする必要があります。 テーブル自体では、それが別のテーブルの一部である場合を除いて、GridItem コントロール パターンも TableItem コントロール パターンもサポートする必要がありません。|  
  
<a name="Required_UI_Automation_Events"></a>
## <a name="required-ui-automation-events"></a>必須の UI オートメーション イベント  
 次の表に、すべてのテーブル コントロールでサポートされなければならない [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] イベントを示します。 イベントの詳細については、「 [UI Automation Events Overview](ui-automation-events-overview.md)」を参照してください。  
  
|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] イベント|サポート|Notes|  
|---------------------------------------------------------------------------------|-------------|-----------|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty> プロパティ変更イベント。|Required|なし|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsOffscreenProperty> プロパティ変更イベント。|Required|なし|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty> プロパティ変更イベント。|Required|なし|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationFocusChangedEvent>|Required|なし|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.StructureChangedEvent>|Required|なし|  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Automation.ControlType.Table>
- [UI オートメーション コントロール型の概要](ui-automation-control-types-overview.md)
- [UI オートメーションの概要](ui-automation-overview.md)
