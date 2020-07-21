---
title: UI オートメーション SelectionItem コントロール パターンの実装
ms.date: 03/30/2017
helpviewer_keywords:
- Selection Item control pattern
- UI Automation, Selection Item control pattern
- control patterns, Selection Item
ms.assetid: 76b0949a-5b23-4cfc-84cc-154f713e2e12
ms.openlocfilehash: 02505224e4673592f1e169c40af1cfb098e5d9bb
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79180103"
---
# <a name="implementing-the-ui-automation-selectionitem-control-pattern"></a>UI オートメーション SelectionItem コントロール パターンの実装
> [!NOTE]
> このドキュメントは、[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 名前空間で定義されているマネージド <xref:System.Windows.Automation> クラスを使用する .NET Framework 開発者を対象としています。 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]の最新情報については、「 [Windows Automation API: UI オートメーション](/windows/win32/winauto/entry-uiauto-win32)」をご覧ください。  
  
 このトピックでは、プロパティ、メソッド、イベントに関する情報など、 <xref:System.Windows.Automation.Provider.ISelectionItemProvider>の実装のためのガイドラインと規則について説明します。 その他のリファレンスへのリンクは、概要の最後に記載します。  
  
 <xref:System.Windows.Automation.SelectionItemPattern> コントロール パターンは、 <xref:System.Windows.Automation.Provider.ISelectionProvider>を実装するコンテナー コントロールの個別の選択可能な子項目として機能するコントロールをサポートするために使用します。 SelectionItem コントロール パターンを実装するコントロールの例については[、「UI オートメーション クライアントのコントロール パターン マッピング」を](control-pattern-mapping-for-ui-automation-clients.md)参照してください。  
  
<a name="Implementation_Guidelines_and_Conventions"></a>
## <a name="implementation-guidelines-and-conventions"></a>実装のガイドラインと規則  
 Selection Item コントロール パターンを実装する場合は、次のガイドラインと規則に留意してください。  
  
- <xref:System.Windows.Automation.Provider.IRawElementProviderFragmentRoot>[画面のプロパティ] **ダイアログ ボックスの** [画面解像度] **スライダーなどの** を実装する子コントロールを管理する単一選択コントロールは <xref:System.Windows.Automation.Provider.ISelectionProvider> を実装する必要があり、その子は <xref:System.Windows.Automation.Provider.IRawElementProviderFragment> と <xref:System.Windows.Automation.Provider.ISelectionItemProvider>の両方を実装する必要があります。  
  
<a name="Required_Members_for_the_IValueProvider_Interface"></a>
## <a name="required-members-for-iselectionitemprovider"></a>ISelectionItemProvider の必須メンバー  
 <xref:System.Windows.Automation.Provider.ISelectionItemProvider>の実装には、次のプロパティ、メソッド、およびイベントが必要です。  
  
|必須メンバー|メンバーの型|Notes|  
|----------------------|-----------------|-----------|  
|<xref:System.Windows.Automation.Provider.ISelectionProvider.CanSelectMultiple%2A>|プロパティ|なし|  
|<xref:System.Windows.Automation.Provider.ISelectionProvider.IsSelectionRequired%2A>|プロパティ|なし|  
|<xref:System.Windows.Automation.Provider.ISelectionProvider.GetSelection%2A>|Method|なし|  
|<xref:System.Windows.Automation.SelectionPatternIdentifiers.InvalidatedEvent>|Event|コンテナー内の選択が大幅に変更され、 <xref:System.Windows.Automation.SelectionItemPatternIdentifiers.ElementSelectedEvent> 定数で許可されたよりも多くの <xref:System.Windows.Automation.SelectionItemPatternIdentifiers.ElementRemovedFromSelectionEvent> イベントと <xref:System.Windows.Automation.Provider.AutomationInteropProvider.InvalidateLimit> イベントを送信する必要がある場合に発生します。|  
  
- <xref:System.Windows.Automation.SelectionItemPattern.Select%2A>の結果<xref:System.Windows.Automation.SelectionItemPattern.AddToSelection%2A>が 1 つの選択項目<xref:System.Windows.Automation.SelectionItemPattern.RemoveFromSelection%2A>である場合は、 が発生します<xref:System.Windows.Automation.SelectionItemPatternIdentifiers.ElementSelectedEvent>。それ以外<xref:System.Windows.Automation.SelectionItemPatternIdentifiers.ElementAddedToSelectionEvent>/ <xref:System.Windows.Automation.SelectionItemPatternIdentifiers.ElementRemovedFromSelectionEvent>の場合は、必要に応じて送信します。  
  
<a name="Exceptions"></a>
## <a name="exceptions"></a>例外  
 プロバイダーは、次の例外をスローする必要があります。  
  
|例外の種類|条件|  
|--------------------|---------------|  
|<xref:System.InvalidOperationException>|次のいずれが試行された場合:<br /><br /> -   <xref:System.Windows.Automation.Provider.ISelectionItemProvider.RemoveFromSelection%2A> = <xref:System.Windows.Automation.SelectionPattern.IsSelectionRequiredProperty> = `true` が呼び出された場合。<br />-   <xref:System.Windows.Automation.Provider.ISelectionItemProvider.RemoveFromSelection%2A> = <xref:System.Windows.Automation.SelectionPattern.IsSelectionRequiredProperty> = `true` が呼び出された場合。<br />-   <xref:System.Windows.Automation.Provider.ISelectionItemProvider.AddToSelection%2A> = <xref:System.Windows.Automation.SelectionPattern.CanSelectMultipleProperty> = `false` が呼び出された場合。|  
  
## <a name="see-also"></a>関連項目

- [UI Automation Control Patterns Overview](ui-automation-control-patterns-overview.md)
- [UI オートメーション プロバイダーでのコントロール パターンのサポート](support-control-patterns-in-a-ui-automation-provider.md)
- [クライアントの UI オートメーション コントロール パターン](ui-automation-control-patterns-for-clients.md)
- [UI オートメーション Selection コントロール パターンの実装](implementing-the-ui-automation-selection-control-pattern.md)
- [UI Automation Tree Overview](ui-automation-tree-overview.md)
- [UI オートメーションにおけるキャッシュの使用](use-caching-in-ui-automation.md)
- [フラグメント プロバイダーのサンプル](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms771502(v=vs.90))
