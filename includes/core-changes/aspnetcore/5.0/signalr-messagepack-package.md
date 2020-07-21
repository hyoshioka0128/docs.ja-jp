---
ms.openlocfilehash: ca0792a3fd05d28cecceac1d644e3e4bf64722bc
ms.sourcegitcommit: 59e36e65ac81cdd094a5a84617625b2a0ff3506e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/27/2020
ms.locfileid: "80345217"
---
### <a name="signalr-messagepack-hub-protocol-moved-to-messagepack-2x-package"></a>SignalR:MessagePack ハブ プロトコルが MessagePack 2.x パッケージに移動された

ASP.NET Core SignalR [MessagePack ハブ プロトコル](/aspnet/core/signalr/messagepackhubprotocol)では、MessagePack のシリアル化に [MessagePack NuGet パッケージ](https://www.nuget.org/packages/MessagePack)が使用されています。 ASP.NET Core 5.0 では、パッケージが 1.x から最新の 2.x パッケージ バージョンにアップグレードされます。

この問題に関するディスカッションについては、[dotnet/aspnetcore#18692](https://github.com/dotnet/aspnetcore/issues/18692) を参照してください。

#### <a name="version-introduced"></a>導入されたバージョン

5.0 Preview 1

#### <a name="old-behavior"></a>以前の動作

ASP.NET Core SignalR では、MessagePack 1.x パッケージを使用して、MessagePack メッセージのシリアル化と逆シリアル化が行われていました。

#### <a name="new-behavior"></a>新しい動作

ASP.NET Core SignalR では、MessagePack 2.x パッケージを使用して、MessagePack メッセージのシリアル化と逆シリアル化が行われます。

#### <a name="reason-for-change"></a>変更理由

MessagePack 2.x パッケージの最新の機能強化により、便利な機能が追加されています。

#### <a name="recommended-action"></a>推奨アクション

この破壊的変更は、次の場合に適用されます。

* <xref:Microsoft.AspNetCore.SignalR.MessagePackHubProtocolOptions> での値の設定または構成。
* MessagePack API の直接的な使用、および同じプロジェクトでの ASP.NET Core SignalR MessagePack ハブ プロトコルの使用。 以前のバージョンの代わりに、新しいバージョンが読み込まれます。

パッケージ作成者からの移行ガイダンスについては、「[MessagePack v1 から MessagePack v2.x への移行](https://github.com/neuecc/MessagePack-CSharp/blob/master/doc/migration.md)」を参照してください。 メッセージのシリアル化と逆シリアル化のいくつかの側面が影響を受けます。 具体的には、[DateTime 値をシリアル化する方法の動作が変わります](https://github.com/neuecc/MessagePack-CSharp/blob/master/doc/migration.md#behavioral-changes)。

#### <a name="category"></a>カテゴリ

ASP.NET Core

#### <a name="affected-apis"></a>影響を受ける API

<xref:Microsoft.AspNetCore.SignalR.MessagePackHubProtocolOptions?displayProperty=nameWithType>

<!--

#### Affected APIs

`T:Microsoft.AspNetCore.SignalR.MessagePackHubProtocolOptions`

-->
