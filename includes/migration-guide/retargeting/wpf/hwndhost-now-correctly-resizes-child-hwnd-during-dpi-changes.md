---
ms.openlocfilehash: 3d1dc8dec18212afd815aa3de7fc82c8a1f680dc
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85616275"
---
### <a name="hwndhost-now-correctly-resizes-child-hwnd-during-dpi-changes"></a>HwndHost で DPI 変更中に子の HWND のサイズが正しく変更されるようになった

#### <a name="details"></a>説明

.NET Framework 4.7.2 以前のバージョンでは、WPF がモニターごとの認識モードで実行されていた場合、モニター間でアプリケーションを移動するときなど、DPI の変更後に、<xref:System.Windows.Interop.HwndHost> 内でホストされていたコントロールのサイズが正しく変更されませんでした。 この修正により、確実に、ホストされるコントロールのサイズが適切に変更されるようになります。

#### <a name="suggestion"></a>提案される解決策

アプリケーションでこれらの変更を利用するには、.NET Framework 4.7.2 以降で実行する必要があり、以下の例のように、アプリ構成ファイルの `<runtime>` セクションの次の [AppContext スイッチ](https://docs.microsoft.com/dotnet/framework/configure-apps/file-schema/runtime/appcontextswitchoverrides-element)を `false` に設定し、この動作を選択する必要があります。

<pre><code class="lang-xml">&lt;?xml version=&quot;1.0&quot; encoding=&quot;utf-8&quot;?&gt;&#13;&#10;&lt;configuration&gt;&#13;&#10;&lt;startup&gt;&#13;&#10;&lt;supportedRuntime version=&quot;v4.0&quot; sku=&quot;.NETFramework,Version=v4.7&quot;/&gt;&#13;&#10;&lt;/startup&gt;&#13;&#10;&lt;runtime&gt;&#13;&#10;&lt;!-- AppContextSwitchOverrides value attribute is in the form of &#39;key1=true/false;key2=true/false  --&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.System.Windows.DoNotUsePresentationDpiCapabilityTier2OrGreater=false&quot; /&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;&lt;/configuration&gt;&#13;&#10;</code></pre>

| 名前    | [値]       |
|:--------|:------------|
| スコープ   | Major       |
| バージョン | 4.8         |
| 種類    | 再ターゲット中 |
