---
ms.openlocfilehash: b893966ceb65246ed6a7d214011b17ca14c50d5a
ms.sourcegitcommit: c23d9666ec75b91741da43ee3d91c317d68c7327
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85802853"
---

> [!WARNING]
> <xref:System.Text.RegularExpressions> を使用して信頼できない入力を処理するときは、タイムアウトを渡します。 悪意のあるユーザーが `RegularExpressions` に入力を提供して、[サービス拒否攻撃](https://www.us-cert.gov/ncas/tips/ST04-015)を行う可能性があります。 `RegularExpressions` を使用する ASP.NET Core フレームワーク API は、タイムアウトを渡します。
