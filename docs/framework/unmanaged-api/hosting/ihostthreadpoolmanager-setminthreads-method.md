---
title: IHostThreadPoolManager::SetMinThreads メソッド
ms.date: 03/30/2017
api_name:
- IHostThreadPoolManager.SetMinThreads
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostThreadPoolManager::SetMinThreads
helpviewer_keywords:
- SetMinThreads method, IHostThreadPoolManager interface [.NET Framework hosting]
- IHostThreadPoolManager::SetMinThreads method [.NET Framework hosting]
ms.assetid: 10409db9-9fd2-4e4d-b8cd-cf6fec0afaa2
topic_type:
- apiref
ms.openlocfilehash: c5b150b161acba3820ced367049f08153dd091aa
ms.sourcegitcommit: e5772b3ddcc114c80b4c9767ffdb3f6c7fad8f05
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/26/2020
ms.locfileid: "83842440"
---
# <a name="ihostthreadpoolmanagersetminthreads-method"></a>IHostThreadPoolManager::SetMinThreads メソッド
ホストが要求を見越して保持する必要があるアイドル状態のスレッドの最小数を設定します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT SetMinThreads (  
    [in] DWORD MinThreads  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `MinThreads`  
 からホストが保持する必要があるスレッドの新しい最小数。  
  
## <a name="return-value"></a>戻り値  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|`SetMinThreads`正常に返されました。|  
|HOST_E_CLRNOTAVAILABLE|共通言語ランタイム (CLR) がプロセスに読み込まれていないか、CLR がマネージコードを実行できない状態であるか、または呼び出しが正常に処理されていません。|  
|HOST_E_TIMEOUT|呼び出しがタイムアウトしました。|  
|HOST_E_NOT_OWNER|呼び出し元がロックを所有していません。|  
|HOST_E_ABANDONED|ブロックされたスレッドまたはファイバーが待機しているときに、イベントが取り消されました。|  
|E_FAIL|原因不明の致命的なエラーが発生しました。 メソッドが E_FAIL を返すと、そのプロセス内で CLR が使用できなくなります。 後続のホストメソッドの呼び出しでは HOST_E_CLRNOTAVAILABLE が返されます。|  
|E_NOTIMPL|ホストはの実装を提供していません `SetMinThreads` 。|  
  
## <a name="remarks"></a>コメント  
 ホストは、の実装を提供する必要はありません `SetMinThreads` 。 この場合、E_NOTIMPL の HRESULT 値が返されます。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Threading.ThreadPool.SetMinThreads%2A>
- <xref:System.Threading.ThreadPool>
- [GetMinThreads メソッド](ihostthreadpoolmanager-getminthreads-method.md)
- [SetMaxThreads メソッド](ihostthreadpoolmanager-setmaxthreads-method.md)
- [IHostThreadPoolManager インターフェイス](ihostthreadpoolmanager-interface.md)
