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
ms.openlocfilehash: 6168c5b27868a261871b292e17ca02b04ae89917
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84500781"
---
# <a name="cor_prf_snapshot_info-enumeration"></a>COR_PRF_SNAPSHOT_INFO 列挙型
プロファイラーの[Stacksnapshotcallback](stacksnapshotcallback-function.md)関数を呼び出すたびに、スタックスナップショットで返すデータ量を指定します。  
  
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
|`COR_PRF_SNAPSHOT_DEFAULT`|パラメーターを除くすべてのパラメーターに対して値を渡す必要があることを示し `StackSnapshotCallback` `context` ます。|  
|`COR_PRF_SNAPSHOT_REGISTER_CONTEXT`|パラメーターを含むすべてのパラメーターに対して値を渡す必要があることを示し `StackSnapshotCallback` `context` ます。|  
|`COR_PRF_SNAPSHOT_X86_OPTIMIZED`|よりシンプルで代替のスタックウォークアルゴリズムが使用されることを示します。|  
  
## <a name="remarks"></a>解説  
 列挙体によって指定された値 `COR_PRF_SNAPSHOT_INFO` は、パラメーターとして[DoStackSnapshot](icorprofilerinfo2-dostacksnapshot-method.md)メソッドに渡されます。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー** : CorProf.idl、CorProf.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [DoStackSnapshot メソッド](icorprofilerinfo2-dostacksnapshot-method.md)
- [列挙体のプロファイリング](profiling-enumerations.md)
