---
title: スレッドの構成設定
description: .NET Core アプリのスレッドを構成するランタイム設定について説明します。
ms.date: 11/27/2019
ms.topic: reference
ms.openlocfilehash: 6a920dbc301830e3f4c95bf637ff3de6d4f464ff
ms.sourcegitcommit: 32a575bf4adccc901f00e264f92b759ced633379
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/04/2019
ms.locfileid: "74998829"
---
# <a name="run-time-configuration-options-for-threading"></a>スレッドのランタイム構成オプション

## <a name="cpu-groups"></a>CPU グループ

- CPU グループ全体にスレッドを自動的に配布するかどうかを構成します。
- 既定:無効 (`0`)。

| | 設定の名前 | 値 |
| - | - | - |
| **runtimeconfig.json** | N/A | N/A |
| **環境変数** | `COMPlus_Thread_UseAllCpuGroups` | `0` - 無効<br/>`1` - 有効 |

## <a name="minimum-threads"></a>最小スレッド数

- ワーカー スレッドプールの最小スレッド数を指定します。
- <xref:System.Threading.ThreadPool.SetMinThreads%2A?displayProperty=nameWithType> メソッドに対応します。

| | 設定の名前 | 値 |
| - | - | - |
| **runtimeconfig.json** | `System.Threading.ThreadPool.MinThreads` | 最小スレッド数を表す整数 |
| **環境変数** | N/A | N/A |

## <a name="maximum-threads"></a>最大スレッド数

- ワーカー スレッドプールの最大スレッド数を指定します。
- <xref:System.Threading.ThreadPool.SetMaxThreads%2A?displayProperty=nameWithType> メソッドに対応します。

| | 設定の名前 | 値 |
| - | - | - |
| **runtimeconfig.json** | `System.Threading.ThreadPool.MaxThreads` | 最大スレッド数を表す整数 |
| **環境変数** | N/A | N/A |
