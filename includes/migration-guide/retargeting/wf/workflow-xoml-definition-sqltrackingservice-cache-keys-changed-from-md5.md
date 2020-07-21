---
ms.openlocfilehash: 7a7ecf052276fe8e62463498b83230d466630c79
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85616271"
---
### <a name="workflow-xoml-definition-and-sqltrackingservice-cache-keys-changed-from-md5-to-sha256"></a>ワークフロー XOML 定義および SqlTrackingService キャッシュ キーの MD5 から SHA256 への変更

#### <a name="details"></a>説明

ワークフロー ランタイムでは、XOML で定義されているワークフロー定義のキャッシュが保持されます。 また、SqlTrackingService では、文字列によってキー指定されるキャッシュが保持されます。 これらのキャッシュは、チェックサム ハッシュ値を含む値によってキー指定されます。 .NET Framework 4.7.2 以前のバージョンでは、このチェックサムのハッシュで MD5 アルゴリズムが使用され、FIPS 対応システムで問題が発生していました。 .NET Framework 4.8 以降では、SHA256 のアルゴリズムが使用されます。ワークフロー ランタイムと SqlTrackingService は開始されるたびに値が再計算されるため、この変更では互換性の問題は発生しないはずです。 しかし、後方互換が提供されるため、お客様は必要に応じて、従来のハッシュ アルゴリズムの使用に戻すことができます。

#### <a name="suggestion"></a>提案される解決策

この変更により、ワークフローの実行時に問題が生じる場合は、次のように、`AppContext` スイッチのいずれか、または両方を設定してみてください。

- &quot;Switch.System.Workflow.Runtime.UseLegacyHashForWorkflowDefinitionDispenserCacheKey&quot; を true にする。
- &quot;Switch.System.Workflow.Runtime.UseLegacyHashForSqlTrackingCacheKey&quot; を true にする。
コード内で以下のように指定します。

<pre><code class="lang-csharp">System.AppContext.SetSwitch(&quot;Switch.System.Workflow.Runtime.UseLegacyHashForWorkflowDefinitionDispenserCacheKey&quot;, true);&#13;&#10;System.AppContext.SetSwitch(&quot;Switch.System.Workflow.Runtime.UseLegacyHashForSqlTrackingCacheKey&quot;, true);&#13;&#10;</code></pre>

または、構成ファイルで次のようにします (<xref:System.Workflow.Runtime.WorkflowRuntime> オブジェクトを作成しているアプリケーションの構成ファイルで、このようにする必要があります)。

<pre><code class="lang-xml">&lt;configuration&gt;&#13;&#10;&lt;runtime&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.System.Workflow.Runtime.UseLegacyHashForWorkflowDefinitionDispenserCacheKey=true&quot; /&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.System.Workflow.Runtime.UseLegacyHashForSqlTrackingCacheKeytrue&quot; /&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;&lt;/configuration&gt;&#13;&#10;</code></pre>

| 名前    | [値]       |
|:--------|:------------|
| スコープ   | マイナー       |
| バージョン | 4.8         |
| 種類    | 再ターゲット中 |
