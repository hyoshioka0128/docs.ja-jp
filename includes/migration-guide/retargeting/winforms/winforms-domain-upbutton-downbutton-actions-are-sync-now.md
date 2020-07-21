---
ms.openlocfilehash: f75a652f15be6b0d184db20dc5cd8aafd80539fe
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85614906"
---
### <a name="winforms-domain-upbutton-and-downbutton-actions-are-in-sync-now"></a>WinForm の Domain upbutton アクションと downbutton アクションが同期するようになった

#### <a name="details"></a>説明

.NET Framework 4.7.1 およびそれより前のバージョンでは、コントロールにテキストが存在すると <xref:System.Windows.Forms.DomainUpDown> コントロールの <xref:System.Windows.Forms.DomainUpDown.UpButton?displayProperty=nameWithType> アクションが無視され、開発者は <xref:System.Windows.Forms.DomainUpDown.UpButton?displayProperty=nameWithType> アクションを使用する前にコントロールで <xref:System.Windows.Forms.DomainUpDown.DownButton?displayProperty=nameWithType> アクションを使用する必要があります。 .NET Framework 4.7.2 以降では、このシナリオで <xref:System.Windows.Forms.DomainUpDown.UpButton?displayProperty=nameWithType> アクションと <xref:System.Windows.Forms.DomainUpDown.DownButton?displayProperty=nameWithType> アクションの両方が独立して動作し、同期を維持します。

#### <a name="suggestion"></a>提案される解決策

アプリケーションでこれらの変更を利用するには、.NET Framework 4.7.2 以降で実行する必要があります。 アプリケーションは、次のいずれかの方法でこれらの変更を利用できます。

- .NET Framework 4.7.2 を対象にして再コンパイルします。 .NET Framework 4.7.2 以降を対象とする Windows フォーム アプリケーションでは、この変更が既定で有効になります。
- 下の例のように、app.config ファイルの `<runtime>` セクションに次の [AppContext スイッチ](https://docs.microsoft.com/dotnet/framework/configure-apps/file-schema/runtime/appcontextswitchoverrides-element)を追加し、それを `false` に設定することで、以前のスクロール動作を無効にします。

<pre><code class="lang-xml">&lt;runtime&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.System.Windows.Forms.DomainUpDown.UseLegacyScrolling=false&quot;/&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;</code></pre>

| 名前    | [値]       |
|:--------|:------------|
| スコープ   | エッジ        |
| バージョン | 4.7.2       |
| 種類    | 再ターゲット中 |

#### <a name="affected-apis"></a>影響を受ける API

- <xref:System.Windows.Forms.DomainUpDown.UpButton?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DomainUpDown.DownButton?displayProperty=nameWithType>
