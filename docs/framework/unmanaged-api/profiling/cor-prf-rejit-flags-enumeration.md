---
title: COR_PRF_REJIT_FLAGS 列挙型
ms.date: 08/06/2019
api_name:
- COR_PRF_REJIT_FLAGS Enumeration
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- COR_PRF_REJIT_FLAGS
helpviewer_keywords:
- COR_PRF_REJIT_FLAGS enumeration [.NET Framework profiling]
topic_type:
- apiref
author: davmason
ms.author: davmason
ms.openlocfilehash: 8fc5f1a488826d8adc6aecb8ef122609bebbe813
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79177098"
---
# <a name="cor_prf_rejit_flags-enumeration"></a>COR_PRF_REJIT_FLAGS 列挙型
[ICorProfilerInfo10::RequestReJITWithInライナー](icorprofilerinfo10-requestrejitwithinliners-method.md) API の動作を示す値が含まれています。  
  
## <a name="syntax"></a>構文  
  
```cpp  
typedef enum  
{
    COR_PRF_REJIT_BLOCK_INLINING = 0x1,
    COR_PRF_REJIT_INLINING_CALLBACKS    = 0x2
} COR_PRF_REJIT_FLAGS;  
```  
  
## <a name="members"></a>メンバー  
  
|メンバー|説明|  
|------------|-----------------|  
|`COR_PRF_REJIT_BLOCK_INLINING`| ReJITted メソッドは、他のメソッドでインライン化されないようにブロックされます。 |  
|`COR_PRF_REJIT_INLINING_CALLBACKS`| RejiTted を要求されたメソッドにインライン化するメソッドのコールバックを受信`GetFunctionParameters`します。 |  

## <a name="requirements"></a>必要条件  
 **プラットフォーム:** NET [Core サポートされるオペレーティング システム](../../../core/install/dependencies.md?pivots=os-windows)を参照してください。  
  
 **ヘッダー** : CorProf.idl、CorProf.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:** [!INCLUDE[net_core_22](../../../../includes/net-core-22-md.md)]
  
## <a name="see-also"></a>関連項目

- [列挙体のプロファイリング](profiling-enumerations.md)
