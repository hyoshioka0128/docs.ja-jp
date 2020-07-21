---
ms.openlocfilehash: f907cb1939e111c586d68243e6b8a8e291974e36
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85615723"
---
### <a name="wpf-layout-rounding-of-margins-has-changed"></a>WPF レイアウトでの余白の丸め方の変更

#### <a name="details"></a>説明

余白、境界線、およびそれらの内部の背景の丸め処理の方法が変更されました。 この変更の結果、以下のようになります。

- 要素の幅または高さが最大で 1 ピクセル拡大または縮小することがあります。
- オブジェクトの配置が最大で 1 ピクセル移動することがあります。
- 中央揃えの要素が中央から最大で 1 ピクセル垂直まは水平方向にずれることがあります。
既定では、この新しいレイアウトは .NET Framework の 4.6 を対象とするアプリに対してのみ有効となります。

#### <a name="suggestion"></a>提案される解決策

この変更では、DPI が高いときにWPF コントロールの一番右または一番下でクリッピングの発生を除去する傾向があるため、app.config ファイルの `<runtime>` セクションに次の行を追加することによって、以前のバージョンの .NET Framework を対象としながら .NET Framework 4.6 上で実行されているアプリがこの新しい動作を選択ことができます。

<pre><code class="lang-xml">&lt;AppContextSwitchOverrides value=&quot;Switch.MS.Internal.DoNotApplyLayoutRoundingToMarginsAndBorderThickness=false&quot; /&gt;&#39;&#13;&#10;</code></pre>

.NET Framework 4.6 を対象としながら以前のレイアウト アルゴリズムを使用して WPF コントロールをレンダリングする必要があるアプリの場合、app.config ファイルの `<runtime>` セクションに次の行を追加することによってそれを行うことができます。

<pre><code class="lang-xml">&lt;AppContextSwitchOverrides value=&quot;Switch.MS.Internal.DoNotApplyLayoutRoundingToMarginsAndBorderThickness=true&quot; /&gt;&#39;.&#13;&#10;</code></pre>

| 名前    | 値       |
|:--------|:------------|
| スコープ   | マイナー       |
| バージョン | 4.6         |
| 種類    | 再ターゲット中 |
