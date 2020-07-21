---
ms.openlocfilehash: cb8c0532bb2bcfbcd619cd382f3d236b431c3480
ms.sourcegitcommit: 0926684d8d34f4c6b5acce58d2193db093cb9cf2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/20/2020
ms.locfileid: "83721228"
---
### <a name="donotloadlatestricheditcontrol-compatibility-switch-not-supported"></a>DoNotLoadLatestRichEditControl 互換性スイッチはサポートされていません

.NET Framework 4.7.1 で導入された `Switch.System.Windows.Forms.UseLegacyImages` 互換スイッチは、.NET Core 3.0 上の Windows フォームではサポートされていません。

#### <a name="change-description"></a>変更の説明

.NET Framework 4.6.2 とそれ以前のバージョンでは、<xref:System.Windows.Forms.RichTextBox> コントロールによって Win32 RichEdit コントロール v3.0 がインスタンス化され、.NET Framework 4.7.1 をターゲットとするアプリケーションの場合、<xref:System.Windows.Forms.RichTextBox> コントロールによって RichEdit v4.1 (*msftedit.dll*) がインスタンス化されます。 `Switch.System.Windows.Forms.DoNotLoadLatestRichEditControl` 互換性スイッチは、.NET Framework 4.7.1 以降のバージョンをターゲットとするアプリケーションが新しい RichEdit v4.1 コントロールをオプトアウトし、代わりに古い RichEdit v3 コントロールを使用できるようにするために導入されました。

.NET Core では、`Switch.System.Windows.Forms.DoNotLoadLatestRichEditControl` スイッチはサポートされていません。 <xref:System.Windows.Forms.RichTextBox> コントロールの新しいバージョンのみがサポートされています。

#### <a name="version-introduced"></a>導入されたバージョン

3.0 Preview 9

#### <a name="recommended-action"></a>推奨アクション

スイッチを削除します。 そのスイッチはサポートされておらず、代替機能はありません。

#### <a name="category"></a>カテゴリ

Windows フォーム

#### <a name="affected-apis"></a>影響を受ける API

- <xref:System.Windows.Forms.RichTextBox?displayProperty=nameWithType>

<!-- 

#### Affected APIs

-  `T:System.Windows.Forms.RichTextBox` 

-->
