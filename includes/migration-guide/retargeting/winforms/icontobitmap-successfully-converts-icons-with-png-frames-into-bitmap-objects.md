---
ms.openlocfilehash: 811b1a91169eeebfa056d9ecdb07d342d3b32d85
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85615714"
---
### <a name="icontobitmap-successfully-converts-icons-with-png-frames-into-bitmap-objects"></a>PNG フレームを含んだアイコンが Icon.ToBitmap によって、Bitmap オブジェクトに正常に変換されます

#### <a name="details"></a>説明

.NET Framework 4.6 以降を対象にしたアプリでは、<xref:System.Drawing.Icon.ToBitmap%2A?displayProperty=nameWithType> メソッドで、PNG フレームを含んだアイコンを正常に Bitmap オブジェクトに変換できます。<p/>.NET Framework 4.5.2 以前のバージョンを対象としたアプリでは、Icon オブジェクトに PNG フレームが含まれていると、<xref:System.Drawing.Icon.ToBitmap%2A?displayProperty=nameWithType> メソッドが <xref:System.ArgumentOutOfRangeException> の例外をスローします。<p/>この変更は、.NET Framework 4.6 を対象として再コンパイルされたアプリのうち、Icon オブジェクトに PNG フレームが含まれている場合は <xref:System.ArgumentOutOfRangeException> をスローするように特別な処理が実装されているアプリに影響します。 .NET Framework 4.6 で実行している場合は、正常に変換が行われ、 <xref:System.ArgumentOutOfRangeException> がスローされることはないため、例外ハンドラーは呼び出されません。

#### <a name="suggestion"></a>提案される解決策

この動作に不都合がある場合は、次に示す要素を app.config ファイルの `<runtime>` セクションに追加することで、以前の動作を維持できます。

<pre><code class="lang-xml">&lt;AppContextSwitchOverrides&#13;&#10;value=&quot;Switch.System.Drawing.DontSupportPngFramesInIcons=true&quot; /&gt;&#13;&#10;</code></pre>

app.config ファイルに既に `AppContextSwitchOverrides` 要素が含まれている場合は、次に示すように新しい値を value 属性にマージする必要があります。

<pre><code class="lang-xml">&lt;AppContextSwitchOverrides&#13;&#10;value=&quot;Switch.System.Drawing.DontSupportPngFramesInIcons=true;&lt;previous key&gt;=&lt;previous value&gt;&quot; /&gt;&#13;&#10;</code></pre>

| 名前    | 値       |
|:--------|:------------|
| スコープ   | マイナー       |
| バージョン | 4.6         |
| 種類    | 再ターゲット中 |

#### <a name="affected-apis"></a>影響を受ける API

- <xref:System.Drawing.Icon.ToBitmap?displayProperty=nameWithType>
