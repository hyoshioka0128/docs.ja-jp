---
title: EMemoryAvailable 列挙型
ms.date: 03/30/2017
api_name:
- EMemoryAvailable
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- EMemoryAvailable
helpviewer_keywords:
- EMemoryAvailable enumeration [.NET Framework hosting]
ms.assetid: 38e72a06-dbed-473b-a59b-7e0b3ea4f2af
topic_type:
- apiref
ms.openlocfilehash: 822396e28d000a5309738680fec502e1aeacd67c
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83616217"
---
# <a name="ememoryavailable-enumeration"></a>EMemoryAvailable 列挙型
コンピューターの空き物理メモリの量を示す値を格納します。 これらの値は、Windows API の関数から返されるメモリの量が多い場合のイベントに論理的にマップされ `CreateMemoryResourceNotification` ます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
typedef enum {  
    eMemoryAvailableLow     = 1,  
    eMemoryAvailableNeutral = 2,  
    eMemoryAvailableHigh    = 3
} EMemoryAvailable;  
```  
  
## <a name="members"></a>メンバー  
  
|メンバー|説明|  
|------------|-----------------|  
|`eMemoryAvailableHigh`|十分な物理メモリを使用できます。|  
|`eMemoryAvailableLow`|使用できる物理メモリが非常に少なくなっています。|  
|`eMemoryAvailableNeutral`|使用可能な物理メモリはニュートラルです。|  
  
## <a name="remarks"></a>解説  
 この値は、 [ICLRMemoryNotificationCallback:: OnMemoryNotification](iclrmemorynotificationcallback-onmemorynotification-method.md)メソッドの呼び出しを使用して、ホストによって共通言語ランタイム (CLR) に渡されます。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ホスティングの列挙体](hosting-enumerations.md)
