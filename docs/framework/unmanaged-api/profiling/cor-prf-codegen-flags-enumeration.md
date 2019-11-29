---
title: COR_PRF_CODEGEN_FLAGS 列挙体
ms.date: 03/30/2017
api_name:
- COR_PRF_CODEGEN_FLAGS
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- COR_PRF_CODEGEN_FLAGS
helpviewer_keywords:
- COR_PRF_CODEGEN_FLAGS enumeration [.NET Framework profiling]
ms.assetid: 3e184022-0247-4824-a23d-6b29593d8d01
topic_type:
- apiref
ms.openlocfilehash: c49bdcb9345960bce018cefd4443948f997c7267
ms.sourcegitcommit: 9a39f2a06f110c9c7ca54ba216900d038aa14ef3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/23/2019
ms.locfileid: "74428363"
---
# <a name="cor_prf_codegen_flags-enumeration"></a>COR_PRF_CODEGEN_FLAGS 列挙体
[ICorProfilerFunctionControl:: SetCodegenFlags](../../../../docs/framework/unmanaged-api/profiling/icorprofilerfunctioncontrol-setcodegenflags-method.md)メソッドで設定できるコード生成フラグを定義します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
typedef enum {  
    COR_PRF_CODEGEN_DISABLE_INLINING =          0x0001,  
    COR_PRF_CODEGEN_DISABLE_ALL_OPTIMIZATIONS = 0x0002,  
} COR_PRF_CODEGEN_FLAGS;  
```  
  
## <a name="members"></a>メンバー  
  
|メンバー|説明|  
|------------|-----------------|  
|`COR_PRF_CODEGEN_DISABLE_INLINING`|関数は、この関数の本体にインライン展開されません。 ただし、関数自体は、その呼び出し元にインライン展開される場合があります。|  
|`COR_PRF_CODEGEN_DISABLE_ALL_OPTIMIZATIONS`|この関数の本体では、すべての最適化が無効になります。 ただし、関数自体を呼び出し元にインライン化することはできます。|  
  
## <a name="remarks"></a>コメント  
 `COR_PRF_CODEGEN_FLAGS` 列挙体は、プロファイラーが JIT 再コンパイル関数のコード生成を制御できるようにするために、 [ICorProfilerFunctionControl:: SetCodegenFlags](../../../../docs/framework/unmanaged-api/profiling/icorprofilerfunctioncontrol-setcodegenflags-method.md)メソッドによって使用されます。  
  
## <a name="requirements"></a>要件  
 **:** 「[システム要件](../../../../docs/framework/get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー** : CorProf.idl、CorProf.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:** [!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>参照

- [列挙型のプロファイリング](../../../../docs/framework/unmanaged-api/profiling/profiling-enumerations.md)
