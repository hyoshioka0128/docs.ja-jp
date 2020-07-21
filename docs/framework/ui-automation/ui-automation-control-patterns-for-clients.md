---
title: クライアントの UI オートメーション コントロール パターン
ms.date: 03/30/2017
helpviewer_keywords:
- UI Automation, control patterns for clients
- control patterns, UI Automation clients
ms.assetid: 571561d8-5f49-43a9-a054-87735194e013
ms.openlocfilehash: 1ee0df5b133f08ec3cf6ba617c80c480e207ddf6
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79179959"
---
# <a name="ui-automation-control-patterns-for-clients"></a>クライアントの UI オートメーション コントロール パターン
> [!NOTE]
> このドキュメントは、[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 名前空間で定義されているマネージド <xref:System.Windows.Automation> クラスを使用する .NET Framework 開発者を対象としています。 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]の最新情報については、「 [Windows Automation API: UI オートメーション](/windows/win32/winauto/entry-uiauto-win32)」をご覧ください。  
  
 この概要では、UI オートメーション クライアントのコントロール パターンについて説明します。 また、UI オートメーション クライアントがコントロール パターンを使用して、 [!INCLUDE[TLA#tla_ui](../../../includes/tlasharptla-ui-md.md)]の情報にアクセスするしくみについても説明します。  
  
 コントロール パターンは、コントロール型や外観に関係なく、コントロールの機能を分類したり公開したりするための手段です。 UI オートメーション クライアントは、 <xref:System.Windows.Automation.AutomationElement> を調べてどのコントロール パターンがサポートされているかを特定し、そのコントロールの動作を確実に実行することができます。  
  
 コントロール パターンの完全なリストについては、「 [UI Automation Control Patterns Overview](ui-automation-control-patterns-overview.md)」をご覧ください。  
  
<a name="uiautomation_getting_control_patterns"></a>
## <a name="getting-control-patterns"></a>コントロール パターンの取得  
 クライアントは、 <xref:System.Windows.Automation.AutomationElement> または <xref:System.Windows.Automation.AutomationElement.GetCachedPattern%2A?displayProperty=nameWithType> を呼び出して、 <xref:System.Windows.Automation.AutomationElement.GetCurrentPattern%2A?displayProperty=nameWithType>からコントロール パターンを取得します。  
  
 クライアントは、 <xref:System.Windows.Automation.AutomationElement.GetSupportedPatterns%2A> メソッドまたは個別の `IsPatternAvailable` プロパティ ( <xref:System.Windows.Automation.AutomationElement.IsTextPatternAvailableProperty>など) を使用して、パターンまたはパターンのグループが <xref:System.Windows.Automation.AutomationElement>でサポートされているかどうかを特定できます。 ただし、サポートされているプロパティを確認してコントロール パターンを取得するよりも、コントロール パターンを取得して `null` 参照に対するテストを試行する方が、プロセス間呼び出しが少なくなるため効率的です。  
  
 <xref:System.Windows.Automation.TextPattern> から <xref:System.Windows.Automation.AutomationElement>コントロール パターンを取得する方法を次の例に示します。  
  
 [!code-csharp[UIATextPattern_snip#1037](../../../samples/snippets/csharp/VS_Snippets_Wpf/UIATextPattern_snip/CSharp/SearchWindow.cs#1037)]  
  
<a name="uiautomation_properties_on_control_patterns"></a>
## <a name="retrieving-properties-on-control-patterns"></a>コントロール パターンのプロパティの取得  
 クライアントは、 <xref:System.Windows.Automation.AutomationElement.GetCachedPropertyValue%2A?displayProperty=nameWithType> または <xref:System.Windows.Automation.AutomationElement.GetCurrentPropertyValue%2A?displayProperty=nameWithType> を呼び出し、返されたオブジェクトを適切な型にキャストすることで、コントロール パターンのプロパティ値を取得できます。 プロパティの[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]詳細については、「[クライアントの UI オートメーション プロパティ 」](ui-automation-properties-for-clients.md)を参照してください。  
  
 `GetPropertyValue`メソッドに加えて、プロパティ値は、共通言語ランタイム (CLR) アクセサーを使用して取得して、パターン[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]のプロパティにアクセスできます。  
  
<a name="uiautomation_with_variable_patterns"></a>
## <a name="controls-with-variable-patterns"></a>変数パターンを持つコントロール  
 一部のコントロール型は、状態やコントロールの使用方法に応じた複数のパターンをサポートしています。 可変パターンを持つことができるコントロールの例としては、リストビュー(サムネイル、タイル、アイコン、リスト、詳細)、Excelグラフ(円、折れ線、横棒、数式付きセル値)、Word の文書領域(標準、Web レイアウト、アウトライン、印刷レイアウト、印刷)などがあります。プレビュー)、およびマイクロソフトのメディア プレーヤーのスキン。  
  
 カスタム コントロール型を実装するコントロールは、機能を表すために必要なコントロール パターンの任意のセットを持つことができます。  
  
## <a name="see-also"></a>関連項目

- [UI オートメーション コントロール パターン](ui-automation-control-patterns.md)
- [UI オートメーション テキスト パターン](ui-automation-text-pattern.md)
- [UI オートメーションを使用したコントロールの呼び出し](invoke-a-control-using-ui-automation.md)
- [UI オートメーションを使用した、チェック ボックスのトグル状態の取得](get-the-toggle-state-of-a-check-box-using-ui-automation.md)
- [UI オートメーション クライアントのコントロール パターン マッピング](control-pattern-mapping-for-ui-automation-clients.md)
- [テキストパターン挿入テキストのサンプル](https://github.com/Microsoft/WPF-Samples/tree/master/Accessibility/InsertText)
- [テキストパターンの検索と選択のサンプル](https://github.com/Microsoft/WPF-Samples/tree/master/Accessibility/FindText)
- [呼び出しパターン、展開折りたたみパターン、およびトグルパターンのサンプル](https://github.com/Microsoft/WPF-Samples/tree/master/Accessibility/InvokePattern)
