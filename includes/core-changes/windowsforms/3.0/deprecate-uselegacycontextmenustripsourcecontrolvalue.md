---
ms.openlocfilehash: 3ada05a13ec7acde1d8374ed733d0d51cdfb408c
ms.sourcegitcommit: 0926684d8d34f4c6b5acce58d2193db093cb9cf2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/20/2020
ms.locfileid: "83721545"
---
### <a name="uselegacycontextmenustripsourcecontrolvalue-compatibility-switch-not-supported"></a>UseLegacyContextMenuStripSourceControlValue 互換性スイッチはサポートされていません

.NET Framework 4.7.2 で導入された `Switch.System.Windows.Forms.UseLegacyContextMenuStripSourceControlValue` 互換スイッチは、.NET Core 3.0 上の Windows フォームではサポートされていません。

#### <a name="change-description"></a>変更の説明

.NET Framework 4.7.2 以降、`Switch.System.Windows.Forms.UseLegacyContextMenuStripSourceControlValue` 互換性スイッチを使用すると、開発者は <xref:System.Windows.Forms.ContextMenuStrip.SourceControl?displayProperty=nameWithType> プロパティの新しい動作を無効にできます。これにより、ソース管理への参照が返されるようになりました。 プロパティの以前の動作では、`null` が返されました。 詳細については、「[\<AppContextSwitchOverrides> 要素](~/docs/framework/configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md)」を参照してください。

.NET Core では、`Switch.System.Windows.Forms.UseLegacyContextMenuStripSourceControlValue` スイッチはサポートされていません。

#### <a name="version-introduced"></a>導入されたバージョン

3.0 Preview 9

#### <a name="recommended-action"></a>推奨アクション

スイッチを削除します。 そのスイッチはサポートされておらず、代替機能はありません。

#### <a name="category"></a>カテゴリ

Windows フォーム

#### <a name="affected-apis"></a>影響を受ける API

- <xref:System.Windows.Forms.ContextMenuStrip.SourceControl?displayProperty=nameWithType>

<!-- 

#### Affected APIs

- `P:System.Windows.Forms.ContextMenuStrip.SourceControl`

-->
