---
ms.openlocfilehash: 9d138f79fcede4acac837f8d7793aa343ced737c
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/14/2020
ms.locfileid: "78290722"
---
### <a name="http-defaulthttpcontext-extensibility-removed"></a>HTTP:DefaultHttpContext の機能拡張の削除

ASP.NET Core 3.0 のパフォーマンスの改善の一環として、`DefaultHttpContext` の機能拡張が削除されました。 クラスは `sealed` になりました。 詳細については、[dotnet/aspnetcore#6504](https://github.com/dotnet/aspnetcore/pull/6504) を参照してください。

単体テストで `Mock<DefaultHttpContext>` を使用する場合は、代わりに `Mock<HttpContext>` または `new DefaultHttpContext()` を使用してください。

ディスカッションについては、[dotnet/aspnetcore#6534](https://github.com/dotnet/aspnetcore/issues/6534) を参照してください。

#### <a name="version-introduced"></a>導入されたバージョン

3.0

#### <a name="old-behavior"></a>以前の動作

クラスは `DefaultHttpContext` から派生できます。

#### <a name="new-behavior"></a>新しい動作

クラスは `DefaultHttpContext` から派生できません。

#### <a name="reason-for-change"></a>変更理由

機能拡張は `HttpContext` のプーリングを可能にするために当初提供されていましたが、不要な複雑さをもたらし、他の最適化の妨げとなっていました。

#### <a name="recommended-action"></a>推奨アクション

単体テストで `Mock<DefaultHttpContext>` を使用する場合、今後は代わりに `Mock<HttpContext>` を使用してください。

#### <a name="category"></a>カテゴリ

ASP.NET Core

#### <a name="affected-apis"></a>影響を受ける API

<xref:Microsoft.AspNetCore.Http.DefaultHttpContext?displayProperty=nameWithType>

<!--

#### Affected APIs

`T:Microsoft.AspNetCore.Http.DefaultHttpContext`

-->
