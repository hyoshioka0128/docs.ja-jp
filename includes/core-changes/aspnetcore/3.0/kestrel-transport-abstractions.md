---
ms.openlocfilehash: fb23418816abcae125106c93b339a546aa9bc2ee
ms.sourcegitcommit: 0926684d8d34f4c6b5acce58d2193db093cb9cf2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/20/2020
ms.locfileid: "83721105"
---
### <a name="kestrel-transport-abstractions-removed-and-made-public"></a>Kestrel: トランスポートの抽象化を削除して公開

"pubternal" API からの移行の一環として、Kestrel トランスポート層の API がパブリック インターフェイスとして `Microsoft.AspNetCore.Connections.Abstractions` ライブラリに公開されています。

#### <a name="version-introduced"></a>導入されたバージョン

3.0

#### <a name="old-behavior"></a>以前の動作

- トランスポート関連の抽象化は、`Microsoft.AspNetCore.Server.Kestrel.Transport.Abstractions` ライブラリで提供されていました。
- `ListenOptions.NoDelay` プロパティが使用可能でした。

#### <a name="new-behavior"></a>新しい動作

- `...Transport.Abstractions` ライブラリの最も使用されている機能を公開するために、`Microsoft.AspNetCore.Connections.Abstractions` ライブラリに `IConnectionListener` インターフェイスが導入されました。
- トランスポート オプション (`LibuvTransportOptions` および `SocketTransportOptions`) で、`NoDelay` が使用できるようになりました。
- `SchedulingMode` は使用できなくなりました。

#### <a name="reason-for-change"></a>変更理由

ASP.NET Core 3.0 は、"pubternal" API から移行しました。

#### <a name="recommended-action"></a>推奨アクション

#### <a name="category"></a>カテゴリ

ASP.NET Core

#### <a name="affected-apis"></a>影響を受ける API

None

<!-- 

#### Affected APIs

Not detectable via API analysis

-->
