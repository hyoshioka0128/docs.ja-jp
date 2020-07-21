---
ms.openlocfilehash: acb5b467fc8f0692d8fa1b3b8263fd27308cc124
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85617166"
---
### <a name="webutilityhtmlencode-and-webutilityhtmldecode-round-trip-bmp-correctly"></a>WebUtility.HtmlEncode と WebUtility.HtmlDecode で BMP が正常に往復する

#### <a name="details"></a>説明

.NET Framework 4.5 を対象とするアプリケーションの場合、基本多言語面 (BMP: Basic Multilingual Plane) の外部にある文字は、<xref:System.Net.WebUtility.HtmlDecode(System.String)> メソッドに渡されたときに正常に往復します。

#### <a name="suggestion"></a>提案される解決策

この変更は現在のアプリケーションには影響を与えないはずですが、元の動作を復元するには、`<httpRuntime>` 要素の `targetFramework` 属性を "4.5" 以外の文字列に設定します。 また、.NET Framework の対象バージョンに関係なくこの動作を制御するために `unicodeEncodingConformance` 構成要素の `unicodeDecodingConformance` 属性と `<webUtility>` 属性を設定することもできます。

| 名前    | [値]       |
|:--------|:------------|
| スコープ   | エッジ        |
| バージョン | 4.5         |
| 種類    | 再ターゲット中 |

#### <a name="affected-apis"></a>影響を受ける API

- <xref:System.Net.WebUtility.HtmlEncode(System.String)?displayProperty=nameWithType>
- <xref:System.Net.WebUtility.HtmlEncode(System.String,System.IO.TextWriter)?displayProperty=nameWithType>
