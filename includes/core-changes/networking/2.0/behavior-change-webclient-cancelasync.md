---
ms.openlocfilehash: 80d4bbbfe52ab9685d7ca54f21b80d4b1773da22
ms.sourcegitcommit: d9c7ac5d06735a01c1fafe34efe9486734841a72
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/06/2020
ms.locfileid: "82859614"
---
### <a name="webclientcancelasync-doesnt-always-cancel-immediately"></a>WebClient.CancelAsync ですぐにキャンセルされない場合がある

.NET Core 2.0 以降、<xref:System.Net.WebClient.CancelAsync?displayProperty=nameWithType> を呼び出したとき、応答がフェッチを開始している場合、要求がすぐにキャンセルされません。

#### <a name="change-description"></a>変更の説明

以前は、<xref:System.Net.WebClient.CancelAsync?displayProperty=nameWithType> を呼び出すと要求がすぐにキャンセルされました。 .NET Core 2.0 以降、<xref:System.Net.WebClient.CancelAsync?displayProperty=nameWithType> を呼び出したとき、応答がフェッチを開始していない場合にのみ、要求がすぐにキャンセルされます。 応答がフェッチを開始している場合、完全な応答が読み取られた後でのみ、要求がキャンセルされます。

この変化の理由は、<xref:System.Net.WebClient> API が非推奨になり、<xref:System.Net.Http.HttpClient> に取って代わられたことにあります。

#### <a name="version-introduced"></a>導入されたバージョン

2.0

#### <a name="recommended-action"></a>推奨アクション

非推奨になっている <xref:System.Net.WebClient?displayProperty=fullName> ではなく、<xref:System.Net.Http.HttpClient?displayProperty=fullName> クラスを使用してください。

#### <a name="category"></a>カテゴリ

ネットワーキング

#### <a name="affected-apis"></a>影響を受ける API

- <xref:System.Net.WebClient.CancelAsync?displayProperty=fullName>

<!--

#### Affected APIs

- `M:System.Net.WebClient.CancelAsync`

-->
