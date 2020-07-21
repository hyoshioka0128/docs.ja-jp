---
title: ICLROnEventManager::RegisterActionOnEvent メソッド
ms.date: 03/30/2017
api_name:
- ICLROnEventManager.RegisterActionOnEvent
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLROnEventManager::RegisterActionOnEvent
helpviewer_keywords:
- ICLROnEventManager::RegisterActionOnEvent method [.NET Framework hosting]
- RegisterActionOnEvent method [.NET Framework hosting]
ms.assetid: b944cf49-918d-4c4e-993b-77d097a52550
topic_type:
- apiref
ms.openlocfilehash: e634b3876d51d461446ed3f5ae537ac1db1545bd
ms.sourcegitcommit: 0926684d8d34f4c6b5acce58d2193db093cb9cf2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/20/2020
ms.locfileid: "83703505"
---
# <a name="iclroneventmanagerregisteractiononevent-method"></a>ICLROnEventManager::RegisterActionOnEvent メソッド
指定されたイベントのコールバックポインターを登録します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT RegisterActionOnEvent (  
    [in] EClrEvent event,  
    [in] IActionOnCLREvent *pAction  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `event`  
 から[Eclrevent](eclrevent-enumeration.md)値の1つ。によって記述されるコールバックポインターを登録するイベントを示し `pAction` ます。  
  
 `pAction`  
 から登録されたイベントが発生したときに呼び出される[Iactiononclrevent](iactiononclrevent-interface.md)オブジェクトへのポインター。  
  
## <a name="return-value"></a>戻り値  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|`RegisterActionOnEvent`正常に返されました。|  
|HOST_E_CLRNOTAVAILABLE|共通言語ランタイム (CLR) がプロセスに読み込まれていないか、CLR がマネージコードを実行できない状態であるか、または呼び出しが正常に処理されていません。|  
|HOST_E_TIMEOUT|呼び出しがタイムアウトしました。|  
|HOST_E_NOT_OWNER|呼び出し元がロックを所有していません。|  
|HOST_E_ABANDONED|ブロックされたスレッドまたはファイバーが待機しているときに、イベントが取り消されました。|  
|E_FAIL|原因不明の致命的なエラーが発生しました。 メソッドが E_FAIL を返すと、そのプロセス内で CLR が使用できなくなります。 後続のホストメソッドの呼び出しでは HOST_E_CLRNOTAVAILABLE が返されます。|  
  
## <a name="remarks"></a>解説  
 ホストは、で説明されている2つのイベントの種類のいずれかまたは両方のコールバックを登録でき `EClrEvent` ます。 ホストは、 `ICLROnEventManager` [ICLRControl:: GetCLRManager](iclrcontrol-getclrmanager-method.md)メソッドを呼び出すことによって、インターフェイスを取得します。  
  
> [!NOTE]
> 登録するイベントは、 `RegisterActionOnEvent` 複数の異なるスレッドから起動して、CLR のアンロードまたは無効化を通知することができます。  
  
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
