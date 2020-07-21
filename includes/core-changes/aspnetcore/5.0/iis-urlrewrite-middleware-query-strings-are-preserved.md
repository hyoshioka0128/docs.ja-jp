---
ms.openlocfilehash: 29908ed916690e67db3cc5d72ebe1b1c6aea45c6
ms.sourcegitcommit: dc2feef0794cf41dbac1451a13b8183258566c0e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/24/2020
ms.locfileid: "85325201"
---
### <a name="iis-urlrewrite-middleware-query-strings-are-preserved"></a>IIS:UrlRewrite ミドルウェア クエリ文字列は保持されます

IIS UrlRewrite ミドルウェアの不具合により、クエリ文字列は書き換えルールに保持されませんでした。 IIS UrlRewrite モジュールの動作との一貫性を維持するため、この不具合が修正されました。

ディスカッションについては、イシュー [dotnet/aspnetcore#22972](https://github.com/dotnet/aspnetcore/issues/22972) を参照してください。

#### <a name="version-introduced"></a>導入されたバージョン

ASP.NET Core 5.0 Preview 7

#### <a name="old-behavior"></a>以前の動作

次の書き換えルールについて考えてみましょう。

```xml
<rule name="MyRule" stopProcessing="true">
  <match url="^about" />
  <action type="Redirect" url="/contact" redirectType="Temporary" appendQueryString="true" />
</rule>
```

上記のルールでは、クエリ文字列は追加されません。 `/about?id=1` のような URI は、`/contact?id=1` ではなく、`/contact` にリダイレクトされます。 `appendQueryString` 属性は既定で `true` にもなります。

#### <a name="new-behavior"></a>新しい動作

クエリ文字列は保持されます。 [以前の動作](#old-behavior)の例からの URI は `/contact?id=1` になります。

#### <a name="reason-for-change"></a>変更理由

以前の動作は、IIS UrlRewrite モジュールの動作と一致しませんでした。 ミドルウェアとモジュールの間で移植をサポートするため、目標は一貫性のある動作を維持することになります。

#### <a name="recommended-action"></a>推奨アクション

クエリ文字列を削除する動作を優先する場合、`action` 要素を `appendQueryString="false"` に設定します。

#### <a name="category"></a>カテゴリ

ASP.NET Core

#### <a name="affected-apis"></a>影響を受ける API

<xref:Microsoft.AspNetCore.Rewrite.IISUrlRewriteOptionsExtensions.AddIISUrlRewrite%2A?displayProperty=nameWithType>

<!--

#### Affected APIs

`Overload:Microsoft.AspNetCore.Rewrite.IISUrlRewriteOptionsExtensions.AddIISUrlRewrite`

-->
