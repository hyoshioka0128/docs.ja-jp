---
ms.openlocfilehash: 6deeb7debce9b731f3871b7de0ad8df8a8cdafea
ms.sourcegitcommit: 7370aa8203b6036cea1520021b5511d0fd994574
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/02/2020
ms.locfileid: "82728287"
---
### <a name="localization-resourcemanagerwithculturestringlocalizer-class-and-withculture-interface-member-removed"></a>ローカリゼーション:ResourceManagerWithCultureStringLocalizer クラスと WithCulture インターフェイス メンバーを削除

.NET 5.0 Preview 1 で [ResourceManagerWithCultureStringLocalizer](/dotnet/api/microsoft.extensions.localization.resourcemanagerwithculturestringlocalizer?view=dotnet-plat-ext-3.1) クラスと [WithCulture](/dotnet/api/microsoft.extensions.localization.resourcemanagerstringlocalizer.withculture?view=dotnet-plat-ext-3.1) メソッドが削除されました。

コンテキストについては、[aspnet/Announcements#346](https://github.com/aspnet/Announcements/issues/346) と [dotnet/aspnetcore#3324](https://github.com/dotnet/aspnetcore/issues/3324) を参照してください。 この変更のディスカッションについては、[dotnet/aspnetcore#7756](https://github.com/dotnet/aspnetcore/issues/7756) を参照してください。

#### <a name="version-introduced"></a>導入されたバージョン

5.0 Preview 1

#### <a name="old-behavior"></a>以前の動作

`ResourceManagerWithCultureStringLocalizer` クラスと `ResourceManagerStringLocalizer.WithCulture` メソッドは、[.NET Core 3.0 Preview 3 以降、古い形式となりました](/dotnet/core/compatibility/2.2-3.0#localization-resourcemanagerwithculturestringlocalizer-and-withculture-marked-obsolete)。

#### <a name="new-behavior"></a>新しい動作

`ResourceManagerWithCultureStringLocalizer` クラスと `ResourceManagerStringLocalizer.WithCulture` メソッドは、.NET 5.0 Preview 1 で削除されています。 加えられた変更のインベントリについては、[dotnet/extensions#2562](https://github.com/dotnet/extensions/pull/2562/files) の pull request を参照してください。

#### <a name="reason-for-change"></a>変更理由

[ResourceManagerWithCultureStringLocalizer](/dotnet/api/microsoft.extensions.localization.resourcemanagerwithculturestringlocalizer?view=dotnet-plat-ext-3.1) クラスと [ResourceManagerStringLocalizer](/dotnet/api/microsoft.extensions.localization.resourcemanagerstringlocalizer.withculture?view=dotnet-plat-ext-3.1) メソッドは、ローカライズでユーザーの混乱の原因になることがよくありました。 カスタムの <xref:Microsoft.Extensions.Localization.IStringLocalizer> 実装を作成する際は、混乱に拍車がかかっていました。 このクラスとメソッドを使用すると、`IStringLocalizer` インスタンスが "言語ごとで、リソースごと" であるような印象をコンシューマーに与えるのです。 実際には、インスタンスは "リソースごと" のみである必要があります。 実行時に、<xref:System.Globalization.CultureInfo.CurrentUICulture%2A?displayProperty=nameWithType> プロパティによって、使用言語が決定されます。

#### <a name="recommended-action"></a>推奨アクション

`ResourceManagerWithCultureStringLocalizer` クラスと `ResourceManagerStringLocalizer.WithCulture` メソッドの使用をやめます。

#### <a name="category"></a>カテゴリ

ASP.NET Core

#### <a name="affected-apis"></a>影響を受ける API

- [ResourceManagerWithCultureStringLocalizer](/dotnet/api/microsoft.extensions.localization.resourcemanagerwithculturestringlocalizer?view=dotnet-plat-ext-3.1)
- [ResourceManagerStringLocalizer.WithCulture](/dotnet/api/microsoft.extensions.localization.resourcemanagerstringlocalizer.withculture?view=dotnet-plat-ext-3.1)

<!--

#### Affected APIs

- `T:Microsoft.Extensions.Localization.ResourceManagerWithCultureStringLocalizer`
- `Overload:Microsoft.Extensions.Localization.ResourceManagerStringLocalizer.WithCulture`

-->
