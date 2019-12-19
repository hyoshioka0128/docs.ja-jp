---
title: コンパイルの構成設定
description: .NET Core アプリの JIT コンパイラの動作方法を構成するランタイム設定について説明します。
ms.date: 11/27/2019
ms.topic: reference
ms.openlocfilehash: bcc445b6edc48d9432ee614b0b19c9c25621f4a0
ms.sourcegitcommit: 32a575bf4adccc901f00e264f92b759ced633379
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/04/2019
ms.locfileid: "74998877"
---
# <a name="run-time-configuration-options-for-compilation"></a>コンパイルのランタイム構成オプション

## <a name="tiered-compilation"></a>階層型コンパイル

- JIT コンパイラで[階層型コンパイル](../whats-new/dotnet-core-3-0.md#tiered-compilation)を使用するかどうかを構成します。
- .NET Core 3.0 以降、階層型コンパイルは既定で有効に設定されます。
- .NET Core 2.1 および 2.2 では、階層型コンパイルは既定で無効に設定されます。

| | 設定の名前 | 値 |
| - | - | - |
| **runtimeconfig.json** | `System.Runtime.TieredCompilation` | `true` - 有効<br/>`false` - 無効 |
| **環境変数** | `COMPlus_TieredCompilation` | `1` - 有効<br/>`0` - 無効 |
