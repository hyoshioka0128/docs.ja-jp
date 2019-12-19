---
ms.openlocfilehash: 84b6bfc32f5a73597b227098e5aee1e3450cf85b
ms.sourcegitcommit: 79a2d6a07ba4ed08979819666a0ee6927bbf1b01
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74643899"
---
### <a name="switchsystemwindowsformsenablevisualstylevalidation-compatibility-switch-not-supported"></a>Switch.System.Windows.Forms.EnableVisualStyleValidation 互換性スイッチはサポートされていません

`Switch.System.Windows.Forms.EnableVisualStyleValidation` 互換性スイッチは、.NET Core 3.0 上の Windows フォームではサポートされていません。

#### <a name="change-description"></a>変更の説明

.NET Framework では、`Switch.System.Windows.Forms.EnableVisualStyleValidation` 互換スイッチによって、アプリケーションで、数値形式で指定された視覚スタイルの検証を無効にすることが許可されていました。

.NET Core では、`Switch.System.Windows.Forms.EnableVisualStyleValidation` スイッチはサポートされていません。

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
