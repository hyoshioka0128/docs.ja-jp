---
ms.openlocfilehash: 7a05f60cf1c04d3d73dadb54541254a83b4ea855
ms.sourcegitcommit: 1cb64b53eb1f253e6a3f53ca9510ef0be1fd06fe
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/29/2020
ms.locfileid: "82507088"
---
### <a name="signalr-messagepack-hub-protocol-options-type-changed"></a>SignalR:MessagePack ハブ プロトコル オプションの種類を変更

ASP.NET Core SignalR MessagePack ハブ プロトコルのオプションの型が `IList<MessagePack.IFormatterResolver>` から [MessagePack](https://www.nuget.org/packages/MessagePack) ライブラリの `MessagePackSerializerOptions` 型に変更されました。

この変更のディスカッションについては、[dotnet/aspnetcore#20506](https://github.com/dotnet/aspnetcore/issues/20506) を参照してください。

#### <a name="version-introduced"></a>導入されたバージョン

5.0 Preview 4

#### <a name="old-behavior"></a>以前の動作

次の例に示されているようにオプションを増やすことができます。

```csharp
services.AddSignalR()
    .AddMessagePackProtocol(options =>
    {
        options.FormatterResolvers.Add(MessagePack.Resolvers.StandardResolver.Instance);
    });
```

次のようにオプションを置換してください。

```csharp
services.AddSignalR()
    .AddMessagePackProtocol(options =>
    {
        options.FormatterResolvers = new List<MessagePack.IFormatterResolver>()
        {
            MessagePack.Resolvers.StandardResolver.Instance
        };
    });
```

#### <a name="new-behavior"></a>新しい動作

次の例に示されているようにオプションを増やすことができます。

```csharp
services.AddSignalR()
    .AddMessagePackProtocol(options =>
    {
        options.SerializerOptions =
            options.SerializeOptions.WithResolver(MessagePack.Resolvers.StandardResolver.Instance);
    });
```

次のようにオプションを置換してください。

```csharp
services.AddSignalR()
    .AddMessagePackProtocol(options =>
    {
        options.SerializerOptions = MessagePackSerializerOptions
                .Standard
                .WithResolver(MessagePack.Resolvers.StandardResolver.Instance)
                .WithSecurity(MessagePackSecurity.UntrustedData);
    });
```

#### <a name="reason-for-change"></a>変更理由

この変更は [aspnet/Announcements#404](https://github.com/aspnet/Announcements/issues/404) で告知した MessagePack v2.x への以降の一環です。 v2.x ライブラリで追加されたオプション API は使いやすく、以前に公開されていた `MessagePack.IFormatterResolver` のリストより機能が多くなっています。

#### <a name="recommended-action"></a>推奨アクション

この重大な変更は、<xref:Microsoft.AspNetCore.SignalR.MessagePackHubProtocolOptions> で値を構成しているユーザーに影響します。 ASP.NET Core SignalR MessagePack ハブ プロトコルを使用しているとき、このオプションを変更する場合、上の画像のように新しいオプション API を使用するように使用状況を更新します。

#### <a name="category"></a>カテゴリ

ASP.NET Core

#### <a name="affected-apis"></a>影響を受ける API

<xref:Microsoft.AspNetCore.SignalR.MessagePackHubProtocolOptions?displayProperty=nameWithType>

<!--

#### Affected APIs

`T:Microsoft.AspNetCore.SignalR.MessagePackHubProtocolOptions`

-->
