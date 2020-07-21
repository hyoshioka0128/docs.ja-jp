---
ms.openlocfilehash: 0470cefc05fb5da6a6195ee0a96f04feef01fd10
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85620433"
---
### <a name="flowdocument-may-show-an-extra-line-of-text"></a>FlowDocument でテキストの余分な行が表示される場合がある

#### <a name="details"></a>説明

.NET Framework 4.0 での実行時の表示と比べて、.NET Framework 4.5 での実行時に <xref:System.Windows.Documents.FlowDocument> 要素でテキストの余分な行が表示されることがあります。 変更によってテキストが正しく表示されなくなったり、読みにくくなったりするようなことはありませんが、以前は <xref:System.Windows.Documents.FlowDocument> のビューから除外されていたテキストが表示される可能性があります。

#### <a name="suggestion"></a>提案される解決策

場合によっては、表示要素の PageHeight プロパティを 1 ずつ減らすことで、表示行の以前の数を復元できます。

| 名前    | [値]       |
|:--------|:------------|
| スコープ   |エッジ|
|バージョン|4.5|
|種類|ランタイム

#### <a name="affected-apis"></a>影響を受ける API

-<xref:System.Windows.Documents.FlowDocument.%23ctor></li><li><xref:System.Windows.Documents.FlowDocument.%23ctor(System.Windows.Documents.Block)></li><li><xref:System.Windows.Controls.FlowDocumentReader.%23ctor></li><li><xref:System.Windows.Controls.FlowDocumentPageViewer.%23ctor></li><li><xref:System.Windows.Controls.Primitives.DocumentPageView.%23ctor></li></ul>|
