---
title: クライアントキー関数の確認 (アンマネージ API リファレンス)
description: 検証クライアントキー機能は、クライアントキーに正しいセキュリティを保証します。
ms.date: 11/06/2017
api_name:
- VerifyClientKey
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- VerifyClientKey
helpviewer_keywords:
- VerifyClientKey function [.NET WMI and performance counters]
topic_type:
- Reference
ms.openlocfilehash: ebb794240494deb0c831b50e95461ec52017a215
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79176709"
---
# <a name="verifyclientkey-function"></a>クライアントキー機能を確認します。
クライアント キーに適切なセキュリティが確実に含められます。  
  
[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]
  
## <a name="syntax"></a>構文  
  
```cpp  
LONG VerifyClientKey();
```  

## <a name="return-value"></a>戻り値

関数が成功した場合、戻り値は`ERROR_SUCCESS`(0) になります。

関数が失敗した場合、戻り値は*WinError.h*で定義された 0 以外のエラー コードです。

## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** WMINet_Utilsデフ  
  
 **.NET Framework のバージョン:** [!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]  
  
## <a name="see-also"></a>関連項目

- [WMI およびパフォーマンス カウンター (アンマネージド API リファレンス)](index.md)
