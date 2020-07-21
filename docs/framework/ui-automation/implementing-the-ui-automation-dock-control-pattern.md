---
title: UI オートメーション Dock コントロール パターンの実装
ms.date: 03/30/2017
helpviewer_keywords:
- control patterns, dock
- dock control pattern
- UI Automation, dock control pattern
ms.assetid: ea3d2212-7c8e-4dd7-bf08-73141ca2d4fb
ms.openlocfilehash: b1213791609245209fa37e3cdcb0876c963bfeb0
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79180203"
---
# <a name="implementing-the-ui-automation-dock-control-pattern"></a>UI オートメーション Dock コントロール パターンの実装
> [!NOTE]
> このドキュメントは、[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 名前空間で定義されているマネージド <xref:System.Windows.Automation> クラスを使用する .NET Framework 開発者を対象としています。 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]の最新情報については、「 [Windows Automation API: UI オートメーション](/windows/win32/winauto/entry-uiauto-win32)」をご覧ください。  
  
 ここでは、プロパティに関する情報など、 <xref:System.Windows.Automation.Provider.IDockProvider>を実装するガイドラインと規則について説明します。 その他のリファレンスへのリンクは、トピックの最後に記載します。  
  
 <xref:System.Windows.Automation.DockPattern> コントロール パターンは、ドッキング コンテナー内のコントロールのドッキング プロパティを公開するために使用します。 ドッキング コンテナーは、子要素を互いに水平方向または垂直方向に整列できるコントロールです。 このコントロール パターンを実装するコントロールの例については、「 [Control Pattern Mapping for UI Automation Clients](control-pattern-mapping-for-ui-automation-clients.md)」をご覧ください。  
  
 ![ドッキングされた 2 つの子を持つドッキング コンテナー。](./media/uia-dockpattern-dockingexample.PNG "UIA_DockPattern_DockingExample")  
"Class View" ウィンドウが DockPosition.Right に "Error List" ウィンドウが DockPosition.Bottom にそれぞれ配置された Visual Studio のドッキングの例  
  
<a name="Implementation_Guidelines_and_Conventions"></a>
## <a name="implementation-guidelines-and-conventions"></a>実装のガイドラインと規則  
 Dock コントロール パターンを実装する場合は、次のガイドラインと規則に注意してください。  
  
- <xref:System.Windows.Automation.Provider.IDockProvider> は、ドッキング コンテナーのプロパティや、ドッキング コンテナー内の現在のコントロールに隣接してドッキングされるコントロールのプロパティは公開しません。  
  
- コントロールは、現在の重ね順に基づき、互いを基準としてドッキングされます。重ね順が上位であるほど、指定されたドッキング コンテナーの端から離れた位置に配置されます。  
  
- ドッキング コンテナーのサイズを変更すると、コンテナー内にドッキングされているコントロールは、もともとドッキングされていたのと同じ端に合わせて再配置されます。 また、ドッキングされているコントロールは、 <xref:System.Windows.Automation.DockPosition>のドッキング動作に従って、コンテナー内のスペースを埋めるようにサイズ変更されます。 たとえば、 <xref:System.Windows.Automation.DockPosition.Top> が指定されている場合は、コントロールの左側と右側が広がって、使用できるスペースを埋めます。 <xref:System.Windows.Automation.DockPosition.Fill> が指定されている場合は、コントロールの 4 つの側面すべてが広がって、使用できるスペースを埋めます。  
  
- マルチモニター システムでは、コントロールは現在のモニターの左側または右側にドッキングする必要があります。 それが不可能な場合は、左端のモニターの左側、または右端のモニターの右側にドッキングする必要があります。  
  
<a name="Required_Members_for_IDockProvider"></a>
## <a name="required-members-for-idockprovider"></a>IDockProvider の必須メンバー  
 次のプロパティとメソッドは、IDockProvider インターフェイスの実装時に必要です。  
  
|必須メンバー|メンバーの型|Notes|  
|----------------------|-----------------|-----------|  
|<xref:System.Windows.Automation.Provider.IDockProvider.DockPosition%2A>|プロパティ|なし|  
|<xref:System.Windows.Automation.Provider.IDockProvider.SetDockPosition%2A>|Method|なし|  
  
 このコントロール パターンには、関連するイベントがありません。  
  
<a name="Exceptions"></a>
## <a name="exceptions"></a>例外  
 プロバイダーは、次の例外をスローする必要があります。  
  
|例外の種類|条件|  
|--------------------|---------------|  
|<xref:System.InvalidOperationException>|<xref:System.Windows.Automation.Provider.IDockProvider.SetDockPosition%2A><br /><br /> - コントロールが要求されたドック スタイルを実行できない場合。|  
  
## <a name="see-also"></a>関連項目

- [UI Automation Control Patterns Overview](ui-automation-control-patterns-overview.md)
- [UI オートメーション プロバイダーでのコントロール パターンのサポート](support-control-patterns-in-a-ui-automation-provider.md)
- [クライアントの UI オートメーション コントロール パターン](ui-automation-control-patterns-for-clients.md)
- [UI Automation Tree Overview](ui-automation-tree-overview.md)
- [UI オートメーションにおけるキャッシュの使用](use-caching-in-ui-automation.md)
