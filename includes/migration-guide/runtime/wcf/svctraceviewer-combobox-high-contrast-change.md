---
ms.openlocfilehash: 06f4186e8f233f5c769dfc5e05d2de5eacd9b053
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85621992"
---
### <a name="svctraceviewer-combobox-high-contrast-change"></a>svcTraceViewer ComboBox のハイ コントラストの変更

#### <a name="details"></a>説明

[Microsoft Service Trace Viewer ツール](~/docs/framework/wcf/service-trace-viewer-tool-svctraceviewer-exe.md)では、特定のハイ コントラストのテーマで ComboBox コントロールが適切な色で表示されませんでした。 この問題は .NET Framework 4.7.2 で修正されました。 しかし、.NET Framework SDK の下位互換性要件により、既定ではお客様に修正が示されませんでした。 .NET 4.8 では、次の [AppContext 構成スイッチ](~/docs/framework/configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md)を svcTraceViewer.exe.config ファイルに追加することで、この変更が示されます。<pre><code class="lang-xml">&lt;AppContextSwitchOverrides value=&quot;Switch.UseLegacyAccessibilityFeatures=false;Switch.UseLegacyAccessibilityFeatures.2=false&quot; /&gt;&#13;&#10;</code></pre>

#### <a name="suggestion"></a>提案される解決策

<ul><li>変更を選択しない方法。ハイ コントラストの動作を変更したくない場合は、svcTraceViewer.exe.config ファイルから次のセクションを削除することで、無効にすることができます。</li></ul><pre><code class="lang-xml">&lt;AppContextSwitchOverrides value=&quot;Switch.UseLegacyAccessibilityFeatures=false;Switch.UseLegacyAccessibilityFeatures.2=false&quot; /&gt;&#13;&#10;</code></pre>

| 名前    | [値]       |
|:--------|:------------|
| スコープ   |エッジ|
|バージョン|4.8|
|種類|ランタイム|
