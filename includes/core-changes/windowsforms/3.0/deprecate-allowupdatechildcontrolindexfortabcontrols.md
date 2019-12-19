---
ms.openlocfilehash: 1d01de4b978309e05a6036953f2a6909628a2480
ms.sourcegitcommit: 79a2d6a07ba4ed08979819666a0ee6927bbf1b01
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74643887"
---
### <a name="switchsystemwindowsformsallowupdatechildcontrolindexfortabcontrols-compatibility-switch-not-supported"></a>Switch.System.Windows.Forms.AllowUpdateChildControlIndexForTabControls 互換性スイッチはサポートされていません

`Switch.System.Windows.Forms.AllowUpdateChildControlIndexForTabControls` 互換性スイッチは、.NET Framework 4.6 以降のバージョンの Windows フォームではサポートされていますが、.NET Core 3.0 以降の Windows フォームではサポートされていません。

#### <a name="change-description"></a>変更の説明

.NET Framework 4.6 以降のバージョンでは、タブを選択すると、そのコントロール コレクションが並べ替えられます。 `Switch.System.Windows.Forms.AllowUpdateChildControlIndexForTabControls` 互換性スイッチを使用すると、この動作が望ましくない場合に、アプリケーションでこの並べ替えをスキップできます。

.NET Core では、`Switch.System.Windows.Forms.AllowUpdateChildControlIndexForTabControls` スイッチはサポートされていません。

#### <a name="version-introduced"></a>導入されたバージョン

3.0 Preview 9

#### <a name="recommended-action"></a>推奨される操作

スイッチを削除します。 そのスイッチはサポートされておらず、代替機能はありません。

#### <a name="category"></a>カテゴリ

Windows フォーム

#### <a name="affected-apis"></a>影響を受ける API

- なし

<!-- 

### Affected APIs

- Not detectable via API analysis

-->
