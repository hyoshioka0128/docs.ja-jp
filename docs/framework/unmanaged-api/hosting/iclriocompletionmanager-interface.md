---
title: ICLRIoCompletionManager インターフェイス
ms.date: 03/30/2017
api_name:
- ICLRIoCompletionManager
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRIoCompletionManager
helpviewer_keywords:
- ICLRIoCompletionManager interface [.NET Framework hosting]
ms.assetid: c6c3ace6-e5e7-4450-8cc5-a9a48208c493
topic_type:
- apiref
ms.openlocfilehash: 71afc5e9772f82b922e8f428e6d808e46d092704
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84504213"
---
# <a name="iclriocompletionmanager-interface"></a>ICLRIoCompletionManager インターフェイス
ホストが、指定された i/o 要求のステータスの共通言語ランタイム (CLR) に通知するためのコールバックメソッドを実装します。  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[OnComplete メソッド](iclriocompletionmanager-oncomplete-method.md)|[Ihohooの](ihostiocompletionmanager-bind-method.md)呼び出しを使用して作成された i/o 要求の状態を CLR に通知します:: Bind メソッド。|  
  
## <a name="remarks"></a>解説  
 ホストは、 [Ihohoocompletion manager](ihostiocompletionmanager-interface.md)インターフェイスを使用して i/o 完了の抽象化を実装します。 CLR はこのインターフェイスを介して i/o 要求を行い、ホストはインターフェイスを使用して、そのような要求の結果をランタイムに通知し `ICLRIoCompletionManager` ます。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [IHostIoCompletionManager インターフェイス](ihostiocompletionmanager-interface.md)
- [IHostThreadPoolManager インターフェイス](ihostthreadpoolmanager-interface.md)
- [ホスト インターフェイス](hosting-interfaces.md)
