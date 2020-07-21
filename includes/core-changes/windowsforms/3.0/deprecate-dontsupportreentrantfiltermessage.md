---
ms.openlocfilehash: 55c13aa70a03bcc548ce1d096cca8f40de6cda84
ms.sourcegitcommit: 0926684d8d34f4c6b5acce58d2193db093cb9cf2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/20/2020
ms.locfileid: "83721593"
---
### <a name="dontsupportreentrantfiltermessage-compatibility-switch-not-supported"></a>DontSupportReentrantFilterMessage 互換性スイッチはサポートされていません

.NET Framework 4.6.1 で導入された `Switch.System.Windows.Forms.DontSupportReentrantFilterMessage` 互換スイッチは、.NET Core 3.0 上の Windows フォームではサポートされていません。

#### <a name="change-description"></a>変更の説明

.NET Framework 4.6.1 以降、`Switch.System.Windows.Forms.DontSupportReentrantFilterMessage` 互換性スイッチでは、カスタムの <xref:System.Windows.Forms.IMessageFilter.PreFilterMessage%2A?displayProperty=nameWithType> 実装で <xref:System.IndexOutOfRangeException> メッセージが呼び出されたときに発生する可能性がある <xref:System.Windows.Forms.Application.FilterMessage%2A?displayProperty=nameWithType> 例外に対処します。 詳細については、[「軽減策: カスタムの IMessageFilter.PreFilterMessage 実装」](~/docs/framework/migration-guide/mitigation-custom-imessagefilter-prefiltermessage-implementations.md)を参照してください。

.NET Core では、`Switch.System.Windows.Forms.DontSupportReentrantFilterMessage` スイッチはサポートされていません。

#### <a name="version-introduced"></a>導入されたバージョン

3.0 Preview 9

#### <a name="recommended-action"></a>推奨アクション

スイッチを削除します。 そのスイッチはサポートされておらず、代替機能はありません。

#### <a name="category"></a>カテゴリ

Windows フォーム

#### <a name="affected-apis"></a>影響を受ける API

- <xref:System.Windows.Forms.Application.FilterMessage%2A?displayProperty=nameWithType>

<!-- 

#### Affected APIs

- `M:System.Windows.Forms.Application.FilterMessage(System.Windows.Forms.Message)`

-->
