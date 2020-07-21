---
title: COR_PRF_GC_ROOT_FLAGS 列挙型
ms.date: 03/30/2017
api_name:
- COR_PRF_GC_ROOT_FLAGS
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- COR_PRF_GC_ROOT_FLAGS
helpviewer_keywords:
- COR_PRF_GC_ROOT_FLAGS enumeration [.NET Framework profiling]
ms.assetid: 4611ee6f-0f05-4d84-91e1-e83d5e7dd7e4
topic_type:
- apiref
ms.openlocfilehash: bbc163c71b47e6fee0db89284d6e3fd27e882768
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84500890"
---
# <a name="cor_prf_gc_root_flags-enumeration"></a>COR_PRF_GC_ROOT_FLAGS 列挙型
ガベージコレクションのルートのプロパティを示します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
typedef enum {  
    COR_PRF_GC_ROOT_PINNING = 0x1,  
    COR_PRF_GC_ROOT_WEAKREF = 0x2,  
    COR_PRF_GC_ROOT_INTERIOR = 0x4,  
    COR_PRF_GC_ROOT_REFCOUNTED = 0x8,  
} COR_PRF_GC_ROOT_FLAGS;  
```  
  
## <a name="members"></a>メンバー  
  
|メンバー|説明|  
|------------|-----------------|  
|`COR_PRF_GC_ROOT_PINNING`|ルートは、ガベージコレクションがオブジェクトを移動できないようにします。|  
|`COR_PRF_GC_ROOT_WEAKREF`|ルートによってガベージコレクションが妨げられることはありません。|  
|`COR_PRF_GC_ROOT_INTERIOR`|ルートは、オブジェクト自体ではなく、オブジェクトのフィールドを参照します。|  
|`COR_PRF_GC_ROOT_REFCOUNTED`|オブジェクトの参照カウントが特定の値の場合、ルートはガベージコレクションを防止します。|  
  
## <a name="remarks"></a>解説  
 `COR_PRF_GC_ROOT_FLAGS`は、特別なルートに関する追加情報を提供するビットマスクです。 ただし、すべてのルートが特別であるとは限りません。 たとえば、一部のルートは、弱い参照、内部ポインター、ピン留め、または参照カウントされていません。 このようなルートの場合、伝えるフラグはありません。 したがって、 [ICorProfilerCallback2:: RootReferences2](icorprofilercallback2-rootreferences2-method.md)メソッドなど、この列挙を使用するメソッドは、フラグのビットマスクとして0を送信し、すべてのフラグがオフになっていることを示します。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー** : CorProf.idl、CorProf.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [列挙体のプロファイリング](profiling-enumerations.md)
