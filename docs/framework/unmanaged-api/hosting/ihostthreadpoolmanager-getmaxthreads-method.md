---
title: IHostThreadPoolManager::GetMaxThreads メソッド
ms.date: 03/30/2017
api_name:
- IHostThreadPoolManager.GetMaxThreads
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostThreadPoolManager::GetMaxThreads
helpviewer_keywords:
- IHostThreadPoolManager::GetMaxThreads method [.NET Framework hosting]
- GetMaxThreads method, IHostThreadPoolManager interface [.NET Framework hosting]
ms.assetid: db268876-6178-4a81-aca3-318ee7f96001
topic_type:
- apiref
ms.openlocfilehash: efbfa310c90f48c99219cb185f090a1b854949a2
ms.sourcegitcommit: e5772b3ddcc114c80b4c9767ffdb3f6c7fad8f05
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/26/2020
ms.locfileid: "83842284"
---
# <a name="ihostthreadpoolmanagergetmaxthreads-method"></a>IHostThreadPoolManager::GetMaxThreads メソッド
ホストがスレッドプール内で同時に保持するスレッドの最大数を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetMaxThreads (  
    [out] DWORD *pdwMaxWorkerThreads  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pdwMaxWorkerThreads`  
 入出力ホストがスレッドプールで保持するスレッドの最大数へのポインター。  
  
## <a name="return-value"></a>戻り値  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|`GetMaxThreads`正常に返されました。|  
|HOST_E_CLRNOTAVAILABLE|共通言語ランタイム (CLR (プロセスに読み込まれていない)、または CLR がマネージコードを実行できない状態であるか、または呼び出しが正常に処理されていません。|  
|HOST_E_TIMEOUT|呼び出しがタイムアウトしました。|  
|HOST_E_NOT_OWNER|呼び出し元がロックを所有していません。|  
|HOST_E_ABANDONED|ブロックされたスレッドまたはファイバーが待機しているときに、イベントが取り消されました。|  
|E_FAIL|原因不明の致命的なエラーが発生しました。 メソッドが E_FAIL を返すと、そのプロセス内で CLR が使用できなくなります。 後続のホストメソッドの呼び出しでは HOST_E_CLRNOTAVAILABLE が返されます。|  
|E_NOTIMPL|ホストはの実装を提供していません `GetMaxThreads` 。|  
  
## <a name="remarks"></a>コメント  
 CLR はを呼び出して、 `GetMaxThreads` スレッドプール内のスレッドの合計数を確認します。 [Get利用スレッド](ihostthreadpoolmanager-getavailablethreads-method.md)メソッドは、現在作業項目を処理していないスレッドの数を取得します。 パラメーターの戻り値を超えるすべての要求は `pdwMaxWorkerThreads` 、スレッドが使用可能になるまでキューに置かれたままになります。  
  
 ホストがの実装を提供していない場合 `GetMaxThreads` 、E_NOTIMPL の HRESULT 値が返されます。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Threading.ThreadPool.GetMaxThreads%2A>
- <xref:System.Threading.ThreadPool>
- [GetMinThreads メソッド](ihostthreadpoolmanager-getminthreads-method.md)
- [SetMaxThreads メソッド](ihostthreadpoolmanager-setmaxthreads-method.md)
- [IHostThreadPoolManager インターフェイス](ihostthreadpoolmanager-interface.md)
