---
title: ICLRIoCompletionManager::OnComplete メソッド
ms.date: 03/30/2017
api_name:
- ICLRIoCompletionManager.OnComplete
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRIoCompletionManager::OnComplete
helpviewer_keywords:
- OnComplete method [.NET Framework hosting]
- ICLRIoCompletionManager::OnComplete method [.NET Framework hosting]
ms.assetid: 003f6974-9727-4322-bed5-e330d1224d0b
topic_type:
- apiref
ms.openlocfilehash: 39c9752912e88b04455516c0e9bed43610ba8aa0
ms.sourcegitcommit: 0926684d8d34f4c6b5acce58d2193db093cb9cf2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/20/2020
ms.locfileid: "83703816"
---
# <a name="iclriocompletionmanageroncomplete-method"></a>ICLRIoCompletionManager::OnComplete メソッド
[Ihohooの](ihostiocompletionmanager-bind-method.md)呼び出しを使用して作成された i/o 要求の状態を共通言語ランタイム (CLR) に通知します:: Bind メソッド。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT OnComplete (  
    [in] DWORD dwErrorCode,  
    [in] DWORD NumberOfBytesTransferred,  
    [in] void* pvOverlapped  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `dwErrorCode`  
 からバインド操作の状態を示す HRESULT 値です。  
  
- S_OK は、操作が正常に完了したことを示します。  
  
- HOST_E_INTERRUPTED は、呼び出しが完了前に終了したことを示します。  
  
- E_FAIL は、不明で回復不可能な重大なエラーが発生したことを示します。  
  
 `NumberOfBytesTransferred`  
 からI/o 要求の処理中に転送されたバイト数。  
  
 `pvOverlapped`  
 から`OVERLAPPED`メソッドの呼び出しに渡された構造体へのポインター `IHostIoCompletionManager::Bind` 。  
  
## <a name="return-value"></a>戻り値  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|`OnComplete`正常に返されました。|  
|HOST_E_CLRNOTAVAILABLE|CLR がプロセスに読み込まれていないか、CLR がマネージドコードを実行できない状態であるか、または呼び出しが正常に処理されていません。|  
|HOST_E_TIMEOUT|呼び出しがタイムアウトしました。|  
|HOST_E_NOT_OWNER|呼び出し元がロックを所有していません。|  
|HOST_E_ABANDONED|ブロックされたスレッドまたはファイバーが待機しているときに、イベントが取り消されました。|  
|E_FAIL|原因不明の致命的なエラーが発生しました。 メソッドが E_FAIL を返すと、そのプロセス内で CLR が使用できなくなります。 後続のホストメソッドの呼び出しでは HOST_E_CLRNOTAVAILABLE が返されます。|  
  
## <a name="remarks"></a>解説  
 ホストで i/o 完了の抽象化が実装されている場合、CLR は[Iho/ocompletion manager](ihostiocompletionmanager-interface.md)のメソッドを使用して、ホストを介して i/o 要求を行います。 次に、ホストはメソッドを呼び出して、その `OnComplete` ような要求の結果をランタイムに通知します。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICLRIoCompletionManager インターフェイス](iclriocompletionmanager-interface.md)
- [IHostIoCompletionManager インターフェイス](ihostiocompletionmanager-interface.md)
- [IHostThreadPoolManager インターフェイス](ihostthreadpoolmanager-interface.md)
