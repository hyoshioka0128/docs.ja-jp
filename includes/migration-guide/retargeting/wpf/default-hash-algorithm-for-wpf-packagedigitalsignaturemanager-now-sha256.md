---
ms.openlocfilehash: d3e0a61601f60a389b662f6f74934b6e6dc6e663
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85614919"
---
### <a name="the-default-hash-algorithm-for-wpf-packagedigitalsignaturemanager-is-now-sha256"></a>WPF PackageDigitalSignatureManager の既定のハッシュ アルゴリズムが SHA256 になりました

#### <a name="details"></a>説明

`System.IO.Packaging.PackageDigitalSignatureManager` は、WPF パッケージに関連してデジタル署名の機能を提供します。  .NET Framework 4.7 以前のバージョンでは、パッケージのパーツへの署名に使用される既定のアルゴリズム (<xref:System.IO.Packaging.PackageDigitalSignatureManager.DefaultHashAlgorithm?displayProperty=nameWithType>) は SHA1 でした。  最近明らかになった SHA1 のセキュリティに関する懸念事項により、この既定値は .NET Framework 4.7.1 で開始する SHA256 に変更されています。  この変更は、XPS ドキュメントを含むあらゆるパッケージの署名に影響します。

#### <a name="suggestion"></a>提案される解決策

.NET Framework 4.7.1 より前のフレームワーク バージョンを対象とするときにこの変更を利用する開発者または .NET Framework 4.7.1 以上を対象とするときに以前の機能を必要とする開発者は、次の AppContext フラグを適宜設定することができます。  true の値を設定すると、SHA1 が既定のアルゴリズムとして使用され、false の値を設定すると SHA256 が使用されます。<pre><code class="lang-xml">&lt;configuration&gt;&#13;&#10;&lt;runtime&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.MS.Internal.UseSha1AsDefaultHashAlgorithmForDigitalSignatures=true&quot;/&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;&lt;/configuration&gt;&#13;&#10;</code></pre>

| 名前    | [値]       |
|:--------|:------------|
| スコープ   | エッジ        |
| バージョン | 4.7.1       |
| 種類    | 再ターゲット中 |

#### <a name="affected-apis"></a>影響を受ける API

- <xref:System.IO.Packaging.PackageDigitalSignatureManager.DefaultHashAlgorithm?displayProperty=nameWithType>
