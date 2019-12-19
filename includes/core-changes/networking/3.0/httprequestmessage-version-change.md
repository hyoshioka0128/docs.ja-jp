---
ms.openlocfilehash: ff156afb3da4b921517fd841c5de2295265a8d7b
ms.sourcegitcommit: 79a2d6a07ba4ed08979819666a0ee6927bbf1b01
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74567748"
---
### <a name="default-value-of-httprequestmessageversion-changed-to-11"></a>HttpRequestMessage.Version の既定値が 1.1 に変更された

<xref:System.Net.Http.HttpRequestMessage.Version?displayProperty=fullName> プロパティの既定値が 2.0 から 1.1 に変更されました。

#### <a name="version-introduced"></a>導入されたバージョン

.NET Core 3.0

#### <a name="change-description"></a>変更の説明

.NET Core 1.0 から 2.0 では、<xref:System.Net.Http.HttpRequestMessage.Version?displayProperty=fullName> プロパティの既定値は 1.1 です。 .NET Core 2.1 以降では、2.1 に変更されました。

.NET Core 3.0 以降では、<xref:System.Net.Http.HttpRequestMessage.Version?displayProperty=fullName> プロパティによって返される既定のバージョン番号は再び 1.1 になりました。

#### <a name="recommended-action"></a>推奨される操作

既定値 2.0 を返す <xref:System.Net.Http.HttpRequestMessage.Version?displayProperty=fullName> プロパティに依存している場合は、コードを更新します。

#### <a name="category"></a>カテゴリ

ネットワーキング

#### <a name="affected-apis"></a>影響を受ける API

- <xref:System.Net.Http.HttpRequestMessage.Version?displayProperty=fullName>

<!--
a def
### Affected APIs

- `P:System.Net.Http.HttpRequestMessage.Version`

-- >

