---
title: IHostThreadPoolManager::SetMaxThreads メソッド
ms.date: 03/30/2017
api_name:
- IHostThreadPoolManager.SetMaxThreads
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostThreadPoolManager::SetMaxThreads
helpviewer_keywords:
- IHostThreadPoolManager::SetMaxThreads method [.NET Framework hosting]
- SetMaxThreads method, IHostThreadPoolManager interface [.NET Framework hosting]
ms.assetid: 77cfd347-95c2-4425-b807-4ecc2a8d4578
topic_type:
- apiref
ms.openlocfilehash: 53d42afda6668acc6462c419fcefd6bc1435a34c
ms.sourcegitcommit: e5772b3ddcc114c80b4c9767ffdb3f6c7fad8f05
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/26/2020
ms.locfileid: "83842453"
---
# <a name="ihostthreadpoolmanagersetmaxthreads-method"></a>IHostThreadPoolManager::SetMaxThreads メソッド
ホストがスレッドプールで保持できるスレッドの最大数を設定します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT SetMaxThreads (  
    [in] DWORD MaxThreads  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `MaxThreads`  
 スレッド プール内のワーカー スレッドの最大数。  
  
## <a name="return-value"></a>戻り値  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|`SetMaxThreads`正常に返されました。|  
|HOST_E_CLRNOTAVAILABLE|共通言語ランタイム (CLR) がプロセスに読み込まれていないか、CLR がマネージコードを実行できない状態であるか、または呼び出しが正常に処理されていません。|  
|HOST_E_TIMEOUT|呼び出しがタイムアウトしました。|  
|HOST_E_NOT_OWNER|呼び出し元がロックを所有していません。|  
|HOST_E_ABANDONED|ブロックされたスレッドまたはファイバーが待機しているときに、イベントが取り消されました。|  
|E_FAIL|不明な重大なエラーが発生しました。 メソッドが E_FAIL を返すと、そのプロセス内で CLR が使用できなくなります。 後続のホストメソッドの呼び出しでは HOST_E_CLRNOTAVAILABLE が返されます。|  
|E_NOTIMPL|ホストはの実装を提供していません `SetMaxThreads` 。|  
  
## <a name="remarks"></a>コメント  
 CLR がスレッドプールのサイズを構成できるようにするために、ホストは必要ありません。 ホストによっては、実装、パフォーマンス、スケーラビリティなどの理由から、スレッドプールを排他的に制御することが必要になる場合があります。 この場合、ホストは E_NOTIMPL の HRESULT 値を返す必要があります。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Threading.ThreadPool.SetMaxThreads%2A>
- <xref:System.Threading.ThreadPool>
- [GetMaxThreads メソッド](ihostthreadpoolmanager-getmaxthreads-method.md)
- [SetMinThreads メソッド](ihostthreadpoolmanager-setminthreads-method.md)
- [IHostThreadPoolManager インターフェイス](ihostthreadpoolmanager-interface.md)
