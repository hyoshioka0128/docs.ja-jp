---
title: 関数 (アンマネージ API リファレンス)
description: 関数は、生のパフォーマンス データを指定した形式に変換します。
ms.date: 11/21/2017
api_name:
- FormatFromRawValue
api_location:
- PerfCounter.dll
api_type:
- DLLExport
f1_keywords:
- FormatFromRawValue
helpviewer_keywords:
- FormatFromRawValue function [.NET WMI and performance counters]
topic_type:
- Reference
ms.openlocfilehash: 0a7c0b8387f0c8e2b6e2ade94f7efeede75bd758
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79176839"
---
# <a name="formatfromrawvalue-function"></a>FormatFromRawValue 関数
1 つの生のパフォーマンス データ値が指定した形式に変換されます。この形式変換が時間ベースである場合は、2 つの生のパフォーマンス データ値が変換されます。

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]

## <a name="syntax"></a>構文

```cpp
int FormatFromRawValue (
   [in] uint                    dwCounterType,
   [in] uint                    dwFormat,
   [in] long*                   pTimeBase,
   [in] PDH_RAW_COUNTER*        pRawValue1,
   [in] PDH_RAW_COUNTER*        pRawValue2,
   [out] PDH_FMT_COUNTERVALUE*  pFmtValue
);
```

## <a name="parameters"></a>パラメーター

`dwCounterType`\
[in]カウンターの種類。 カウンターの種類の一覧については、「 [WMI パフォーマンス カウンターの種類](/windows/desktop/WmiSdk/wmi-performance-counter-types)」を参照してください。 `dwCounterType`は、 および 以外の`PERF_LARGE_RAW_FRACTION`任意`PERF_LARGE_RAW_BASE`のカウンター型にすることができます。

`dwFormat`\
[in]生のパフォーマンス データを変換する形式。 次のいずれかの値を指定できます。

|常時  |Value  |説明 |
|---------|---------|---------|
| `PDH_FMT_DOUBLE` |0x00000200 | 計算された値を倍精度浮動小数点値として返します。 |
| `PDH_FMT_LARGE` | 0x00000400 | 計算された値を 64 ビット整数で返します。 |
| `PDH_FMT_LONG` | 0x00000100 | 計算された値を 32 ビットの整数で返します。 |

上記の値の 1 つを、次のいずれかのスケーリング フラグを使用して、ORed にすることができます。

|常時  |Value  |説明 |
|---------|---------|---------|
| `PDH_FMT_NOSCALE` | 0x00001000 | カウンタのスケーリング係数は適用しないでください。 |
| `PDH_FMT_1000` | 0x00002000 | 最終的な値に 1,000 を掛けます。 |

`pTimeBase`\
[in]フォーマット変換に必要な場合は、時間ベースへのポインタ。 フォーマット変換に時間ベース情報が必要ない場合、このパラメーターの値は無視されます。

`pRawValue1`\
[in]生のパフォーマンス値[`PDH_RAW_COUNTER`](/windows/win32/api/pdh/ns-pdh-pdh_raw_counter)を表す構造体へのポインター。

`pRawValue2`\
[in]2 番目の[`PDH_RAW_COUNTER`](/windows/win32/api/pdh/ns-pdh-pdh_raw_counter)生のパフォーマンス値を表す構造体へのポインター。 2 番目の生のパフォーマンス値が必要ない場合、この`null`パラメーターは にする必要があります。

`pFmtValue`\
[アウト]フォーマットされたパフォーマンス値[`PDH_FMT_COUNTERVALUE`](/windows/win32/api/pdh/ns-pdh-pdh_fmt_countervalue)を受け取る構造体へのポインター。

## <a name="return-value"></a>戻り値

この関数では、次の値が返されます。

|常時  |Value  |説明  |
|---------|---------|---------|
| `ERROR_SUCCESS` | 0 | 関数呼び出しが成功しました。 |
| `PDH_INVALID_ARGUMENT` | 0xC0000BBD | 必要な引数がないか、または正しくありません。 |
| `PDH_INVALID_HANDLE` | 0xC0000BBC | ハンドルが有効な PDH オブジェクトではありません。 |

## <a name="remarks"></a>解説

この関数は[、関数の](https://docs.microsoft.com/previous-versions/ms231047(v=vs.85))呼び出しをラップします。

## <a name="requirements"></a>必要条件

 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。

 **ライブラリ:** パーフカウンター.dll

 **.NET Framework のバージョン:** [!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]

## <a name="see-also"></a>関連項目

- [WMI およびパフォーマンス カウンター (アンマネージド API リファレンス)](index.md)
