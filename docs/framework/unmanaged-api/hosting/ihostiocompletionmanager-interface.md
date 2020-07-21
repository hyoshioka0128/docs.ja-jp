---
title: IHostIoCompletionManager インターフェイス
ms.date: 03/30/2017
api_name:
- IHostIoCompletionManager
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostIoCompletionManager
helpviewer_keywords:
- IHostIoCompletionManager interface [.NET Framework hosting]
ms.assetid: c28d1983-83f7-46e2-990f-dbb9dc07c818
topic_type:
- apiref
ms.openlocfilehash: 095872f8d4bd4f7d3351b8b3e3f8f8445b615cd8
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84501539"
---
# <a name="ihostiocompletionmanager-interface"></a>IHostIoCompletionManager インターフェイス
共通言語ランタイム (CLR) がホストによって提供される i/o 完了ポートと対話できるようにするメソッドを提供します。  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[Bind メソッド](ihostiocompletionmanager-bind-method.md)|I/o 完了ポートにハンドルをバインドします。|  
|[CloseIoCompletionPort メソッド](ihostiocompletionmanager-closeiocompletionport-method.md)|以前のの呼び出しによって作成されたポートを閉じ `CreateIoCompletionPort` ます。|  
|[CreateIoCompletionPort メソッド](ihostiocompletionmanager-createiocompletionport-method.md)|ホストが新しい i/o 完了ポートを作成することを要求します。|  
|[GetAvailableThreads メソッド](ihostiocompletionmanager-getavailablethreads-method.md)|現在要求を処理していない i/o 完了スレッドの数を取得します。|  
|[GetHostOverlappedSize メソッド](ihostiocompletionmanager-gethostoverlappedsize-method.md)|ホストが i/o 要求に追加しようとしているカスタムデータのサイズを取得します。|  
|[GetMaxThreads メソッド](ihostiocompletionmanager-getmaxthreads-method.md)|ホストがサービス i/o 要求に割り当てることができるスレッドの最大数を取得します。|  
|[GetMinThreads メソッド](ihostiocompletionmanager-getminthreads-method.md)|ホストが i/o 要求を処理するために提供するスレッドの最小数を取得します。|  
|[InitializeHostOverlapped メソッド](ihostiocompletionmanager-initializehostoverlapped-method.md)|I/o 要求に関するカスタムデータを初期化する機会をホストに提供します。|  
|[SetCLRIoCompletionManager メソッド](ihostiocompletionmanager-setclriocompletionmanager-method.md)|CLR によって実装されている[Iclrio提供マネージャー](iclriocompletionmanager-interface.md)インスタンスへのインターフェイスポインターをホストに提供します。|  
|[SetMaxThreads メソッド](ihostiocompletionmanager-setmaxthreads-method.md)|ホストが大量の i/o 要求を処理するスレッドの最大数を設定します。|  
|[SetMinThreads メソッド](ihostiocompletionmanager-setminthreads-method.md)|ホストが i/o 完了に割り当てる必要があるスレッドの最小数を設定します。|  
  
## <a name="remarks"></a>解説  
 `IHostIoCompletionManager`CLR によって実装されるインターフェイスに対応し `ICLRIoCompletionManager` ます。 CLR は、のメソッドを呼び出して、 `IHostIoCompletionManager` ホストが提供するポートにハンドルをバインドします。また、ホストはのメソッドを呼び出して、i/o `ICLRIoCompletionManager` 要求の完了を報告します。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ホスト インターフェイス](hosting-interfaces.md)
