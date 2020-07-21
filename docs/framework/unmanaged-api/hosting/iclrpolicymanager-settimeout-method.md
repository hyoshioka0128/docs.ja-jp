---
title: ICLRPolicyManager::SetTimeout メソッド
ms.date: 03/30/2017
api_name:
- ICLRPolicyManager.SetTimeout
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRPolicyManager::SetTimeout
helpviewer_keywords:
- SetTimeout method [.NET Framework hosting]
- ICLRPolicyManager::SetTimeout method [.NET Framework hosting]
ms.assetid: 954404fd-d52d-4e68-b582-8692f3a5f608
topic_type:
- apiref
ms.openlocfilehash: b3e66a1e04ca3f3031adf1f0f7f71d689ee76b04
ms.sourcegitcommit: 0926684d8d34f4c6b5acce58d2193db093cb9cf2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/20/2020
ms.locfileid: "83703411"
---
# <a name="iclrpolicymanagersettimeout-method"></a>ICLRPolicyManager::SetTimeout メソッド
指定された操作のタイムアウト値を設定します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT SetTimeout (  
    [in] EClrOperation operation,  
    [in] DWORD dsMilliseconds  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `operation`  
 からタイムアウトを設定する共通言語ランタイム (CLR) 操作を示す[EClrOperation](eclroperation-enumeration.md)値の1つ。 次の値がサポートされています。  
  
- OPR_AppDomainUnload  
  
- OPR_ProcessExit  
  
- OPR_ThreadRudeAbortInCriticalRegion  
  
- OPR_ThreadRudeAbortInNonCriticalRegion  
  
 `dwMilliseconds`  
 から新しいタイムアウト値 (ミリ秒単位)。 値を無限にすると、操作はタイムアウトしません。  
  
## <a name="return-value"></a>戻り値  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|`SetTimeout`正常に返されました。|  
|HOST_E_CLRNOTAVAILABLE|CLR がプロセスに読み込まれていないか、CLR がマネージドコードを実行できない状態であるか、または呼び出しが正常に処理されていません。|  
|HOST_E_TIMEOUT|呼び出しがタイムアウトしました。|  
|HOST_E_NOT_OWNER|呼び出し元がロックを所有していません。|  
|HOST_E_ABANDONED|ブロックされたスレッドまたはファイバーが待機しているときに、イベントが取り消されました。|  
|E_FAIL|原因不明の致命的なエラーが発生しました。 メソッドが E_FAIL を返すと、そのプロセス内で CLR が使用できなくなります。 後続のホストメソッドの呼び出しでは HOST_E_CLRNOTAVAILABLE が返されます。|  
|E_INVALIDARG|指定されたに対してタイムアウトを設定できない `operation` か、に無効な値が指定されました `operation` 。|  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [EClrOperation 列挙型](eclroperation-enumeration.md)
- [ICLRControl インターフェイス](iclrcontrol-interface.md)
- [ICLRPolicyManager インターフェイス](iclrpolicymanager-interface.md)
