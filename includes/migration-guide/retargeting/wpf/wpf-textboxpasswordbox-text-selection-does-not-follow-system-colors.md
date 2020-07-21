---
ms.openlocfilehash: 7c2e80669d9ef27f87cde9442d8eeab0ee31a524
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85614976"
---
### <a name="wpf-textboxpasswordbox-text-selection-does-not-follow-system-colors"></a>WPF TextBox/PasswordBox のテキスト選択がシステム カラーに従っていない

#### <a name="details"></a>説明

.NET Framework 4.7.1 以前のバージョンでは、WPF の `System.Windows.Controls.TextBox` および `System.Windows.Controls.PasswordBox` は装飾層のテキスト選択のみをレンダリングできました。 そのため、一部のシステム テーマではテキストが遮られ、読みにくくなっていました。  .NET framework 4.7.2 以降では、開発者は、この問題を軽減する非装飾ベースの選択レンダリング スキームを有効にするオプションを選択することができます。

#### <a name="suggestion"></a>提案される解決策

この変更を利用する開発者は、次の AppContext フラグを適切に設定する必要があります。  この機能を利用するには、インストールされている .NET Framework のバージョンが 4.7.2 以上である必要があります。非装飾ベースの選択を有効にするには、次の AppContext フラグを使用します。<pre><code class="lang-xml">&lt;configuration&gt;&#13;&#10;&lt;runtime&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.System.Windows.Controls.Text.UseAdornerForTextboxSelectionRendering=false&quot;/&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;&lt;/configuration&gt;&#13;&#10;</code></pre>

| 名前    | [値]       |
|:--------|:------------|
| スコープ   | エッジ        |
| バージョン | 4.7.2       |
| 種類    | 再ターゲット中 |
