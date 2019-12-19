---
title: グローバリゼーションの構成設定
description: .NET Core アプリのグローバリゼーションの側面 (たとえば、日本語の日付の解析方法など) を構成するランタイム設定について説明します。
ms.date: 11/27/2019
ms.topic: reference
ms.openlocfilehash: 0571c64eff5b38aafa37026fb2ba7f4aef778beb
ms.sourcegitcommit: 32a575bf4adccc901f00e264f92b759ced633379
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/04/2019
ms.locfileid: "74998841"
---
# <a name="run-time-configuration-options-for-globalization"></a>グローバリゼーションのランタイム構成オプション

## <a name="invariant-mode"></a>インバリアント モード

- .NET Core を、カルチャ固有のデータや動作にアクセスせずにグローバリゼーション インバリアント モードで実行するか、またはカルチャ データにアクセスできるかどうかを決定します。
- 既定:カルチャ データにアクセスしてアプリを実行します (`false`)。
- 詳細については、「[.NET Core のグローバリゼーション インバリアント モード](https://github.com/dotnet/corefx/blob/master/Documentation/architecture/globalization-invariant-mode.md)」を参照してください。

| | 設定の名前 | 値 |
| - | - | - |
| **runtimeconfig.json** | `System.Globalization.Invariant` | `false` - カルチャ データにアクセスする<br/>`true` - インバリアント モードで実行する |
| **環境変数** | `DOTNET_SYSTEM_GLOBALIZATION_INVARIANT` | `0` - カルチャ データにアクセスする<br/>`1` - インバリアント モードで実行する |

## <a name="era-year-ranges"></a>年号の範囲

- 複数の年号をサポートするカレンダーの範囲チェックを緩和するか、または日付が年号の日付範囲をオーバーフローした場合に <xref:System.ArgumentOutOfRangeException> をスローするかを決定します。
- 既定:範囲チェックを緩和します (`false`)。
- 詳細については、「[カレンダー、時代 (年号)、および日付範囲: 緩やかな範囲のチェック](../../standard/datetime/working-with-calendars.md#calendars-eras-and-date-ranges-relaxed-range-checks)」を参照してください。

| | 設定の名前 | 値 |
| - | - | - |
| **runtimeconfig.json** | `Switch.System.Globalization.EnforceJapaneseEraYearRanges` | `false` - 緩和された範囲チェック<br/>`true` - オーバーフローによって例外が発生する |
| **環境変数** | N/A | N/A |

## <a name="japanese-date-parsing"></a>日本の日付の解析

- 年として "1" または "元年" のいずれかを含む文字列を正しく解析するか、または "1" のみをサポートするかを決定します。
- 既定:"1" または "元年" のいずれかを含む文字列を年として解析します (`false`)。
- 詳細については、「[複数の時代 (年号) のカレンダーで日付を表す](../../standard/datetime/working-with-calendars.md#represent-dates-in-calendars-with-multiple-eras)」を参照してください。

| | 設定の名前 | 値 |
| - | - | - |
| **runtimeconfig.json** | `Switch.System.Globalization.EnforceLegacyJapaneseDateParsing` | `false` - "元年" または "1" をサポートする<br/>`true` - "1" のみをサポートする |
| **環境変数** | N/A | N/A |

## <a name="japanese-year-format"></a>日本の年の形式

- 和暦の元年を "元年" または "1" のどちらで書式設定するかを決定します。
- 既定:元年を "元年" として書式設定します (`false`)。
- 詳細については、「[複数の時代 (年号) のカレンダーで日付を表す](../../standard/datetime/working-with-calendars.md#represent-dates-in-calendars-with-multiple-eras)」を参照してください。

| | 設定の名前 | 値 |
| - | - | - |
| **runtimeconfig.json** | `Switch.System.Globalization.FormatJapaneseFirstYearAsANumber` | `false` - "元年" として書式設定する<br/>`true` - 数字として書式設定する |
| **環境変数** | N/A | N/A |
