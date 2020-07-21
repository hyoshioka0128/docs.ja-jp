---
ms.openlocfilehash: ca369c4e3f78648c6e8e0bcb5d54711d3009a769
ms.sourcegitcommit: cb27c01a8b0b4630148374638aff4e2221f90b22
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/09/2020
ms.locfileid: "86174265"
---
### <a name="blazor-insignificant-whitespace-trimmed-from-components-at-compile-time"></a>Blazor: コンパイル時にコンポーネントからトリミングされる無意味な空白文字

ASP.NET Core 5.0 Preview 7 より、Razor コンパイラでは、コンパイル時に Blazor コンポーネント ( *.razor* ファイル) の無意味な空白文字が除外されます。 ディスカッションについては、イシュー [dotnet/aspnetcore#23568](https://github.com/dotnet/aspnetcore/issues/23568) を参照してください。

#### <a name="version-introduced"></a>導入されたバージョン

5.0 Preview 7

#### <a name="old-behavior"></a>以前の動作

Blazor Server と Blazor WebAssembly の 3.x バージョンでは、コンポーネントのソース コードで空白文字が許可されます。 空白文字のみのテキスト ノードは、視覚効果がないときでも、ブラウザーのドキュメント オブジェクト モデル (DOM) にレンダリングされます。

次の Blazor コンポーネント コードについて考えてみましょう。

```razor
<ul>
    @foreach (var item in Items)
    {
        <li>
            @item.Text
        </li>
    }
</ul>
```

前の例では、次の場所で 2 つの空白文字ノードがレンダリングされます。

* `@foreach` コード ブロックの外側。
* `<li>` 要素の前後。
* `@item.Text` 出力の前後。

100 項目が含まれるリストの場合、402 の空白文字ノードが生成されます。 これは、レンダリングされる出力に視覚的に影響を与える空白文字ノードがない場合でも、レンダリングされる全ノードの半分以上です。

コンポーネントの静的 HTML をレンダリングする場合、タグ内の空白文字は保持されませんでした。 たとえば、次のコンポーネントのソースをご覧ください。

```razor
<foo        bar="baz"     />
```

空白文字が保持されていません。 プレレンダリングされた出力は次のようになります。

```razor
<foo bar="baz" />
```

#### <a name="new-behavior"></a>新しい動作

`@preservewhitespace` ディレクティブが値 `true` と共に使用されない限り、空白文字ノードは次の場合に削除されます。

* 要素内で先頭または末尾にある。
* `RenderFragment` パラメーター内の先頭または末尾にある。 たとえば、別のコンポーネントに渡される子コンテンツです。
* `@if` や `@foreach` のような、C# コード ブロックの前か後にある。

#### <a name="reason-for-change"></a>変更理由

ASP.NET Core 5.0 の Blazor の目標は、レンダリングと比較のパフォーマンスを改善することです。 無意味な空白文字ツリー ノードによって、ベンチマークでは、レンダリング時間の最大 40% が消費されていました。

#### <a name="recommended-action"></a>推奨アクション

ほとんどの場合、レンダリングされたコンポーネントのビジュアル レイアウトは影響を受けません。 ただし、空白文字の削除は、`white-space: pre` などの CSS ルールを使用するときに、レンダリングされた出力に影響を与えることがあります。 このパフォーマンスの最適化を無効にして、空白を保持するには、次のいずれかの操作を実行します。

* 特定のコンポーネントに設定を適用するには、 *.razor* ファイルの先頭に `@preservewhitespace true` ディレクティブを追加する。
* サブディレクトリ全体またはプロジェクト全体に設定を適用するには、 *_Imports.razor* ファイル内に `@preservewhitespace true` ディレクティブを追加する。

ほとんどの場合、アプリケーションでは一般的に通常の動作が続行されるため (ただし、速くなります)、何の措置も必要ありません。 空白文字の削除で特定のコンポーネントに問題が発生する場合、そのコンポーネントで `@preservewhitespace true` を使用し、この最適化を無効にします。

#### <a name="category"></a>カテゴリ

ASP.NET Core

#### <a name="affected-apis"></a>影響を受ける API

None

<!--

#### Affected APIs

Not detectable via API analysis

-->
