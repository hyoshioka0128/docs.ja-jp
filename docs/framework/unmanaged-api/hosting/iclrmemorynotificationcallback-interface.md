---
title: ICLRMemoryNotificationCallback インターフェイス
ms.date: 03/30/2017
api_name:
- ICLRMemoryNotificationCallback
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRMemoryNotificationCallback
helpviewer_keywords:
- ICLRMemoryNotificationCallback interface [.NET Framework hosting]
ms.assetid: 873639e2-4837-4568-83b3-4493e67e4174
topic_type:
- apiref
ms.openlocfilehash: 52fc21044d345998ad72c045cdf5e80a8a03a38e
ms.sourcegitcommit: 0926684d8d34f4c6b5acce58d2193db093cb9cf2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/20/2020
ms.locfileid: "83703803"
---
# <a name="iclrmemorynotificationcallback-interface"></a>ICLRMemoryNotificationCallback インターフェイス
Win32 関数と同様の方法を使用して、ホストがメモリ不足状態を報告できるようにし `CreateMemoryResourceNotification` ます。  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[OnMemoryNotification メソッド](iclrmemorynotificationcallback-onmemorynotification-method.md)|コンピューターのメモリ負荷の共通言語ランタイム (CLR) に通知します。|  
  
## <a name="remarks"></a>解説  
 ホストは、このインターフェイスを使用して、 `ICLRMemoryNotificationCallback` CLR のメモリリソースを解放するように要求します。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [IHostMemoryManager インターフェイス](ihostmemorymanager-interface.md)
- [ホスト インターフェイス](hosting-interfaces.md)
