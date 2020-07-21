---
ms.openlocfilehash: 8f03e5166e7f1f598e9bba7fb8c550809f287b82
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85615648"
---
### <a name="htmltextwriter-does-not-render-br-element-correctly"></a>HtmlTextWriter によって `<br/>` 要素が正しく表示されない

#### <a name="details"></a>説明

.NET Framework 4.6 以降では、`<BR />` 要素を指定して <xref:System.Web.UI.HtmlTextWriter.RenderBeginTag(System.String)> と <xref:System.Web.UI.HtmlTextWriter.RenderEndTag> を呼び出すと、`<BR />` が 1 つのみ (2 つではなく) 正しく挿入されます。

#### <a name="suggestion"></a>提案される解決策

アプリが余分な `<BR />` タグに依存している場合は、<xref:System.Web.UI.HtmlTextWriter.RenderBeginTag(System.String)> をもう一度呼び出す必要があります。 この動作の変更は、.NET Framework 4.6 以降を対象とするアプリにのみ影響するので、以前の動作を得るためには、以前のバージョンの .NET Framework を対象とするという方法もあります。

| 名前    | 値       |
|:--------|:------------|
| スコープ   | エッジ        |
| バージョン | 4.6         |
| 種類    | 再ターゲット中 |

#### <a name="affected-apis"></a>影響を受ける API

- <xref:System.Web.UI.HtmlTextWriter.RenderBeginTag(System.String)?displayProperty=nameWithType>
- <xref:System.Web.UI.HtmlTextWriter.RenderBeginTag(System.Web.UI.HtmlTextWriterTag)?displayProperty=nameWithType>
