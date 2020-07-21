---
ms.openlocfilehash: e3b9711ac66901d69838de4c9f309d086b06fd4d
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85620517"
---
### <a name="xslt-forward-compat-now-works"></a>XSLT 上位互換が機能するようになった

#### <a name="details"></a>説明

.NET Framework 4 では、XSLT 1.0 の上位互換性に、次の問題がありました。<ul><li>バージョンが 2.0 に設定されているときに、パーサーが認識できない XSLT 1.0 コンストラクトに遭遇すると、スタイル シートの読み込みが失敗していました。</li><li>スタイル シートのバージョンが 1.1 に設定されている場合、<code>xsl:sort</code> コンストラクトでデータを並べ替えることができませんでした。</li></ul>.NET Framework 4.5 では、これらの問題は修正され、XSLT 1.0 の上位互換モードが正常に機能するようになりました。

#### <a name="suggestion"></a>提案される解決策

ほとんどのアプリには影響しませんが、xsl:sort が優先される場合は異なる方法でデータが並べ替えられます。 <code>xsl:sort</code> が 1.1 スタイル シートで使用されている場合は、アプリが並べ替えられていないデータの順序に依存していないことを確認してください。 アプリが 4.0 の並べ替え動作に依存している場合は、スタイル シートから <code>xsl:sort</code> を削除してください。

| 名前    | [値]       |
|:--------|:------------|
| スコープ   |エッジ|
|バージョン|4.5|
|種類|ランタイム

#### <a name="affected-apis"></a>影響を受ける API

-<xref:System.Xml.Xsl.XslCompiledTransform?displayProperty=nameWithType></li></ul>|
