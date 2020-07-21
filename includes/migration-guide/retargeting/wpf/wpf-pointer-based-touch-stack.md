---
ms.openlocfilehash: eb89cbc72d8b09fd1aa5bc775a6c539eb208fa70
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85614892"
---
### <a name="wpf-pointer-based-touch-stack"></a>WPF ポインター ベースのタッチ スタック

#### <a name="details"></a>説明

この変更で、オプションの WM_POINTER ベースの WPF タッチ/スタイラス スタックを有効にする機能が追加されます。  これを明示的に有効にしていない開発者は、WPF タッチ/スタイラス動作の変更を確認できません。オプションの WM_POINTER ベースのタッチ/スタイラス スタックに関する現在の既知の問題を以下に示します。

- リアルタイム インクがサポートされない。
- インクと StylusPlugins がまだ機能している間は、UI スレッドで処理されますが、パフォーマンスの低下につながる可能性があります。
- プロモーションの変更により、タッチ/スタイラス イベントからマウス イベントに動作が変更される。
- 操作の動作が異なる場合があります。
- ドラッグ/ドロップでは、タッチ入力の適切なフィードバックが表示されません。
- これはスタイラス入力には影響しません。
- ドラッグ/ドロップは、タッチ/スタイラス イベントで開始できなくなりました。
- そのため、マウス入力が検出されるまで、アプリケーションがハングする可能性があります。
- 代わりに、開発者はマウス イベントからドラッグ アンド ドロップを開始する必要があります。

#### <a name="suggestion"></a>提案される解決策

このスタックを有効にする開発者は、アプリケーションの App.config ファイルに次の行を追加/マージできます。

<pre><code class="lang-xml">&lt;configuration&gt;&#13;&#10;&lt;runtime&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.System.Windows.Input.Stylus.EnablePointerSupport=true&quot;/&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;&lt;/configuration&gt;&#13;&#10;</code></pre>

これを削除するか、値を false に設定すると、このオプションのスタックがオフになります。このスタックは Windows 10 Creators Update 以降でのみ使用できることに注意してください。

| 名前    | 値       |
|:--------|:------------|
| スコープ   | エッジ        |
| バージョン | 4.7         |
| 種類    | 再ターゲット中 |
