---
ms.openlocfilehash: 0ef39d67cd4335658658f5772b5bce49d827cad0
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85614934"
---
### <a name="selector-selectionchanged-event-and-selectedvalue-property"></a>セレクター SelectionChanged イベントおよび SelectedValue プロパティ

#### <a name="details"></a>説明

NET Framework 4.7.1 以降、<xref:System.Windows.Controls.Primitives.Selector> は選択の変更が発生すると必ず、<xref:System.Windows.Controls.Primitives.Selector.SelectionChanged> イベントが発生する前に <xref:System.Windows.Controls.Primitives.Selector.SelectedValue%2A> プロパティの値を更新します。 これにより、SelectedValue プロパティと、イベント発生前に更新されるその他の選択プロパティ (<xref:System.Windows.Controls.Primitives.Selector.SelectedItem%2A> および <xref:System.Windows.Controls.Primitives.Selector.SelectedIndex%2A>) との整合性が確保されます。<p/>.NET Framework 4.7 以前のバージョンでは、ほとんどの場合、イベントの前に SelectedValue に対する更新が行われました。しかし、選択の変更が <xref:System.Windows.Controls.Primitives.Selector.SelectedValue%2A> プロパティの変更に起因している場合、SelectedValue に対する更新はイベントの後に行われていました。

#### <a name="suggestion"></a>提案される解決策

.NET Framework 4.7.1 以降を対象とするアプリでこの変更を無効にし、従来の動作を使用することができます。その場合、アプリケーション構成ファイルの `<runtime>` セクションに次の行を追加します。

<pre><code class="lang-xml">&lt;runtime&gt;&#13;&#10;&lt;AppContextSwitchOverrides&#13;&#10;value=&quot;Switch.System.Windows.Controls.TabControl.SelectionPropertiesCanLagBehindSelectionChangedEvent=true&quot; /&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;</code></pre>

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
