---
ms.openlocfilehash: cb72e1b92172b8989ce99b47181c13561a7ccd76
ms.sourcegitcommit: 79a2d6a07ba4ed08979819666a0ee6927bbf1b01
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74643893"
---
### <a name="switchsystemwindowsformsdontsupportreentrantfiltermessage-compatibility-switch-not-supported"></a>Switch.System.Windows.Forms.DontSupportReentrantFilterMessage 互換性スイッチはサポートされていません

.NET Framework 4.6.1 で導入された `Switch.System.Windows.Forms.DontSupportReentrantFilterMessage` 互換スイッチは、.NET Core 3.0 上の Windows フォームではサポートされていません。

#### <a name="change-description"></a>変更の説明

.NET Framework 4.6.1 以降、`Switch.System.Windows.Forms.DontSupportReentrantFilterMessage` 互換性スイッチでは、カスタムの <xref:System.Windows.Forms.IMessageFilter.PreFilterMessage%2A?displayProperty=nameWithType> 実装で <xref:System.IndexOutOfRangeException> メッセージが呼び出されたときに発生する可能性がある <xref:System.Windows.Forms.Application.FilterMessage%2A?displayProperty=nameWithType> 例外に対処します。 詳細については、「[軽減策:カスタムの IMessageFilter.PreFilterMessage 実装](~/docs/framework/migration-guide/mitigation-custom-imessagefilter-prefiltermessage-implementations.md)」を参照してください。

.NET Core では、`Switch.System.Windows.Forms.DontSupportReentrantFilterMessage` スイッチはサポートされていません。

#### <a name="version-introduced"></a>導入されたバージョン

3.0 Preview 9

#### <a name="recommended-action"></a>推奨される操作

スイッチを削除します。 そのスイッチはサポートされておらず、代替機能はありません。

#### <a name="category"></a>カテゴリ

Windows フォーム

#### <a name="affected-apis"></a>影響を受ける API

- <xref:System.Windows.Forms.Application.FilterMessage%2A?displayProperty=nameWithType>

<!-- 

### Affected APIs

- `M:System.Windows.Forms.Application.FilterMessage(System.Windows.Forms.Message)`

-->
