---
ms.openlocfilehash: 39d609c955596354d1af28b4ed19d367dab0462b
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85620156"
---
### <a name="pageloadcomplete-event-no-longer-causes-systemwebuiwebcontrolsentitydatasource-control-to-invoke-data-binding"></a>Page.LoadComplete イベントによって、System.Web.UI.WebControls.EntityDataSource コントロールがデータ バインディングを呼び出さなくなりました

#### <a name="details"></a>説明

<xref:System.Web.UI.Page.LoadComplete> イベントが原因で、<xref:System.Web.UI.WebControls.EntityDataSource?displayProperty=fullName> のコントロールがパラメーターの作成/更新/削除に変更を加えるためにデータ バインディングを呼び出すことがなくなりました。 この変更により、データベースへの不要なアクセスが排除され、コントロールの値がリセットされるのを防ぐことができるほか、<xref:System.Web.UI.WebControls.SqlDataSource?displayProperty=fullName> や <xref:System.Web.UI.WebControls.ObjectDataSource?displayProperty=fullName>などのように他のデータ コントロールと一貫性の取れた動作が生成されます。 この変更により、アプリケーションが <xref:System.Web.UI.Page.LoadComplete> イベントのデータ バインディングの呼び出しに依存するような珍しい状況において、異なる動作が生成されるようになりました。

#### <a name="suggestion"></a>提案される解決策

データバインドの必要がある場合は、ポストバックの前半であるイベントでデータバインドを手動で呼び出します。

| 名前    | [値]       |
|:--------|:------------|
| スコープ   |エッジ|
|バージョン|4.5|
|種類|ランタイム|
