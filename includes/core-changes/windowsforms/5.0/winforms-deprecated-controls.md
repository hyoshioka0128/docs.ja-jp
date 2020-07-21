---
ms.openlocfilehash: c9720f51e40ada4cd2cf6997ba7006a232893553
ms.sourcegitcommit: 0926684d8d34f4c6b5acce58d2193db093cb9cf2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/20/2020
ms.locfileid: "83702485"
---
### <a name="removed-status-bar-controls"></a>削除されたステータス バー コントロール

.NET 5.0 Preview 1 以降では、一部の Windows フォーム コントロールが利用できなくなります。

#### <a name="change-description"></a>変更の説明

.NET 5.0 Preview 1 以降では、Windows フォームのステータス バー関連のコントロールの一部が利用できなくなります。 デザインとサポートが改善された代替コントロールは .NET Framework 2.0 で導入されました。 非推奨コントロールは前にデザイナー ツールボックスから削除されましたが、引き続き利用できました。 現在は、完全に削除されています。

次の型は現在なくなっています。

* `StatusBar`
* `StatusBarDrawItemEventArgs`
* `StatusBarDrawItemEventHandler`
* `StatusBarPanel`
* `StatusBarPanelAutoSize`
* `StatusBarPanelBorderStyle`
* `StatusBarPanelClickEventArgs`
* `StatusBarPanelClickEventHandler`
* `StatusBarPanelStyle`

#### <a name="version-introduced"></a>導入されたバージョン

5.0 Preview 1

#### <a name="recommended-action"></a>推奨アクション

これらのコントロールに対する代わりの API とそのシナリオに移行します。

| 古いコントロール (API) | 推奨される代替機能                          |
|-------------------|--------------------------------------------------|
| StatusBar         | <xref:System.Windows.Forms.StatusStrip>          |
| StatusBarPanel    | <xref:System.Windows.Forms.ToolStripStatusLabel> |

#### <a name="category"></a>カテゴリ

Windows フォーム

#### <a name="affected-apis"></a>影響を受ける API

- <xref:System.Windows.Forms.StatusBar?displayProperty=fullName>
- <xref:System.Windows.Forms.StatusBarDrawItemEventArgs?displayProperty=fullName>
- <xref:System.Windows.Forms.StatusBarDrawItemEventHandler?displayProperty=fullName>
- <xref:System.Windows.Forms.StatusBarPanel?displayProperty=fullName>
- <xref:System.Windows.Forms.StatusBarPanelAutoSize?displayProperty=fullName>
- <xref:System.Windows.Forms.StatusBarPanelBorderStyle?displayProperty=fullName>
- <xref:System.Windows.Forms.StatusBarPanelClickEventArgs?displayProperty=fullName>
- <xref:System.Windows.Forms.StatusBarPanelClickEventHandler?displayProperty=fullName>
- <xref:System.Windows.Forms.StatusBarPanelStyle?displayProperty=fullName>

<!-- 

#### Affected APIs

- `T:System.Windows.Forms.StatusBar`
- `T:System.Windows.Forms.StatusBarDrawItemEventArgs`
- `T:System.Windows.Forms.StatusBarDrawItemEventHandler`
- `T:System.Windows.Forms.StatusBarPanel`
- `T:System.Windows.Forms.StatusBarPanelAutoSize`
- `T:System.Windows.Forms.StatusBarPanelBorderStyle`
- `T:System.Windows.Forms.StatusBarPanelClickEventArgs`
- `T:System.Windows.Forms.StatusBarPanelClickEventHandler`
- `T:System.Windows.Forms.StatusBarPanelStyle` 

-->
