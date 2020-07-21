---
title: リセットセキュリティ関数 (アンマネージ API リファレンス)
description: ResetSecurity 関数は、偽装トークンを現在のスレッドに割り当てます。
ms.date: 11/06/2017
api_name:
- ResetSecurity
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- ResetSecurity
helpviewer_keywords:
- ResetSecurity function [.NET WMI and performance counters]
topic_type:
- Reference
ms.openlocfilehash: ce74494455c6cc7fe382a4ea4ef2ff0c4e98c61b
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79174863"
---
# <a name="resetsecurity-function"></a>ResetSecurity 関数
指定した偽装トークンが現在のスレッドに割り当てられます。
  
[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT ResetSecurity (
   [in] HANDLE token
);
```  

## <a name="parameters"></a>パラメーター

`token`  
[in]現在のスレッドに関連付ける偽装トークン。 この値は `null` の場合もあります。

## <a name="return-value"></a>戻り値

関数が成功した場合、戻り値は`S_OK`(0) になります。

関数が失敗した場合、戻り値は 0 以外のエラー コードです。 拡張エラー情報を取得するには[、GetErrorInfo](geterrorinfo.md)関数を呼び出します。
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** WMINet_Utils.idl  
  
 **.NET Framework のバージョン:** [!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]  
  
## <a name="see-also"></a>関連項目

- [WMI およびパフォーマンス カウンター (アンマネージド API リファレンス)](index.md)
