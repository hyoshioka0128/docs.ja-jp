---
title: ICLRSyncManager::CreateRWLockOwnerIterator メソッド
ms.date: 03/30/2017
api_name:
- ICLRSyncManager.CreateRWLockOwnerIterator
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRSyncManager::CreateRWLockOwnerIterator
helpviewer_keywords:
- ICLRSyncManager::CreateRWLockOwnerIterator method [.NET Framework hosting]
- CreateRWLockOwnerIterator method [.NET Framework hosting]
ms.assetid: b5535b87-9439-424e-b9b3-7d6fafb9819e
topic_type:
- apiref
ms.openlocfilehash: f8fde4905c41dffde90c6361b5a8cdffa15deb4a
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84503966"
---
# <a name="iclrsyncmanagercreaterwlockowneriterator-method"></a>ICLRSyncManager::CreateRWLockOwnerIterator メソッド
リーダーライターロックを待機しているタスクのセットを決定するために使用するホストの反復子を共通言語ランタイム (CLR) が作成することを要求します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT CreateRWLockOwnerIterator (  
    [in]  SIZE_T    cookie,  
    [out] SIZE_T   *pIterator  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `cookie`  
 から目的のリーダーライターロックに関連付けられているクッキー。  
  
 `pIterator`  
 入出力[GetRWLockOwnerNext](iclrsyncmanager-getrwlockownernext-method.md)メソッドおよび[DeleteRWLockOwnerIterator](iclrsyncmanager-deleterwlockowneriterator-method.md)メソッドに渡すことができる反復子へのポインター。  
  
## <a name="return-value"></a>戻り値  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|`CreateRWLockOwnerIterator`正常に返されました。|  
|HOST_E_CLRNOTAVAILABLE|CLR がプロセスに読み込まれていないか、CLR がマネージドコードを実行できない状態であるか、または呼び出しが正常に処理されていません。|  
|HOST_E_TIMEOUT|呼び出しがタイムアウトしました。|  
|HOST_E_NOT_OWNER|呼び出し元がロックを所有していません。|  
|HOST_E_ABANDONED|ブロックされたスレッドまたはファイバーが待機しているときに、イベントが取り消されました。|  
|E_FAIL|原因不明の致命的なエラーが発生しました。 メソッドが E_FAIL を返すと、そのプロセス内で CLR が使用できなくなります。 後続のホストメソッドの呼び出しでは HOST_E_CLRNOTAVAILABLE が返されます。|  
|HOST_E_INVALIDOPERATION|`CreateRWLockOwnerIterator`は、現在マネージコードを実行しているスレッドで呼び出されました。|  
  
## <a name="remarks"></a>解説  
 通常、ホストは `CreateRWLockOwnerIterator` 、 `DeleteRWLockOwnerIterator` デッドロックの検出時に、、およびの各メソッドを呼び出し `GetRWLockOwnerNext` ます。 ホストは、リーダーライターロックが有効であることを CLR が防ぐため、リーダーライターロックが引き続き有効であることを保証する役割を担います。 ホストでは、次のようないくつかの方法でロックの有効性を確認できます。  
  
- ホストは、このブロックでデッドロックが発生しないようにするために、リーダーライターロック (たとえば、 [IHostSemaphore:: ReleaseSemaphore](ihostsemaphore-releasesemaphore-method.md)) でのリリース呼び出しをブロックできます。  
  
- ホストは、リーダーライターロックに関連付けられているイベントオブジェクトでの終了の待機をブロックできます。このブロックによってデッドロックが発生しないようにします。  
  
> [!NOTE]
> `CreateRWLockOwnerIterator`は、現在アンマネージコードを実行しているスレッドでのみ呼び出す必要があります。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICLRSyncManager インターフェイス](iclrsyncmanager-interface.md)
- [IHostSyncManager インターフェイス](ihostsyncmanager-interface.md)
