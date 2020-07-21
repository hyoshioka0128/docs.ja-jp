---
ms.openlocfilehash: 53ded5ae6e5a025fc7992da099c3481587bb6f31
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85614905"
---
### <a name="privatefontcollectionaddfontfile-method-releases-font-resources"></a>PrivateFontCollection.AddFontFile メソッドが Font リソースを解放する

#### <a name="details"></a>説明

.NET Framework 4.7.1 およびそれより前のバージョンの <xref:System.Drawing.Text.PrivateFontCollection?displayProperty=nameWithType> クラスは、<xref:System.Drawing.Text.PrivateFontCollection.AddFontFile(System.String)> メソッドを使用してこのコレクションに追加された <xref:System.Drawing.Font> オブジェクトの <xref:System.Drawing.Text.PrivateFontCollection> が破棄された後も、GDI+ フォント リソースを解放しません。 .NET Framework 4.7.2 およびそれより降の <xref:System.Drawing.Text.FontCollection.Dispose%2A> は、ファイルとしてコレクションに追加された GDI+ フォントを解放します。

#### <a name="suggestion"></a>提案される解決策

**これらの変更を選択する方法と選択しない方法** アプリケーションでこれらの変更を利用するには、.NET Framework 4.7.2 以降で実行する必要があります。 アプリケーションは、次のいずれかの方法でこれらの変更を利用できます。

- .NET Framework 4.7.2 を対象にして再コンパイルします。 .NET Framework 4.7.2 以降を対象とする Windows フォーム アプリケーションでは、この変更が既定で有効になります。
- .NET Framework 4.7.1 以前を対象にして、下の例のように、app.config ファイルの `<runtime>` セクションに次の [AppContext スイッチ](https://docs.microsoft.com/dotnet/framework/configure-apps/file-schema/runtime/appcontextswitchoverrides-element)を追加し、それを `false` に設定することで、以前のアクセシビリティ動作を無効にします。

<pre><code class="lang-xml">&lt;runtime&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.System.Drawing.Text.DoNotRemoveGdiFontsResourcesFromFontCollection=false&quot;/&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;</code></pre>

.NET Framework 4.7.2 以降を対象とするアプリケーションで以前の動作を残す場合、この AppContext スイッチを明示的に `true` に設定することで、フォント リソースを解放しないようにすることができます。

| 名前    | [値]       |
|:--------|:------------|
| スコープ   | エッジ        |
| バージョン | 4.7.2       |
| 種類    | 再ターゲット中 |

#### <a name="affected-apis"></a>影響を受ける API

- <xref:System.Drawing.Text.PrivateFontCollection.AddFontFile(System.String)?displayProperty=nameWithType>
- <xref:System.Drawing.Text.FontCollection.Dispose?displayProperty=nameWithType>
