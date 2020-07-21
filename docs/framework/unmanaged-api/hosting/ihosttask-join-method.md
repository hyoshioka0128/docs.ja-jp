---
title: IHostTask::Join メソッド
ms.date: 03/30/2017
api_name:
- IHostTask.Join
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostTask::Join
helpviewer_keywords:
- IHostTask::Join method [.NET Framework hosting]
- Join method, IHostTask interface [.NET Framework hosting]
ms.assetid: 2cffcc52-19e0-4ced-a440-fc7375078ac9
topic_type:
- apiref
ms.openlocfilehash: 20919bd9889408821cf57817082e3c7d5cebc240
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84503920"
---
# <a name="ihosttaskjoin-method"></a>IHostTask::Join メソッド
現在の[IHostTask](ihosttask-interface.md)インスタンスによって表されるタスクが完了するまで、または指定された時間が経過するか、または[IHostTask:: Alert](ihosttask-alert-method.md)が呼び出されるまで、呼び出し元のタスクをブロックします。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT Join (  
    [in] DWORD milliseconds,  
    [in] DWORD option  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `milliseconds`  
 からタスクの終了を待機する時間間隔 (ミリ秒単位)。 タスクが終了する前にこの間隔が経過すると、呼び出し元のタスクがブロック解除されます。  
  
 `option`  
 から[WAIT_OPTION](wait-option-enumeration.md)値の1つ。 値 WAIT_ALERTABLE `Alert` は、が経過する前にが呼び出された場合に、タスクをウェイクアップするようにホストに指示 `milliseconds` します。  
  
## <a name="return-value"></a>戻り値  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|`Join`正常に返されました。|  
|HOST_E_CLRNOTAVAILABLE|共通言語ランタイム (CLR) がプロセスに読み込まれていないか、CLR がマネージコードを実行できない状態であるか、または呼び出しが正常に処理されていません。|  
|HOST_E_TIMEOUT|呼び出しがタイムアウトしました。|  
|HOST_E_NOT_OWNER|呼び出し元がロックを所有していません。|  
|HOST_E_ABANDONED|ブロックされたスレッドまたはファイバーが待機中であるか、または現在の `IHostTask` インスタンスがタスクに関連付けられていないときに、イベントが取り消されました。|  
|E_FAIL|原因不明の致命的なエラーが発生しました。 メソッドが E_FAIL を返すと、そのプロセス内で CLR が使用できなくなります。 後続のホストメソッドの呼び出しでは HOST_E_CLRNOTAVAILABLE が返されます。|  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICLRTask インターフェイス](iclrtask-interface.md)
- [ICLRTaskManager インターフェイス](iclrtaskmanager-interface.md)
- [IHostTask インターフェイス](ihosttask-interface.md)
- [IHostTaskManager インターフェイス](ihosttaskmanager-interface.md)
- [WAIT_OPTION 列挙型](wait-option-enumeration.md)
