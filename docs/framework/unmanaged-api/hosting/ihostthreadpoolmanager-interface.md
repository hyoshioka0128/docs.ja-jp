---
title: IHostThreadPoolManager インターフェイス
ms.date: 03/30/2017
api_name:
- IHostThreadPoolManager
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostThreadPoolManager
helpviewer_keywords:
- IHostThreadPoolManager interface [.NET Framework hosting]
ms.assetid: c3a2cd90-7c4e-4374-bb87-b41befb8344f
topic_type:
- apiref
ms.openlocfilehash: bac29b5950f1547c5c60ac716d40d2ef4b1a2cc2
ms.sourcegitcommit: e5772b3ddcc114c80b4c9767ffdb3f6c7fad8f05
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/26/2020
ms.locfileid: "83842481"
---
# <a name="ihostthreadpoolmanager-interface"></a>IHostThreadPoolManager インターフェイス
共通言語ランタイム (CLR) がスレッドプールを構成し、作業項目をスレッドプールにキューするようにするメソッドを提供します。  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[GetAvailableThreads メソッド](ihostthreadpoolmanager-getavailablethreads-method.md)|現在作業項目を処理していないスレッドプール内のスレッドの数を取得します。|  
|[GetMaxThreads メソッド](ihostthreadpoolmanager-getmaxthreads-method.md)|ホストがスレッドプール内で同時に保持するスレッドの最大数を取得します。|  
|[GetMinThreads メソッド](ihostthreadpoolmanager-getminthreads-method.md)|要求を処理するためにホストが保持するアイドル状態のスレッドの最小数を取得します。|  
|[QueueUserWorkItem メソッド](ihostthreadpoolmanager-queueuserworkitem-method.md)|実行する関数をキューに配置し、関数によって使用されるデータを格納しているオブジェクトを提供します。|  
|[SetMaxThreads メソッド](ihostthreadpoolmanager-setmaxthreads-method.md)|ホストがスレッドプールで保持できるスレッドの最大数を設定します。|  
|[SetMinThreads メソッド](ihostthreadpoolmanager-setminthreads-method.md)|ホストが要求を見越して保持する必要があるアイドル状態のスレッドの最小数を設定します。|  
  
## <a name="remarks"></a>コメント  
 ホストは、 `SetMaxThreads` メソッドおよびメソッドの呼び出しで指定された値を使用して、スレッドプールを構成する必要はありません `SetMinThreads` 。 この場合、ホストは、これらのメソッドから E_NOTIMPL の HRESULT 値を返す必要があります。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Threading>
- <xref:System.Threading.ThreadPool>
- [ホスト インターフェイス](hosting-interfaces.md)
