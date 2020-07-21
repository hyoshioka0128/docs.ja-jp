---
ms.openlocfilehash: 329ef39c7626ecd743577f336a4c8cd4a38fb082
ms.sourcegitcommit: e48a54ebe62e874500a7043f6ee0b77a744d55b4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/26/2020
ms.locfileid: "80291642"
---
### <a name="signalr-usesignalr-and-useconnections-methods-removed"></a>SignalR:UseSignalR メソッドと UseConnections メソッドが削除された

ASP.NET Core 3.0 の SignalR では、エンドポイント ルーティングが採用されました。 その変更の一環として、<xref:Microsoft.AspNetCore.Builder.SignalRAppBuilderExtensions.UseSignalR%2A>、<xref:Microsoft.AspNetCore.Builder.ConnectionsAppBuilderExtensions.UseConnections%2A>、およびいくつかの関連するメソッドが古い機能としてマークされました。 ASP.NET Core 5.0 では、これらの古いメソッドが削除されました。 メソッドの完全な一覧については、「[影響を受ける API](#affected-apis)」をご覧ください。

この問題に関するディスカッションについては、[dotnet/aspnetcore#20082](https://github.com/dotnet/aspnetcore/issues/20082) を参照してください。

#### <a name="version-introduced"></a>導入されたバージョン

5.0 Preview 3

#### <a name="old-behavior"></a>以前の動作

SignalR のハブと接続ハンドラーは、`UseSignalR` または `UseConnections` メソッドを使用して、ミドルウェア パイプラインで登録できました。

#### <a name="new-behavior"></a>新しい動作

SignalR のハブと接続ハンドラーは、<xref:Microsoft.AspNetCore.Routing.IEndpointRouteBuilder> の <xref:Microsoft.AspNetCore.SignalR.HubRouteBuilder.MapHub%2A> および <xref:Microsoft.AspNetCore.Http.Connections.ConnectionsRouteBuilder.MapConnectionHandler%2A> 拡張メソッドを使用して、<xref:Microsoft.AspNetCore.Builder.EndpointRoutingApplicationBuilderExtensions.UseEndpoints%2A> 内で登録する必要があります。

#### <a name="reason-for-change"></a>変更理由

以前のメソッドには、ASP.NET Core の他のルーティング コンポーネントとやり取りしないカスタム ルーティング ロジックがありました。 ASP.NET Core 3.0 では、エンドポイント ルーティングと呼ばれる新しい汎用ルーティング システムが導入されました。 エンドポイント ルーティングにより、SignalR は他のルーティング コンポーネントとやり取りできるようになりました。 このモデルに切り替えることで、ユーザーはエンドポイント ルーティングの利点を最大限に活用できます。 そのため、古いメソッドは削除されています。

#### <a name="recommended-action"></a>推奨アクション

プロジェクトの `Startup.Configure` メソッドから、`UseSignalR` または `UseConnections` を呼び出すコードを削除します。 それを、`UseEndpoints` の呼び出しの本体内で、それぞれ `MapHub` または `MapConnectionHandler` の呼び出しに置き換えます。 次に例を示します。

**古いコード:**

```csharp
app.UseSignalR(routes =>
{
    routes.MapHub<SomeHub>("/path");
});
```

**新しいコード:**

```csharp
app.UseEndpoints(endpoints =>
{
    endpoints.MapHub<SomeHub>("/path");
});
```

一般に、以前の `MapHub` および `MapConnectionHandler` の呼び出しは、ほとんどまたはまったく変更を行わずに、`UseSignalR` および `UseConnections` の本体から `UseEndpoints` に直接移すことができます。

#### <a name="category"></a>カテゴリ

ASP.NET Core

#### <a name="affected-apis"></a>影響を受ける API

- <xref:Microsoft.AspNetCore.Builder.ConnectionsAppBuilderExtensions.UseConnections%2A?displayProperty=nameWithType>
- <xref:Microsoft.AspNetCore.Builder.SignalRAppBuilderExtensions.UseSignalR%2A?displayProperty=nameWithType>
- <xref:Microsoft.AspNetCore.Http.Connections.ConnectionsRouteBuilder.MapConnections%2A?displayProperty=nameWithType>
- <xref:Microsoft.AspNetCore.Http.Connections.ConnectionsRouteBuilder.MapConnectionHandler%2A?displayProperty=nameWithType>
- <xref:Microsoft.AspNetCore.SignalR.HubRouteBuilder.MapHub%2A?displayProperty=nameWithType>

<!--

#### Affected APIs

- `Overload:Microsoft.AspNetCore.Builder.ConnectionsAppBuilderExtensions.UseConnections`
- `Overload:Microsoft.AspNetCore.Builder.SignalRAppBuilderExtensions.UseSignalR`
- `Overload:Microsoft.AspNetCore.Http.Connections.ConnectionsRouteBuilder.MapConnections`
- `Overload:Microsoft.AspNetCore.Http.Connections.ConnectionsRouteBuilder.MapConnectionHandler`
- `Overload:Microsoft.AspNetCore.SignalR.HubRouteBuilder.MapHub`

-->
