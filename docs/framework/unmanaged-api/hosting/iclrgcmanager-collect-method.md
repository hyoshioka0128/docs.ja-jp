---
title: ICLRGCManager::Collect メソッド
ms.date: 03/30/2017
api_name:
- ICLRGCManager.Collect
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRGCManager::Collect
helpviewer_keywords:
- ICLRGCManager::Collect method [.NET Framework hosting]
- Collect method, ICLRGCManager interface [.NET Framework hosting]
ms.assetid: 0c6cbbea-c27c-4695-bda3-17c1910d8ddb
topic_type:
- apiref
ms.openlocfilehash: aa906e314c408b7653e611b07d7ad21d4519b715
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83616984"
---
# <a name="iclrgcmanagercollect-method"></a>ICLRGCManager::Collect メソッド
指定したジェネレーションのガベージコレクションを強制的に実行します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT Collect (  
    [in] LONG Generation  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `Generation`  
 から収集するジェネレーション。 値が-1 の場合は、すべてのジェネレーションのコレクションが強制的に実行します。  
  
## <a name="return-value"></a>戻り値  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|`Collect`正常に返されました。|  
|HOST_E_CLRNOTAVAILABLE|共通言語ランタイム (CLR) がプロセスに読み込まれていないか、CLR がマネージコードを実行できない状態であるか、または呼び出しが正常に処理されていません。|  
|HOST_E_TIMEOUT|呼び出しがタイムアウトしました。|  
|HOST_E_NOT_OWNER|呼び出し元がロックを所有していません。|  
|HOST_E_ABANDONED|ブロックされたスレッドまたはファイバーが待機しているときに、イベントが取り消されました。|  
|E_FAIL|原因不明の致命的なエラーが発生しました。 メソッドが E_FAIL を返すと、そのプロセス内で CLR が使用できなくなります。 後続のホストメソッドの呼び出しでは HOST_E_CLRNOTAVAILABLE が返されます。|  
  
## <a name="remarks"></a>解説  
 メソッドは、 `Collect` 現在の状態に関係なく、CLR のガベージコレクターがコレクションを実行するように強制します。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [自動メモリ管理](../../../standard/automatic-memory-management.md)
- [ガベージ コレクション](../../../standard/garbage-collection/index.md)
- [ICLRControl インターフェイス](iclrcontrol-interface.md)
- [ICLRGCManager インターフェイス](iclrgcmanager-interface.md)
- [CLR ホスト インターフェイス](clr-hosting-interfaces.md)
- [ホスト インターフェイス](hosting-interfaces.md)
- [ホスティング](index.md)
