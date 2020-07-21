---
ms.openlocfilehash: 0b7d6d9543035ab0a8fdda675ae71572ace12a1f
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85620163"
---
### <a name="webutilityhtmldecode-no-longer-decodes-invalid-input-sequences"></a>WebUtility.HtmlDecode が無効な入力シーケンスをデコードしなくなった

#### <a name="details"></a>説明

既定では、デコード メソッドによって無効な入力シーケンスが無効な UTF-16 文字列にデコードされることがなくなりました。 代わりに、元の入力が返されます。

#### <a name="suggestion"></a>提案される解決策

デコーダーの出力の変更は、UTF-16 データではなくバイナリ データを文字列に格納した場合にのみ影響があります。 明示的にこの動作を制御するには、[appSettings](~/docs/framework/configure-apps/file-schema/appsettings/index.md) 要素の <code>aspnet:AllowRelaxedUnicodeDecoding</code> 属性を <code>true</code> に設定して従来の動作を有効にするか、<code>false</code> に設定して現在の動作を有効にします。

| 名前    | [値]       |
|:--------|:------------|
| スコープ   |マイナー|
|バージョン|4.5|
|種類|ランタイム

#### <a name="affected-apis"></a>影響を受ける API

-<xref:System.Net.WebUtility.HtmlDecode(System.String)?displayProperty=nameWithType></li><li><xref:System.Net.WebUtility.HtmlDecode(System.String,System.IO.TextWriter)?displayProperty=nameWithType></li><li><xref:System.Net.WebUtility.UrlDecode(System.String)?displayProperty=nameWithType></li></ul>|
