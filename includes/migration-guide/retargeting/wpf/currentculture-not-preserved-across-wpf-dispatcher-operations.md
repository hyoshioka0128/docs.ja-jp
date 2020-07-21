---
ms.openlocfilehash: bd656478a55856e676853e57f3e7386ea0aa0211
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85614822"
---
### <a name="currentculture-is-not-preserved-across-wpf-dispatcher-operations"></a>CurrentCulture が、複数の WPF ディスパッチャー操作にわたって維持されない

#### <a name="details"></a>説明

.NET Framework 4.6 以降では、<xref:System.Windows.Threading.Dispatcher?displayProperty=fullName> 内で <xref:System.Globalization.CultureInfo.CurrentCulture?displayProperty=fullName> または <xref:System.Globalization.CultureInfo.CurrentUICulture?displayProperty=fullName> に加えられた変更は、そのディスパッチャー操作の終了時に失われます。 同様に、ディスパッチャー操作の外部で <xref:System.Globalization.CultureInfo.CurrentCulture?displayProperty=fullName> または <xref:System.Globalization.CultureInfo.CurrentUICulture?displayProperty=fullName> に加えられた変更は、その操作の実行時には反映されない場合があります。具体的に言うと、<xref:System.Globalization.CultureInfo.CurrentCulture?displayProperty=fullName> と <xref:System.Globalization.CultureInfo.CurrentUICulture?displayProperty=fullName> の変更は、WPF UI コールバックと WPF アプリケーション内の他のコードの間でフローされない場合があるということです。これは、<xref:System.Threading.ExecutionContext?displayProperty=fullName> の変更によるものであり、この変更により、.NET Framework 4.6 以降を対象とするアプリでは、<xref:System.Globalization.CultureInfo.CurrentCulture?displayProperty=fullName> および <xref:System.Globalization.CultureInfo.CurrentUICulture?displayProperty=fullName> は実行コンテキストに格納されます。 WPF ディスパッチャー操作は、操作を開始するために使用された実行コンテキストを格納して、操作が完了したときに、以前のコンテキストを復元します。 <xref:System.Globalization.CultureInfo.CurrentCulture?displayProperty=fullName> と <xref:System.Globalization.CultureInfo.CurrentUICulture?displayProperty=fullName> がそのコンテキストの一部になったため、ディスパッチャー操作内でそれらに加えられた変更は、操作の外部では保持されません。

#### <a name="suggestion"></a>提案される解決策

この変更による影響を受けるアプリは、望ましい <xref:System.Globalization.CultureInfo.CurrentCulture?displayProperty=fullName> または <xref:System.Globalization.CultureInfo.CurrentUICulture?displayProperty=fullName> をフィールドに格納し、すべてのディスパッチャー操作の本体 (UI イベントのコールバック ハンドラーを含む) で、正しい <xref:System.Globalization.CultureInfo.CurrentCulture?displayProperty=fullName> と <xref:System.Globalization.CultureInfo.CurrentUICulture?displayProperty=fullName> が設定されていることを確認することによって回避できます。 または、この WPF の変更の元となっている ExecutionContext の変更は、.NET Framework 4.6 以降を対象とするアプリのみに影響するため、.NET Framework 4.5.2 を対象とすることによって、この問題を回避できます。また、.NET Framework 4.6 以降を対象とするアプリでは、以下の互換性スイッチを設定することでこの問題を回避することができます。

<pre><code class="lang-csharp">AppContext.SetSwitch(&quot;Switch.System.Globalization.NoAsyncCurrentCulture&quot;, true);&#13;&#10;</code></pre>

この問題は、.NET Framework 4.6.2 の WPF で修正されました。 また、.NET Frameworks 4.6、4.6.1 では [KB 3139549](https://support.microsoft.com/kb/3139549) を通じて修正されました。 .NET Framework 4.6 以降を対象とするアプリケーションでは WPF アプリケーション (<xref:System.Globalization.CultureInfo.CurrentCulture?displayProperty=fullName>/<xref:System.Globalization.CultureInfo.CurrentUICulture?displayProperty=fullName>) の正しい動作が自動的に取得されます。これは、ディスパッチャー操作にわたって維持されます。

| 名前    | 値       |
|:--------|:------------|
| スコープ   | マイナー       |
| バージョン | 4.6         |
| 種類    | 再ターゲット中 |
