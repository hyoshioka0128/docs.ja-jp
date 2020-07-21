---
title: WAIT_OPTION 列挙型
ms.date: 03/30/2017
api_name:
- WAIT_OPTION
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- WAIT_OPTION
helpviewer_keywords:
- WAIT_OPTION enumeration [.NET Framework hosting]
ms.assetid: 962fc293-8ded-4b3b-90ce-2c21a4f1b244
topic_type:
- apiref
ms.openlocfilehash: 2f83bc5b114b746958f936c311efa823d88441d1
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84503888"
---
# <a name="wait_option-enumeration"></a>WAIT_OPTION 列挙型
共通言語ランタイム (CLR) ブロックによって操作が要求された場合にホストが実行するアクションを示す値を格納します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
typedef enum {  
    WAIT_MSGPUMP       = 0x1,  
    WAIT_ALERTABLE     = 0x2,  
    WAIT_NOTINDEADLOCK = 0x4,  
} WAIT_OPTION;  
```  
  
## <a name="members"></a>メンバー  
  
|メンバー|説明|  
|------------|-----------------|  
|`WAIT_ALERTABLE`|CLR が[IHostTask:: Alert](ihosttask-alert-method.md)メソッドを呼び出した場合に、タスクが起こされる必要があることをホストに通知します。|  
|`WAIT_MSGPUMP`|スレッドがブロックされた場合に、現在の OS スレッドでメッセージをポンプする必要があることをホストに通知します。 ランタイムは、スレッドに対してのみこの値を指定し <xref:System.Threading.ApartmentState.STA> ます。|  
|`WAIT_NOTINDEADLOCK`|指定された同期要求がホストによって壊れていないことをホストに通知します。 つまり、ホストはを返すことができません `HOST_E_DEADLOCK` 。|  
  
## <a name="remarks"></a>解説  
 [IHostTaskManager:: Sleep](ihosttaskmanager-sleep-method.md)メソッドと[IHostTaskManager:: switchtotask](ihosttaskmanager-switchtotask-method.md)メソッドは、どちらもこの型のパラメーターを受け取ります。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ホスティングの列挙型](hosting-enumerations.md)
