---
ms.openlocfilehash: 8e077d5cde6e824af5aac3742308593f1d91dd92
ms.sourcegitcommit: a9b8945630426a575ab0a332e568edc807666d1b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/30/2020
ms.locfileid: "80391183"
---
### <a name="static-files-csv-content-type-changed-to-standards-compliant"></a>静的ファイル: CSV コンテンツ タイプが標準準拠に変更されました

ASP.NET Core 5.0 では、[静的ファイル ミドルウェア](/aspnet/core/fundamentals/static-files) によって *.csv* ファイルに使用される既定の `Content-Type` 応答ヘッダー値が、標準に準拠した値 `text/csv` に変更されました。

この問題に関するディスカッションについては、[dotnet/aspnetcore#17385](https://github.com/dotnet/AspNetCore/issues/17385) を参照してください。

#### <a name="version-introduced"></a>導入されたバージョン

5.0 Preview 1

#### <a name="old-behavior"></a>以前の動作

`Content-Type` ヘッダー値 `application/octet-stream` が使用されていました。

#### <a name="new-behavior"></a>新しい動作

`Content-Type` ヘッダー値 `text/csv` が使用されます。

#### <a name="reason-for-change"></a>変更理由

[RFC 7111](https://tools.ietf.org/html/rfc7111#section-5.1) 標準に準拠しています。

#### <a name="recommended-action"></a>推奨アクション

この変更によってアプリが影響を受ける場合は、ファイル拡張子と MIME の種類のマッピングをカスタマイズできます。 MIME の種類 `application/octet-stream` に戻すには、`Startup.Configure` でメソッド呼び出し <xref:Microsoft.AspNetCore.Builder.StaticFileExtensions.UseStaticFiles%2A> を変更します。 次に例を示します。

```csharp
var provider = new FileExtensionContentTypeProvider();
provider.Mappings[".csv"] = MediaTypeNames.Application.Octet;

app.UseStaticFiles(new StaticFileOptions
{
    ContentTypeProvider = provider
});
```

マッピングのカスタマイズの詳細については、「[FileExtensionContentTypeProvider](/aspnet/core/fundamentals/static-files#fileextensioncontenttypeprovider)」を参照してください。

#### <a name="category"></a>カテゴリ

ASP.NET Core

#### <a name="affected-apis"></a>影響を受ける API

<xref:Microsoft.AspNetCore.StaticFiles.FileExtensionContentTypeProvider?displayProperty=nameWithType>

<!--

#### Affected APIs

`T:Microsoft.AspNetCore.StaticFiles.FileExtensionContentTypeProvider`

-->
