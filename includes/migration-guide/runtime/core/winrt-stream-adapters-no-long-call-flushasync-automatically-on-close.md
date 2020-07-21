---
ms.openlocfilehash: 60937459b6f18e9abae87ad2dc97c3942325eedc
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85620275"
---
### <a name="winrt-stream-adapters-no-long-call-flushasync-automatically-on-close"></a>終了時に WinRT ストリーム アダプターで FlushAsync が自動的に呼び出されなくなりました

#### <a name="details"></a>説明

Windows ストア アプリの Windows ランタイム ストリーム アダプターで、Dispose メソッドから FlushAsync メソッドが呼び出されなくなりました。

#### <a name="suggestion"></a>提案される解決策

この変更は透過的である必要があります。 開発者は次のようなコードを記述して以前の動作を復元できます。<pre><code class="lang-csharp">using (var stream = GetWindowsRuntimeStream() as Stream)&#13;&#10;{&#13;&#10;// do something&#13;&#10;await stream.FlushAsync();&#13;&#10;}&#13;&#10;</code></pre>

| 名前    | [値]       |
|:--------|:------------|
| スコープ   |透明|
|バージョン|4.5.1|
|種類|ランタイム|
