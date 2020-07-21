---
ms.openlocfilehash: 9c9c4ec55143ef991e9b69a389e0f3368263bb4e
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85614849"
---
### <a name="nullreferenceexception-in-exception-handling-code-from-imagesourceconverterconvertfrom"></a>ImageSourceConverter.ConvertFrom からの例外処理コード内の NullReferenceException

#### <a name="details"></a>説明

<xref:System.Windows.Media.ImageSourceConverter.ConvertFrom(System.ComponentModel.ITypeDescriptorContext,System.Globalization.CultureInfo,System.Object)> の例外処理コードのエラーでは、目的の例外 (<xref:System.IO.DirectoryNotFoundException?displayProperty=fullName> または <xref:System.IO.FileNotFoundException?displayProperty=fullName>) の代わりに <xref:System.NullReferenceException?displayProperty=fullName> が誤ってスローされていました。 この変更によりエラーが修正されるため、このメソッドは正しい例外をスローするようになりました。 <p/>既定では、.NET Framework 4.6.2 以前を対象とするすべてのアプリケーションが、引き続き互換性のために <xref:System.NullReferenceException?displayProperty=fullName> をスローします。 .NET Framework 4.7 以降を使用する開発者には、正しい例外が表示されます。

#### <a name="suggestion"></a>提案される解決策

NET Framework 4.7 以降を対象とする場合に <xref:System.NullReferenceException?displayProperty=fullName> を取得する構成に戻したい開発者は、アプリケーションの App.config ファイルに次のコードを追加/マージします。

<pre><code class="lang-xml">&lt;configuration&gt;&#13;&#10;&lt;runtime&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.System.Windows.Media.ImageSourceConverter.OverrideExceptionWithNullReferenceException=true&quot;/&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;&lt;/configuration&gt;&#13;&#10;</code></pre>

| 名前    | [値]       |
|:--------|:------------|
| スコープ   | エッジ        |
| バージョン | 4.7         |
| 種類    | 再ターゲット中 |

#### <a name="affected-apis"></a>影響を受ける API

- <xref:System.Windows.Media.ImageSourceConverter.ConvertFrom(System.ComponentModel.ITypeDescriptorContext,System.Globalization.CultureInfo,System.Object)?displayProperty=nameWithType>
