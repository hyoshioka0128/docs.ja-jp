---
title: ネットワークに関する破壊的変更
description: .NET Core のネットワークに関する破壊的変更の一覧を示します。
ms.date: 05/05/2020
ms.openlocfilehash: 07e0b2e062ce244cd6312bbe08bcc63db4c74347
ms.sourcegitcommit: d9c7ac5d06735a01c1fafe34efe9486734841a72
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/06/2020
ms.locfileid: "82859629"
---
# <a name="networking-breaking-changes"></a>ネットワークに関する破壊的変更

このページでは、次の破壊的変更について説明します。

| 互換性に影響する変更点 | 導入されたバージョン |
| - | - |
| [HttpRequestMessage.Version の既定値が 1.1 に変更された](#default-value-of-httprequestmessageversion-changed-to-11) | 3.0 |
| [WebClient.CancelAsync がすぐにキャンセルされない場合がある](#webclientcancelasync-doesnt-always-cancel-immediately) | 2.0 |

## <a name="net-core-30"></a>.NET Core 3.0

[!INCLUDE[Default value of HttpRequestMessage.Version changed to 1.1](~/includes/core-changes/networking/3.0/httprequestmessage-version-change.md)]

***

## <a name="net-core-20"></a>.NET Core 2.0

[!INCLUDE [behavior-change-webclient-cancelasync](../../../includes/core-changes/networking/2.0/behavior-change-webclient-cancelasync.md)]

***
