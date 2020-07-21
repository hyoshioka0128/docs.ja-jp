---
title: グローバリゼーションに関する破壊的変更
description: .NET Core におけるグローバリゼーションでの破壊的変更の一覧を示します。
ms.date: 04/07/2020
ms.openlocfilehash: 0c3367cb3515c6f473f53be6062b54f2e836b8c5
ms.sourcegitcommit: 0926684d8d34f4c6b5acce58d2193db093cb9cf2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/20/2020
ms.locfileid: "83702305"
---
# <a name="globalization-breaking-changes"></a>グローバリゼーションに関する破壊的変更

このページでは、次の破壊的変更について説明します。

| 互換性に影響する変更点 | 導入されたバージョン |
| - | :-: |
| [グローバリゼーション API では Windows 上の ICU ライブラリが使用される](#globalization-apis-use-icu-libraries-on-windows) | 5.0 |
| [StringInfo と TextElementEnumerator は現在 UAX29 に準拠する](#stringinfo-and-textelementenumerator-are-now-uax29-compliant) | 5.0 |
| ["C" ロケールをインバリアント ロケールにマップ](#c-locale-maps-to-the-invariant-locale) | 3.0 |

## <a name="net-50"></a>.NET 5.0

[!INCLUDE [icu-globalization-api](../../../includes/core-changes/globalization/5.0/icu-globalization-api.md)]

***

[!INCLUDE [uax29-compliant-grapheme-enumeration](../../../includes/core-changes/globalization/5.0/uax29-compliant-grapheme-enumeration.md)]

***

## <a name="net-core-30"></a>.NET Core 3.0

[!INCLUDE["C" locale maps to the invariant locale](~/includes/core-changes/globalization/3.0/c-locale-maps-to-invariant-locale.md)]

***
