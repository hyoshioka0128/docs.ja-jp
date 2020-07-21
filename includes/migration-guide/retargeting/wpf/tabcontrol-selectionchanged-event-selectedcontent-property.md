---
ms.openlocfilehash: dfdb62e8dd6db67d4fd12aba93928f4615e3f284
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85614948"
---
### <a name="tabcontrol-selectionchanged-event-and-selectedcontent-property"></a>TabControl SelectionChanged イベントおよび SelectedContent プロパティ

#### <a name="details"></a>説明

.NET Framework 4.7.1、以降の<xref:System.Windows.Controls.TabControl>の値を更新、<xref:System.Windows.Controls.TabControl.SelectedContent>を発生させる前に、プロパティ、<xref:System.Windows.Controls.Primitives.Selector.SelectionChanged>イベント、その選択が変更されたときにします。 .NET Framework 4.7 と以前のバージョンでは、イベント後に SelectedContent への更新が発生しました。

#### <a name="suggestion"></a>提案される解決策

.NET Framework 4.7.1 以降を対象とするアプリでこの変更を無効にし、従来の動作を使用することができます。その場合、アプリケーション構成ファイルの `<runtime>` セクションに次の行を追加します。

<pre><code class="lang-xml">&lt;runtime&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.System.Windows.Controls.TabControl.SelectionPropertiesCanLagBehindSelectionChangedEvent=true&quot; /&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;</code></pre>

.NET Framework 4.7 以前を対象とするものの、.NET Framework 4.7.1 以降で実行されているアプリでは、新しい動作を有効にすることができます。その場合、アプリケーション構成ファイルの `<runtime>` セクションに次の行を追加します。

<pre><code class="lang-xml">&lt;runtime&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.System.Windows.Controls.TabControl.SelectionPropertiesCanLagBehindSelectionChangedEvent=false&quot; /&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;</code></pre>

| 名前    | 値       |
|:--------|:------------|
| スコープ   | マイナー       |
| バージョン | 4.7.1       |
| 種類    | 再ターゲット中 |

#### <a name="affected-apis"></a>影響を受ける API

- <xref:System.Windows.Controls.TabControl.SelectedContent?displayProperty=nameWithType>
- <xref:System.Windows.Controls.Primitives.Selector.SelectionChanged?displayProperty=nameWithType>
