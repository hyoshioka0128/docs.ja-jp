---
title: COR_PRF_SNAPSHOT_INFO 列挙型
ms.date: 03/30/2017
api_name:
- COR_PRF_SNAPSHOT_INFO
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- COR_PRF_SNAPSHOT_INFO
helpviewer_keywords:
- COR_PRF_SNAPSHOT_INFO enumeration [.NET Framework profiling]
ms.assetid: a5906b2a-ad4a-4cc6-a421-2d7d8adf7468
topic_type:
- apiref
ms.openlocfilehash: 6ade4f7877e39a8307a36f3a3268f79e8b4d44fd
ms.sourcegitcommit: 9a39f2a06f110c9c7ca54ba216900d038aa14ef3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/23/2019
ms.locfileid: "74427270"
---
# <a name="cor_prf_snapshot_info-enumeration"></a>COR_PRF_SNAPSHOT_INFO 列挙型
プロファイラーの[Stacksnapshotcallback](../../../../docs/framework/unmanaged-api/profiling/stacksnapshotcallback-function.md)関数を呼び出すたびに、スタックスナップショットで返すデータ量を指定します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
typedef enum _COR_PRF_SNAPSHOT_INFO {  
    COR_PRF_SNAPSHOT_DEFAULT = 0x0,  
    COR_PRF_SNAPSHOT_REGISTER_CONTEXT = 0x1,  
    COR_PRF_SNAPSHOT_X86_OPTIMIZED = 0X2  
} COR_PRF_SNAPSHOT_INFO;  
```  
  
## <a name="members"></a>メンバー  
  
|メンバー|説明|  
|-------------|-----------------|  
|`COR_PRF_SNAPSHOT_DEFAULT`|`context` パラメーターを除くすべての `StackSnapshotCallback` パラメーターに対して値を渡す必要があることを示します。|  
|`COR_PRF_SNAPSHOT_REGISTER_CONTEXT`|`context` パラメーターを含め、すべての `StackSnapshotCallback` パラメーターに対して値を渡す必要があることを示します。|  
|`COR_PRF_SNAPSHOT_X86_OPTIMIZED`|よりシンプルで代替のスタックウォークアルゴリズムが使用されることを示します。|  
  
## <a name="remarks"></a>コメント  
 `COR_PRF_SNAPSHOT_INFO` 列挙体によって指定された値は、 [DoStackSnapshot](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-dostacksnapshot-method.md)メソッドにパラメーターとして渡されます。  
  
## <a name="requirements"></a>要件  
 **:** 「[システム要件](../../../../docs/framework/get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー** : CorProf.idl、CorProf.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>参照

- [DoStackSnapshot メソッド](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-dostacksnapshot-method.md)
- [列挙型のプロファイリング](../../../../docs/framework/unmanaged-api/profiling/profiling-enumerations.md)
