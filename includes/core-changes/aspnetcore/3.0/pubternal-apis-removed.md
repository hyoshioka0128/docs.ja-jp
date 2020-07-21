---
ms.openlocfilehash: b1fb9647091cecb80b9c2f04ec9b6bb156eb39ba
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/05/2020
ms.locfileid: "84466841"
---
### <a name="pubternal-apis-removed"></a>"Pubternal" API の削除

ASP.NET Core のパブリック API サーフェイスを管理しやすくするため、`*.Internal` 名前空間のほとんどの型 (:::no-loc text="\"pubternal\""::: API と呼んでいたもの) が本当に internal になりました。 これらの名前空間のメンバーは、公開 API としてサポートされるべきものではありませんでした。 API の破壊的変更はマイナー リリースで発生する可能性があり、よく発生しています。 ASP.NET Core 3.0 に更新すると、これらの API に依存するコードは破壊的変更の影響を受けます。

詳細については、[dotnet/aspnetcore#4932](https://github.com/dotnet/aspnetcore/issues/4932) および [dotnet/aspnetcore#11312](https://github.com/dotnet/aspnetcore/issues/11312) を参照してください。

#### <a name="version-introduced"></a>導入されたバージョン

3.0

#### <a name="old-behavior"></a>以前の動作

影響を受ける API は `public` アクセス修飾子でマークされ、`*.Internal` 名前空間に存在します。

#### <a name="new-behavior"></a>新しい動作

影響を受ける API は、[internal](/dotnet/csharp/language-reference/keywords/internal) アクセス修飾子でマークされ、そのアセンブリ外のコードでは使用できなくなります。

#### <a name="reason-for-change"></a>変更理由

これらの :::no-loc text="\"pubternal\""::: API のガイダンスでは以下が示されていました。

* 予告なしに変更されることがあります。
* 破壊的変更を防ぐために、.NET ポリシーの対象ではありません。

API を `public` (`*.Internal` 名前空間でも) にしておくことは、ユーザーにとって混乱を招きます。

#### <a name="recommended-action"></a>推奨アクション

これらの :::no-loc text="\"pubternal\""::: API の使用を停止します。 代わりの API について不明点がある場合は、[dotnet/aspnetcore](https://github.com/dotnet/aspnetcore/issues) リポジトリで問題を提起します。

たとえば、ASP.NET Core 2.2 プロジェクトの次の HTTP 要求バッファーリング コードを考えてみます。 `EnableRewind` 拡張メソッドは、`Microsoft.AspNetCore.Http.Internal` 名前空間に存在します。

```csharp
HttpContext.Request.EnableRewind();
```

ASP.NET Core 3.0 プロジェクトで、`EnableRewind` 呼び出しを `EnableBuffering` 拡張メソッドへの呼び出しで置き換えます。 要求バッファーリング機能は、以前と同様に機能します。 `EnableBuffering` は `internal` API を呼び出すようになりました。

```csharp
HttpContext.Request.EnableBuffering();
```

#### <a name="category"></a>カテゴリ

ASP.NET Core

#### <a name="affected-apis"></a>影響を受ける API

名前空間名に `Internal` セグメントが含まれる、`Microsoft.AspNetCore.*` 名前空間と `Microsoft.Extensions.*` 名前空間のすべての API。 次に例を示します。

- `Microsoft.AspNetCore.Authentication.Internal`
- `Microsoft.AspNetCore.Builder.Internal`
- `Microsoft.AspNetCore.DataProtection.Cng.Internal`
- `Microsoft.AspNetCore.DataProtection.Internal`
- `Microsoft.AspNetCore.Hosting.Internal`
- `Microsoft.AspNetCore.Http.Internal`
- `Microsoft.AspNetCore.Mvc.Core.Infrastructure`
- `Microsoft.AspNetCore.Mvc.Core.Internal`
- `Microsoft.AspNetCore.Mvc.Cors.Internal`
- `Microsoft.AspNetCore.Mvc.DataAnnotations.Internal`
- `Microsoft.AspNetCore.Mvc.Formatters.Internal`
- `Microsoft.AspNetCore.Mvc.Formatters.Json.Internal`
- `Microsoft.AspNetCore.Mvc.Formatters.Xml.Internal`
- `Microsoft.AspNetCore.Mvc.Internal`
- `Microsoft.AspNetCore.Mvc.ModelBinding.Internal`
- `Microsoft.AspNetCore.Mvc.Razor.Internal`
- `Microsoft.AspNetCore.Mvc.RazorPages.Internal`
- `Microsoft.AspNetCore.Mvc.TagHelpers.Internal`
- `Microsoft.AspNetCore.Mvc.ViewFeatures.Internal`
- `Microsoft.AspNetCore.Rewrite.Internal`
- `Microsoft.AspNetCore.Routing.Internal`
- `Microsoft.AspNetCore.Server.Kestrel.Core.Adapter.Internal`
- `Microsoft.AspNetCore.Server.Kestrel.Core.Internal.Http`
- `Microsoft.AspNetCore.Server.Kestrel.Core.Internal.Infrastructure`
- `Microsoft.AspNetCore.Server.Kestrel.Https.Internal`

<!--

#### Affected APIs

- `N:Microsoft.AspNetCore.Authentication.Internal`
- `N:Microsoft.AspNetCore.Builder.Internal`
- `N:Microsoft.AspNetCore.DataProtection.Cng.Internal`
- `N:Microsoft.AspNetCore.DataProtection.Internal`
- `N:Microsoft.AspNetCore.Hosting.Internal`
- `N:Microsoft.AspNetCore.Http.Internal`
- `N:Microsoft.AspNetCore.Mvc.Core.Infrastructure`
- `N:Microsoft.AspNetCore.Mvc.Core.Internal`
- `N:Microsoft.AspNetCore.Mvc.Cors.Internal`
- `N:Microsoft.AspNetCore.Mvc.DataAnnotations.Internal`
- `N:Microsoft.AspNetCore.Mvc.Formatters.Internal`
- `N:Microsoft.AspNetCore.Mvc.Formatters.Json.Internal`
- `N:Microsoft.AspNetCore.Mvc.Formatters.Xml.Internal`
- `N:Microsoft.AspNetCore.Mvc.Internal`
- `N:Microsoft.AspNetCore.Mvc.ModelBinding.Internal`
- `N:Microsoft.AspNetCore.Mvc.Razor.Internal`
- `N:Microsoft.AspNetCore.Mvc.RazorPages.Internal`
- `N:Microsoft.AspNetCore.Mvc.TagHelpers.Internal`
- `N:Microsoft.AspNetCore.Mvc.ViewFeatures.Internal`
- `N:Microsoft.AspNetCore.Rewrite.Internal`
- `N:Microsoft.AspNetCore.Routing.Internal`
- `N:Microsoft.AspNetCore.Server.Kestrel.Core.Adapter.Internal`
- `N:Microsoft.AspNetCore.Server.Kestrel.Core.Internal.Http`
- `N:Microsoft.AspNetCore.Server.Kestrel.Core.Internal.Infrastructure`
- `N:Microsoft.AspNetCore.Server.Kestrel.Https.Internal`

-->
