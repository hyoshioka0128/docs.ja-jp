---
ms.openlocfilehash: 4303b177ffe01328965c909a5a3809414fcead91
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85614933"
---
### <a name="the-default-hash-algorithm-for-wpfs-markup-compiler-is-now-sha256"></a>WPF のマークアップ コンパイラの既定のハッシュ アルゴリズムが SHA256 になった

#### <a name="details"></a>説明

WPF マークアップ コンパイラでは、XAML マークアップ ファイルのコンパイル サービスが提供されます。  .NET Framework 4.7.1 以前のバージョンでは、チェックサムで使用される既定のハッシュ アルゴリズムは SHA1 でした。 最近明らかになった SHA1 のセキュリティに関する懸念事項により、.NET Framework 4.7.2 以降では、この既定値は SHA256 に変更されています。  この変更は、コンパイル中のマークアップ ファイルのすべてのチェックサム生成に影響します。

#### <a name="suggestion"></a>提案される解決策

.NET Framework 4.7.2 以降を対象とし、SHA1 ハッシュの動作に戻す開発者は、以下の AppContext フラグを設定する必要があります。

<pre><code class="lang-xml">&lt;configuration&gt;&#13;&#10;&lt;runtime&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.System.Windows.Markup.DoNotUseSha256ForMarkupCompilerChecksumAlgorithm=true&quot;/&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;&lt;/configuration&gt;&#13;&#10;</code></pre>

.NET 4.7.2 より前のバージョンのフレームワークを対象とするときに SHA256 ハッシュを利用する開発者は、以下の AppContext フラグを設定する必要があります。  インストールされている .NET Framework のバージョンは 4.7.2 以降である必要があることに注意してください。

<pre><code class="lang-xml">&lt;configuration&gt;&#13;&#10;&lt;runtime&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.System.Windows.Markup.DoNotUseSha256ForMarkupCompilerChecksumAlgorithm=false&#13;&#10;&lt;/runtime&gt;&#13;&#10;&lt;/configuration&gt;&#13;&#10;</code></pre>

| 名前    | [値]       |
|:--------|:------------|
| スコープ   | 透明 |
| バージョン | 4.7.2       |
| 種類    | 再ターゲット中 |
