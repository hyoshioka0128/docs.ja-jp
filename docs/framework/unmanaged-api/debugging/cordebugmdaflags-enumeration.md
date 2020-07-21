---
title: CorDebugMDAFlags 列挙型
ms.date: 03/30/2017
api_name:
- CorDebugMDAFlags
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- CorDebugMDAFlags
helpviewer_keywords:
- CorDebugMDAFlags enumeration [.NET Framework debugging]
ms.assetid: 7c0c92fe-8bd2-477f-b307-aca0143732ca
topic_type:
- apiref
ms.openlocfilehash: e024500ea66dcb42e712e07e976a709401160a27
ms.sourcegitcommit: de7f589de07a9979b6ac28f54c3e534a617d9425
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/05/2020
ms.locfileid: "82795769"
---
# <a name="cordebugmdaflags-enumeration"></a>CorDebugMDAFlags 列挙型
マネージド デバッグ アシスタント (MDA) が生成されるスレッドのステータスを指定します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
typedef enum CorDebugMDAFlags {  
    MDA_FLAG_SLIP = 0x2  
} CorDebugMDAFlags;  
```  
  
## <a name="members"></a>メンバー  
  
|メンバー|説明|  
|------------|-----------------|  
|`MDA_FLAG_SLIP`|Mda が起動されてから、MDA が起動されたスレッドが遅れています。|  
  
## <a name="remarks"></a>Remarks  
 呼び出し履歴で、MDA が最初に発生した場所が記述されなくなった場合、スレッドは*遅れ*ていると見なされます。 これは、スレッドが終了時に無効な操作を実行したことによって発生する異常な状況です。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [列挙体のデバッグ](debugging-enumerations.md)
