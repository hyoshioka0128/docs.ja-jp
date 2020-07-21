---
title: グローバリゼーションの構成設定
description: .NET Core アプリのグローバリゼーションの側面 (たとえば、日本語の日付の解析方法など) を構成するランタイム設定について説明します。
ms.date: 05/18/2020
ms.topic: reference
ms.openlocfilehash: 56228e9a6cb6dbab6a22bdc00d11212e1019776b
ms.sourcegitcommit: c76c8b2c39ed2f0eee422b61a2ab4c05ca7771fa
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83761968"
---
# <a name="run-time-configuration-options-for-globalization"></a>グローバリゼーションのランタイム構成オプション

## <a name="invariant-mode"></a>インバリアント モード

- .NET Core を、カルチャ固有のデータや動作にアクセスせずにグローバリゼーション インバリアント モードで実行するかどうかを決定します。
- この設定を省略した場合、アプリはカルチャ データにアクセスできる状態で実行されます。 これは、値を `false` に設定した場合と同じです。
- 詳細については、「[.NET Core のグローバリゼーション インバリアント モード](https://github.com/dotnet/runtime/blob/master/docs/design/features/globalization-invariant-mode.md)」を参照してください。

| | 設定の名前 | 値 |
| - | - | - |
| **runtimeconfig.json** | `System.Globalization.Invariant` | `false` - カルチャ データにアクセスする<br/>`true` - インバリアント モードで実行する |
| **MSBuild のプロパティ** | `InvariantGlobalization` | `false` - カルチャ データにアクセスする<br/>`true` - インバリアント モードで実行する |
| **環境変数** | `DOTNET_SYSTEM_GLOBALIZATION_INVARIANT` | `0` - カルチャ データにアクセスする<br/>`1` - インバリアント モードで実行する |

### <a name="examples"></a>使用例

*runtimeconfig.json* ファイル:

```json
{
   "runtimeOptions": {
      "configProperties": {
         "System.Globalization.Invariant": true
      }
   }
}
```

プロジェクト ファイル:

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <InvariantGlobalization>true</InvariantGlobalization>
  </PropertyGroup>

</Project>
```

## <a name="era-year-ranges"></a>年号の範囲

- 複数の年号をサポートするカレンダーの範囲チェックを緩和するか、または日付が年号の日付範囲をオーバーフローした場合に <xref:System.ArgumentOutOfRangeException> をスローするかを決定します。
- この設定を省略した場合、範囲チェックは緩和されます。 これは、値を `false` に設定した場合と同じです。
- 詳細については、「[カレンダー、時代 (年号)、および日付範囲: 緩やかな範囲のチェック](../../standard/datetime/working-with-calendars.md#calendars-eras-and-date-ranges-relaxed-range-checks)」を参照してください。

| | 設定の名前 | 値 |
| - | - | - |
| **runtimeconfig.json** | `Switch.System.Globalization.EnforceJapaneseEraYearRanges` | `false` - 緩和された範囲チェック<br/>`true` - オーバーフローによって例外が発生する |
| **環境変数** | N/A | N/A |

## <a name="japanese-date-parsing"></a>日本の日付の解析

- 年として "1" または "元年" のいずれかを含む文字列を正しく解析するか、または "1" のみをサポートするかを決定します。
- この設定を省略した場合、年として "1" または "元年" が含まれる文字列は、正常に解析されます。 これは、値を `false` に設定した場合と同じです。
- 詳細については、「[複数の時代 (年号) のカレンダーで日付を表す](../../standard/datetime/working-with-calendars.md#represent-dates-in-calendars-with-multiple-eras)」を参照してください。

| | 設定の名前 | 値 |
| - | - | - |
| **runtimeconfig.json** | `Switch.System.Globalization.EnforceLegacyJapaneseDateParsing` | `false` - "元年" または "1" をサポートする<br/>`true` - "1" のみをサポートする |
| **環境変数** | N/A | N/A |

## <a name="japanese-year-format"></a>日本の年の形式

- 和暦の元年を "元年" または "1" のどちらで書式設定するかを決定します。
- この設定を省略した場合、最初の年は "元年" として書式設定されます。 これは、値を `false` に設定した場合と同じです。
- 詳細については、「[複数の時代 (年号) のカレンダーで日付を表す](../../standard/datetime/working-with-calendars.md#represent-dates-in-calendars-with-multiple-eras)」を参照してください。

| | 設定の名前 | 値 |
| - | - | - |
| **runtimeconfig.json** | `Switch.System.Globalization.FormatJapaneseFirstYearAsANumber` | `false` - "元年" として書式設定する<br/>`true` - 数字として書式設定する |
| **環境変数** | N/A | N/A |

## <a name="nls"></a>NLS

- .NET で Windows アプリ用に各国語サポート (NLS) または International Components for Unicode (ICU) のグローバリゼーション API が使用されるかどうかを決定します。 .NET 5.0 以降のバージョンの場合、Windows 10 May 2019 Update 以降のバージョンでは ICU グローバリゼーション API が既定で使用されます。
- この設定を省略した場合、.NET では ICU グローバリゼーション API が既定で使用されます。 これは、値を `false` に設定した場合と同じです。
- 詳細については、「[グローバリゼーション API では Windows 上の ICU ライブラリが使用される](../compatibility/3.1-5.0.md#globalization-apis-use-icu-libraries-on-windows)」を参照してください。

| | 設定の名前 | 値 | 導入時期 |
| - | - | - | - |
| **runtimeconfig.json** | `System.Globalization.UseNls` | `false` - ICU グローバリゼーション API を使用します<br/>`true` - NLS グローバリゼーション API を使用します | .NET 5.0 |
| **環境変数** | `DOTNET_SYSTEM_GLOBALIZATION_USENLS` | `false` - ICU グローバリゼーション API を使用します<br/>`true` - NLS グローバリゼーション API を使用します | .NET 5.0 |
