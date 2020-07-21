---
ms.openlocfilehash: aade03c29ff16053a97683499cf719a98ae33f3f
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85616274"
---
### <a name="add-selectiontextbrush-public-property-to-textboxpasswordbox-non-adorner-selection"></a>TextBox/PasswordBox の非装飾選択に SelectionTextBrush パブリック プロパティを追加する

#### <a name="details"></a>説明

<xref:System.Windows.Controls.TextBox> と <xref:System.Windows.Controls.PasswordBox> の[非装飾ベースのテキスト選択](https://github.com/Microsoft/dotnet/blob/master/Documentation/compatibility/wpf-TextBox-PasswordBox-text-selection-does-not-follow-system-colors.md)を使用する WPF アプリケーションでは、開発者は、選択されたテキストのレンダリングを変更するために、新しく追加された SelectionTextBrush プロパティを設定できるようになりました。  既定では、<xref:System.Windows.SystemColors.HighlightTextBrushKey> でこの色が変更されます。  非装飾ベースのテキスト選択が有効でない場合は、このプロパティで何も行われません。

#### <a name="suggestion"></a>提案される解決策

非装飾ベースのテキスト選択が有効になったら、<xref:System.Windows.Controls.PasswordBox.SelectionTextBrush?displayProperty=nameWithType> および <xref:System.Windows.Controls.Primitives.TextBoxBase.SelectionTextBrush> プロパティを使用して、選択されたテキストの外観を変更することができます。 これは XAML を使用して実行できます。

<pre><code class="lang-xaml">&lt;TextBox SelectionBrush=&quot;Red&quot; SelectionTextBrush=&quot;White&quot;  SelectionOpacity=&quot;0.5&quot;&#13;&#10;Foreground=&quot;Blue&quot; CaretBrush=&quot;Blue&quot;&gt;&#13;&#10;This is some text.&#13;&#10;&lt;/TextBox&gt;&#13;&#10;</code></pre>

| 名前    | [値]       |
|:--------|:------------|
| スコープ   | Major       |
| バージョン | 4.8         |
| 種類    | 再ターゲット中 |

#### <a name="affected-apis"></a>影響を受ける API

- <xref:System.Windows.Controls.Primitives.TextBoxBase.SelectionTextBrushProperty?displayProperty=nameWithType>
- <xref:System.Windows.Controls.Primitives.TextBoxBase.SelectionTextBrush?displayProperty=nameWithType>
- [System.Windows.Controls.TextBox](xref:System.Windows.Controls.TextBox)
- [System.Windows.Controls.PasswordBox](xref:System.Windows.Controls.PasswordBox)
