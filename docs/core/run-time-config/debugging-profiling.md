---
title: デバッグとプロファイルの構成設定
description: .NET Core アプリのデバッグとプロファイルを構成するランタイム設定について説明します。
ms.date: 11/27/2019
ms.topic: reference
ms.openlocfilehash: 5efd0f776da4b7ce6ff7f3bdfda24feec6e00f79
ms.sourcegitcommit: c76c8b2c39ed2f0eee422b61a2ab4c05ca7771fa
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83761994"
---
# <a name="run-time-configuration-options-for-debugging-and-profiling"></a>デバッグとプロファイルのランタイム構成オプション

## <a name="enable-diagnostics"></a>診断を有効化する

- デバッガー、プロファイラー、EventPipe 診断を有効にするか、または無効にするかを構成します。
- この設定を省略すると、診断は有効になります。 これは、値を `1` に設定した場合と同じです。

| | 設定の名前 | 値 |
| - | - | - |
| **runtimeconfig.json** | N/A | N/A |
| **環境変数** | `COMPlus_EnableDiagnostics` | `1` - 有効<br/>`0` - 無効 |

## <a name="enable-profiling"></a>プロファイルを有効にする

- 現在実行中のプロセスに対してプロファイルを有効にするかどうかを構成します。
- この設定を省略すると、プロファイルは無効になります。 これは、値を `0` に設定した場合と同じです。

| | 設定の名前 | 値 |
| - | - | - |
| **runtimeconfig.json** | N/A | N/A |
| **環境変数** | `CORECLR_ENABLE_PROFILING` | `0` - 無効<br/>`1` - 有効 |

## <a name="profiler-guid"></a>プロファイラー GUID

- 現在実行中のプロセスに読み込むプロファイラーの GUID を指定します。

| | 設定の名前 | 値 |
| - | - | - |
| **runtimeconfig.json** | N/A | N/A |
| **環境変数** | `CORECLR_PROFILER` | *string-guid* |

## <a name="profiler-location"></a>プロファイラーの場所

- 現在実行中のプロセス (32 ビット プロセスまたは 64 ビット プロセス) に読み込むプロファイラー DLL へのパスを指定します。
- 複数の変数が設定されている場合、ビット固有の変数が優先されます。 これらは、ロードするプロファイラーのビットを指定します。
- 詳細については、「[プロファイラー ライブラリを検索する](https://github.com/dotnet/runtime/blob/master/docs/design/coreclr/profiling/Profiler%20Loading.md)」を参照してください。

| | 設定の名前 | 値 |
| - | - | - |
| **環境変数** | `CORECLR_PROFILER_PATH` | *string-path* |
| **環境変数** | `CORECLR_PROFILER_PATH_32` | *string-path* |
| **環境変数** | `CORECLR_PROFILER_PATH_64` | *string-path* |

## <a name="write-perf-map"></a>パフォーマンス マップの作成

- Linux システムでの */tmp/perf-$pid.map* の作成を有効または無効にします。
- この設定を省略すると、パフォーマンス マップの作成は無効になります。 これは、値を `0` に設定した場合と同じです。

| | 設定の名前 | 値 |
| - | - | - |
| **runtimeconfig.json** | N/A | N/A |
| **環境変数** | `COMPlus_PerfMapEnabled` | `0` - 無効<br/>`1` - 有効 |

## <a name="perf-log-markers"></a>パフォーマンス ログのマーカー

- 指定したシグナルのパフォーマンス ログでのマーカーとしての受け入れおよび無視を有効または無効にします。
- この設定を省略すると、指定したシグナルは無視されません。 これは、値を `0` に設定した場合と同じです。

| | 設定の名前 | 値 |
| - | - | - |
| **runtimeconfig.json** | N/A | N/A |
| **環境変数** | `COMPlus_PerfMapIgnoreSignal` | `0` - 無効<br/>`1` - 有効 |

> [!NOTE]
> この設定は、[COMPlus_PerfMapEnabled](#write-perf-map) が省略されるか、または `0` (無効) に設定されている場合は、無視されます。
