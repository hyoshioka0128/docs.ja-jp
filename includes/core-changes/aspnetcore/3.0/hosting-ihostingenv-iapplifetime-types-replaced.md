---
ms.openlocfilehash: be1fad236dd3eed047b010e93285aec8bc607b61
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/14/2020
ms.locfileid: "72394337"
---
### <a name="hosting-ihostingenvironment-and-iapplicationlifetime-types-marked-obsolete-and-replaced"></a>ホスティング:IHostingEnvironment と IApplicationLifetime の型が不使用とマークされ、置き換えられました

既存の `IHostingEnvironment` と `IApplicationLifetime` の型を置き換えるために新しい型が導入されました。

#### <a name="version-introduced"></a>導入されたバージョン

3.0

#### <a name="old-behavior"></a>以前の動作

`Microsoft.Extensions.Hosting` および `Microsoft.AspNetCore.Hosting` の 2 つの `IHostingEnvironment` および `IApplicationLifetime` という型がありました。

#### <a name="new-behavior"></a>新しい動作

古い型は不使用とマークされ、新しい型に置き換えられています。

#### <a name="reason-for-change"></a>変更理由

`Microsoft.Extensions.Hosting` が ASP.NET Core 2.1 で導入されたときに、`IHostingEnvironment` や `IApplicationLifetime` などの一部の型が `Microsoft.AspNetCore.Hosting` からコピーされました。 ASP.NET Core 3.0 の一部の変更により、アプリに `Microsoft.Extensions.Hosting` と `Microsoft.AspNetCore.Hosting` の両方の名前空間が含まれるようになります。 これらの重複する型を使用すると、両方の名前空間が参照されるときに "あいまいな参照" コンパイラ エラーが発生します。

#### <a name="recommended-action"></a>推奨アクション

次のように、古い型の使用を新しく導入された型に置き換えます。

**古い型 (警告):**

- <xref:Microsoft.Extensions.Hosting.IHostingEnvironment?displayProperty=nameWithType>
- <xref:Microsoft.AspNetCore.Hosting.IHostingEnvironment?displayProperty=nameWithType>
- <xref:Microsoft.Extensions.Hosting.IApplicationLifetime?displayProperty=nameWithType>
- <xref:Microsoft.AspNetCore.Hosting.IApplicationLifetime?displayProperty=nameWithType>
- <xref:Microsoft.Extensions.Hosting.EnvironmentName?displayProperty=nameWithType>
- <xref:Microsoft.AspNetCore.Hosting.EnvironmentName?displayProperty=nameWithType>

**新しい型:**

- <xref:Microsoft.Extensions.Hosting.IHostEnvironment?displayProperty=nameWithType>
- `Microsoft.AspNetCore.Hosting.IWebHostEnvironment : IHostEnvironment`
- <xref:Microsoft.Extensions.Hosting.IHostApplicationLifetime?displayProperty=nameWithType>
- <xref:Microsoft.Extensions.Hosting.Environments?displayProperty=nameWithType>

新しい `IHostEnvironment`、`IsDevelopment` および `IsProduction` 拡張メソッドは、`Microsoft.Extensions.Hosting` 名前空間にあります。 その名前空間は、プロジェクトに追加する必要がある場合があります。

#### <a name="category"></a>カテゴリ

ASP.NET Core

#### <a name="affected-apis"></a>影響を受ける API

- <xref:Microsoft.AspNetCore.Hosting.EnvironmentName?displayProperty=nameWithType>
- <xref:Microsoft.AspNetCore.Hosting.IApplicationLifetime?displayProperty=nameWithType>
- <xref:Microsoft.AspNetCore.Hosting.IHostingEnvironment?displayProperty=nameWithType>
- <xref:Microsoft.Extensions.Hosting.EnvironmentName?displayProperty=nameWithType>
- <xref:Microsoft.Extensions.Hosting.IApplicationLifetime?displayProperty=nameWithType>
- <xref:Microsoft.Extensions.Hosting.IHostingEnvironment?displayProperty=nameWithType>

<!-- 

#### Affected APIs

- `T:Microsoft.AspNetCore.Hosting.EnvironmentName`
- `T:Microsoft.AspNetCore.Hosting.IApplicationLifetime`
- `T:Microsoft.AspNetCore.Hosting.IHostingEnvironment`
- `T:Microsoft.Extensions.Hosting.EnvironmentName`
- `T:Microsoft.Extensions.Hosting.IApplicationLifetime`
- `T:Microsoft.Extensions.Hosting.IHostingEnvironment`

-->
