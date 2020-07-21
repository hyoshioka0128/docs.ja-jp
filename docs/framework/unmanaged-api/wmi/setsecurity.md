---
title: セットセキュリティ関数 (アンマネージ API リファレンス)
description: SetSecurity 関数は、現在のスレッドの偽装トークンを取得します。
ms.date: 11/06/2017
api_name:
- SetSecurity
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- SetSecurity
helpviewer_keywords:
- SetSecurity function [.NET WMI and performance counters]
topic_type:
- Reference
ms.openlocfilehash: 809f6a95fdd6854b3a591b496877838c48d52199
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79176735"
---
# <a name="setsecurity-function"></a>SetSecurity 関数

現在のスレッドに関連付けられている偽装トークンが取得されます。

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]

## <a name="syntax"></a>構文

```cpp
HRESULT SetSecurity (
   [out] boolean* pNeedToReset,
   [out] HANDLE* pCurrentThreadToken
);
```

## <a name="parameters"></a>パラメーター

`pNeedToReset`\
[アウト]関数が返されるときに[、ResetSecurity](resetsecurity.md)関数を`boolean`呼び出してトークンをリセットするかどうかを示すポインターを格納します。

`token`\
[アウト]関数が戻るときに、現在のスレッドに関連付けられている偽装トークンのハンドルへのポインターを格納します。 この値は、`null`現在のスレッドに関連付けられたトークンがない場合に使用できます。

## <a name="return-value"></a>戻り値

関数が成功した場合、戻り値は`S_OK`(0) になります。

関数が失敗した場合、戻り値は 0 以外のエラー コードです。 拡張エラー情報を取得するには[、GetErrorInfo](geterrorinfo.md)関数を呼び出します。

## <a name="requirements"></a>必要条件

 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。

 **ヘッダー:** WMINet_Utils.idl

 **.NET Framework のバージョン:** [!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]

## <a name="see-also"></a>関連項目

- [WMI およびパフォーマンス カウンター (アンマネージド API リファレンス)](index.md)
