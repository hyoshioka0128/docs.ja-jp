---
ms.openlocfilehash: d7a93cb539baee6a70f75d3afe52fd7546ac2399
ms.sourcegitcommit: 1cb64b53eb1f253e6a3f53ca9510ef0be1fd06fe
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/29/2020
ms.locfileid: "82507089"
---
### <a name="extensions-package-reference-changes-affecting-some-nuget-packages"></a>拡張機能:一部の NuGet パッケージに影響するパッケージ参照の変更

[aspnet/Announcements#411](https://github.com/aspnet/Announcements/issues/411) に説明があるように、[dotnet/extensions](https://github.com/dotnet/extensions) リポジトリから [dotnet/runtime](https://github.com/dotnet/runtime) に一部の `Microsoft.Extensions.*` NuGet パッケージを移行するとき、移行されたパッケージの一部にパッケージングの変更が適用されます。 この問題に関するディスカッションについては、[dotnet/aspnetcore#21033](https://github.com/dotnet/aspnetcore/issues/21033) を参照してください。

#### <a name="version-introduced"></a>導入されたバージョン

5.0 Preview 4

#### <a name="old-behavior"></a>以前の動作

一部の `Microsoft.Extensions.*` パッケージには、アプリが依存していた API のパッケージ参照が含まれていました。

#### <a name="new-behavior"></a>新しい動作

アプリによっては、`Microsoft.Extensions.*` パッケージ依存関係を追加する必要があります。

#### <a name="reason-for-change"></a>変更理由

*dotnet/runtime* リポジトリと足並みをそろえるよう、パッケージング ポリシーが更新されました。 新しいポリシーの下では、パッケージング中、未使用のパッケージ参照が *.nupkg* ファイルから削除されます。

#### <a name="recommended-action"></a>推奨アクション

影響を受けるパッケージを利用しているとき、削除したパッケージ依存関係からの API が使用されている場合、自分のプロジェクトで、削除したパッケージ依存関係に直接的な依存関係を追加してください。 影響を受けるパッケージとそれが該当する変更をまとめたものが次の表です。

|パッケージ名|変更の説明|
|------------|------------------|
|[Microsoft.Extensions.Configuration.Binder](https://nuget.org/packages/Microsoft.Extensions.Configuration.Binder)|`Microsoft.Extensions.Configuration` の参照を削除しました|
|[Microsoft.Extensions.Configuration.Json](https://nuget.org/packages/Microsoft.Extensions.Configuration.Json)    |`System.Threading.Tasks.Extensions` の参照を削除しました|
|[Microsoft.Extensions.Hosting.Abstractions](https://nuget.org/packages/Microsoft.Extensions.Hosting.Abstractions)|`Microsoft.Extensions.Logging.Abstractions` の参照を削除しました|
|[Microsoft.Extensions.Logging](https://nuget.org/packages/Microsoft.Extensions.Logging)                          |`Microsoft.Extensions.Configuration.Binder` の参照を削除しました|
|[Microsoft.Extensions.Logging.Console](https://nuget.org/packages/Microsoft.Extensions.Logging.Console)          |`Microsoft.Extensions.Configuration.Abstractions` の参照を削除しました|
|[Microsoft.Extensions.Logging.EventLog](https://nuget.org/packages/Microsoft.Extensions.Logging.EventLog)        |.NET Framework 4.6.1 ターゲット フレームワーク モニカーの `System.Diagnostics.EventLog` の参照を削除しました|
|[Microsoft.Extensions.Logging.EventSource](https://nuget.org/packages/Microsoft.Extensions.Logging.EventSource)  |`System.Threading.Tasks.Extensions` の参照を削除しました|
|[Microsoft.Extensions.Options](https://nuget.org/packages/Microsoft.Extensions.Options)                          |`System.ComponentModel.Annotations` の参照を削除しました|

たとえば、`Microsoft.Extensions.Configuration` のパッケージ参照が `Microsoft.Extensions.Configuration.Binder` から削除されました。 依存関係からの API はパッケージで使用されていません。 `Microsoft.Extensions.Configuration` からの API に依存する `Microsoft.Extensions.Configuration.Binder` のユーザーは、自分のプロジェクトで、その直接的な参照を追加してください。

#### <a name="category"></a>カテゴリ

ASP.NET Core

#### <a name="affected-apis"></a>影響を受ける API

None

<!--

#### Affected APIs

Not detectable via API analysis

-->
