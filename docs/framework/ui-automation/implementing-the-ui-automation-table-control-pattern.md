---
title: UI オートメーション Table コントロール パターンの実装
ms.date: 03/30/2017
helpviewer_keywords:
- UI Automation, Table control pattern
- control patterns, Table
- TableControl pattern
ms.assetid: 880cd85c-aa8c-4fb5-9369-45491d34bb78
ms.openlocfilehash: 0b3d000112060550734890ad3c4063a26c320b04
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79180114"
---
# <a name="implementing-the-ui-automation-table-control-pattern"></a>UI オートメーション Table コントロール パターンの実装
> [!NOTE]
> このドキュメントは、[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 名前空間で定義されているマネージド <xref:System.Windows.Automation> クラスを使用する .NET Framework 開発者を対象としています。 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]の最新情報については、「 [Windows Automation API: UI オートメーション](/windows/win32/winauto/entry-uiauto-win32)」をご覧ください。  
  
 このトピックでは、プロパティ、メソッド、イベントに関する情報など、 <xref:System.Windows.Automation.Provider.ITableProvider>の実装のためのガイドラインと規則について説明します。 その他のリファレンスへのリンクは、概要の最後に記載します。  
  
 <xref:System.Windows.Automation.TablePattern> コントロール パターンは、子要素のコレクションのコンテナーとして機能するコントロールをサポートするために使用します。 この要素の子には <xref:System.Windows.Automation.Provider.ITableItemProvider> を実装する必要があります。また、この要素の子は、行と列で表現できる 2 次元の論理座標システムで編成しなければなりません。 このコントロール パターンは、<xref:System.Windows.Automation.Provider.ITableProvider> を実装するコントロールが各子要素の列ヘッダーまたは行ヘッダーの関係を公開する必要もあることを除いて、<xref:System.Windows.Automation.Provider.IGridProvider> に似ています。 このコントロール パターンを実装するコントロールの例については、「 [Control Pattern Mapping for UI Automation Clients](control-pattern-mapping-for-ui-automation-clients.md)」をご覧ください。  
  
<a name="Implementation_Guidelines_and_Conventions"></a>
## <a name="implementation-guidelines-and-conventions"></a>実装のガイドラインと規則  
 Table コントロール パターンを実装する場合は、次のガイドラインと規則に留意してください。  
  
- 個々のセルのコンテンツへのアクセスは、2 次元論理座標系または <xref:System.Windows.Automation.Provider.IGridProvider> の必要な同時実装によって提供される配列を経由します。  
  
- 列ヘッダーまたは行ヘッダーは、テーブル オブジェクト内に含めることも、テーブル オブジェクトに関連付けられた別のヘッダー オブジェクトにすることもできます。  
  
- 列ヘッダーと行ヘッダーには、プライマリ ヘッダーだけでなく、任意の補助ヘッダーも含めることができます。  
  
> [!NOTE]
> この概念は、ユーザーが "名" 列を定義した Microsoft Excel スプレッドシートで明らかになります。 これで、この列のヘッダーは、ユーザーが定義した [ファースト ネーム] ヘッダーとアプリケーションによって割り当てられたその列の英数字指定の 2 つになります。  
  
- 関連する[グリッド機能については、「UI オートメーション グリッド コントロール パターンの実装](implementing-the-ui-automation-grid-control-pattern.md)」を参照してください。  
  
 ![複雑なヘッダー項目を含むテーブル。](./media/uia-tablepattern-complex-column-headers.PNG "UIA_TablePattern_Complex_Column_Headers")  
列ヘッダーが複雑なテーブルの例  
  
 ![あいまいな RowOrColumnMajor プロパティを含むテーブル。](./media/uia-tablepattern-roworcolumnmajorproperty.PNG "UIA_TablePattern_RowOrColumnMajorProperty")  
RowOrColumnMajor プロパティがあいまいなテーブルの例  
  
<a name="Required_Members_for_ITableProvider"></a>
## <a name="required-members-for-itableprovider"></a>ITableProvider の必須メンバー  
 ITableProvider インターフェイスには、次のプロパティとメソッドが必要です。  
  
|必須メンバー|メンバーの型|Notes|  
|----------------------|-----------------|-----------|  
|<xref:System.Windows.Automation.Provider.ITableProvider.RowOrColumnMajor%2A>|プロパティ|なし|  
|<xref:System.Windows.Automation.Provider.ITableProvider.GetColumnHeaders%2A>|Method|なし|  
|<xref:System.Windows.Automation.Provider.ITableProvider.GetRowHeaders%2A>|Method|なし|  
  
 このコントロール パターンには、関連するイベントがありません。  
  
<a name="Exceptions"></a>
## <a name="exceptions"></a>例外  
 このコントロール パターンに関連付けられた例外はありません。  
  
## <a name="see-also"></a>関連項目

- [UI Automation Control Patterns Overview](ui-automation-control-patterns-overview.md)
- [UI オートメーション プロバイダーでのコントロール パターンのサポート](support-control-patterns-in-a-ui-automation-provider.md)
- [クライアントの UI オートメーション コントロール パターン](ui-automation-control-patterns-for-clients.md)
- [UI オートメーション TableItem コントロール パターンの実装](implementing-the-ui-automation-tableitem-control-pattern.md)
- [UI オートメーション Grid コントロール パターンの実装](implementing-the-ui-automation-grid-control-pattern.md)
- [UI Automation Tree Overview](ui-automation-tree-overview.md)
- [UI オートメーションにおけるキャッシュの使用](use-caching-in-ui-automation.md)
