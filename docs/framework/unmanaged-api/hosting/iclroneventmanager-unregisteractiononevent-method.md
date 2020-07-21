---
title: ICLROnEventManager::UnregisterActionOnEvent メソッド
ms.date: 03/30/2017
api_name:
- ICLROnEventManager.UnregisterActionOnEvent
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLROnEventManager::UnregisterActionOnEvent
helpviewer_keywords:
- UnRegisterActionOnEvent method [.NET Framework hosting]
- ICLROnEventManager::UnRegisterActionOnEvent method [.NET Framework hosting]
ms.assetid: 4c02ec37-cdf0-46b2-890e-235092741236
topic_type:
- apiref
ms.openlocfilehash: a3018d8477d5abd7d03ad8675503624d2e44e8f4
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84504135"
---
# <a name="iclroneventmanagerunregisteractiononevent-method"></a>ICLROnEventManager::UnregisterActionOnEvent メソッド
指定されたイベントに対して、以前に登録されたコールバックポインターの登録を解除します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT UnregisterActionOnEvent (  
    [in] EClrEvent event,  
    [in] IActionOnCLREvent *pAction  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `event`  
 から[Eclrevent](eclrevent-enumeration.md)値の1つ。によって記述されたコールバックポインターの登録を解除する対象のイベントを示し `pAction` ます。  
  
 `pAction`  
 から[Registeractiononevent](iclroneventmanager-registeractiononevent-method.md)メソッドにパラメーターとして渡された[Iactiononclrevent](iactiononclrevent-interface.md)オブジェクトへのポインター。  
  
## <a name="return-value"></a>戻り値  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|`UnregisterActionOnEvent`正常に返されました。|  
|HOST_E_CLRNOTAVAILABLE|共通言語ランタイム (CLR) がプロセスに読み込まれていないか、CLR がマネージコードを実行できない状態であるか、または呼び出しが正常に処理されていません。|  
|HOST_E_TIMEOUT|呼び出しがタイムアウトしました。|  
|HOST_E_NOT_OWNER|呼び出し元がロックを所有していません。|  
|HOST_E_ABANDONED|ブロックされたスレッドまたはファイバーが待機しているときに、イベントが取り消されました。|  
|E_FAIL|原因不明の致命的なエラーが発生しました。 メソッドが E_FAIL を返すと、そのプロセス内で CLR が使用できなくなります。 後続のホストメソッドの呼び出しでは HOST_E_CLRNOTAVAILABLE が返されます。|  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [EClrEvent 列挙型](eclrevent-enumeration.md)
- [IActionOnCLREvent インターフェイス](iactiononclrevent-interface.md)
- [ICLRControl インターフェイス](iclrcontrol-interface.md)
- [ICLROnEventManager インターフェイス](iclroneventmanager-interface.md)
