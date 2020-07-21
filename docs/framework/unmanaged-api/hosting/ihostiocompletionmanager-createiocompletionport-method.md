---
title: IHostIoCompletionManager::CreateIoCompletionPort メソッド
ms.date: 03/30/2017
api_name:
- IHostIoCompletionManager.CreateIoCompletionPort
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostIoCompletionManager::CreateIoCompletionPort
helpviewer_keywords:
- IHostIoCompletionManager::CreateIoCompletionPort method [.NET Framework hosting]
- CreateIoCompletionPort method [.NET Framework hosting]
ms.assetid: 907a2b43-68db-44a7-acac-89e792e7bb3c
topic_type:
- apiref
ms.openlocfilehash: 240712296254e02f4d268a00e1c15ef34f4519f1
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84501548"
---
# <a name="ihostiocompletionmanagercreateiocompletionport-method"></a>IHostIoCompletionManager::CreateIoCompletionPort メソッド
ホストが新しい i/o 完了ポートを作成することを要求します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT CreateIoCompletionPort (  
    [out] HANDLE *phPort  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `phPort`  
 入出力新しく作成された i/o 完了ポートのハンドルへのポインター。ポートを作成できなかった場合は 0 (ゼロ)。  
  
## <a name="return-value"></a>戻り値  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|`CreateIoCompletionPort`正常に返されました。|  
|HOST_E_CLRNOTAVAILABLE|共通言語ランタイム (CLR) がプロセスに読み込まれていないか、CLR がマネージコードを実行できない状態であるか、または呼び出しが正常に処理されていません。|  
|HOST_E_TIMEOUT|呼び出しがタイムアウトしました。|  
|HOST_E_NOT_OWNER|呼び出し元がロックを所有していません。|  
|HOST_E_ABANDONED|ブロックされたスレッドまたはファイバーが待機しているときに、イベントが取り消されました。|  
|E_FAIL|原因不明の致命的なエラーが発生しました。 メソッドが E_FAIL を返すと、そのプロセス内で CLR が使用できなくなります。 後続のホストメソッドの呼び出しでは HOST_E_CLRNOTAVAILABLE が返されます。|  
|E_OUTOFMEMORY|要求されたリソースを割り当てるのに十分なメモリがありませんでした。|  
  
## <a name="remarks"></a>解説  
 CLR は、メソッドを呼び出して、 `CreateIoCompletionPort` ホストが新しい i/o 完了ポートを作成するように要求します。 このポートは、 [Ihoを](ihostiocompletionmanager-bind-method.md)呼び出して、このポートに i/o 操作をバインドします。 ホストは、 [Iclriocomplete manager:: OnComplete](iclriocompletionmanager-oncomplete-method.md)を呼び出すことによって、状態を CLR に報告します。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICLRIoCompletionManager インターフェイス](iclriocompletionmanager-interface.md)
- [IHostIoCompletionManager インターフェイス](ihostiocompletionmanager-interface.md)
