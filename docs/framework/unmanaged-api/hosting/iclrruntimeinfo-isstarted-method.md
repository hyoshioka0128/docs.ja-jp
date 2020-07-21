---
title: ICLRRuntimeInfo::IsStarted メソッド
ms.date: 03/30/2017
api_name:
- ICLRRuntimeInfo.IsStarted
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRRuntimeInfo::IsStarted
helpviewer_keywords:
- IsStarted method [.NET Framework hosting]
- ICLRRuntimeInfo::IsStarted method [.NET Framework hosting]
ms.assetid: ef6f2662-323b-4534-aa82-6d1afb7b9309
ms.openlocfilehash: 85a7adddf395e07297c8fb6ceab4aa81e0aaf012
ms.sourcegitcommit: c76c8b2c39ed2f0eee422b61a2ab4c05ca7771fa
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83762202"
---
# <a name="iclrruntimeinfoisstarted-method"></a>ICLRRuntimeInfo::IsStarted メソッド
ランタイムが開始されたかどうか (つまり、 [ICLRRuntimeHost:: Start メソッド](iclrruntimehost-start-method.md)が呼び出され、成功したかどうか) を示します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT IsStarted(  
        [out] BOOL     *pbStarted,  
        [out] DWORD    *pdwStartupFlags);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pbStarted`  
 [出力] `true`このランタイムが開始されている場合は。それ以外の場合は `false` 。  
  
 `pdwStartupFlags`  
 入出力ランタイムを開始するために使用されたフラグを返します。  
  
## <a name="return-value"></a>戻り値  
 このメソッドは、次の特定の HRESULT と、メソッドの失敗を示す HRESULT エラーも返します。  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|メソッドは正常に完了しました。|  
|E_NOTIMPL|共通言語ランタイム (CLR) のバージョンは、.NET Framework 4 の CLR バージョンよりも前のバージョンです。|  
  
## <a name="remarks"></a>解説  
 このメソッドは、.NET Framework 4 の CLR バージョンより前の CLR バージョンでは機能しません。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** メタホスト .h  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICLRRuntimeInfo インターフェイス](iclrruntimeinfo-interface.md)
- [ホスト インターフェイス](hosting-interfaces.md)
- [ホスティング](index.md)
