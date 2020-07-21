---
title: ICorProfilerCallback2::GarbageCollectionStarted メソッド
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback2.GarbageCollectionStarted
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback2::GarbageCollectionStarted
helpviewer_keywords:
- GarbageCollectionStarted method [.NET Framework profiling]
- ICorProfilerCallback2::GarbageCollectionStarted method [.NET Framework profiling]
ms.assetid: 44eef087-f21f-4fe2-b481-f8a0ee022e7d
topic_type:
- apiref
ms.openlocfilehash: f025f4c0bc0ec8e11decddcdf64be50f68955266
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84499806"
---
# <a name="icorprofilercallback2garbagecollectionstarted-method"></a>ICorProfilerCallback2::GarbageCollectionStarted メソッド
ガベージコレクションが開始されたことをコードプロファイラーに通知します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GarbageCollectionStarted(  
    [in] int cGenerations,  
    [in, size_is(cGenerations), length_is(cGenerations)] BOOL generationCollected[],  
    [in] COR_PRF_GC_REASON reason);  
```  
  
## <a name="parameters"></a>パラメーター  
 `cGenerations`  
 から配列内のエントリの合計数 `generationCollected` 。  
  
 `generationCollected`  
 からブール値の配列 `true` 。配列インデックスに対応するジェネレーションがこのガベージコレクションによって収集されている場合は、それ以外の場合は `false` です。  
  
 配列は、生成を示す[COR_PRF_GC_GENERATION](cor-prf-gc-generation-enumeration.md)列挙体の値によってインデックスが作成されます。  
  
 `reason`  
 からガベージコレクションが発生した理由を示す[COR_PRF_GC_REASON](cor-prf-gc-reason-enumeration.md)列挙体の値。  
  
## <a name="remarks"></a>解説  
 このガベージコレクションに関連するすべてのコールバックは、 `GarbageCollectionStarted` コールバックとそれに対応する[ICorProfilerCallback2:: GarbageCollectionFinished](icorprofilercallback2-garbagecollectionfinished-method.md)コールバックの間で発生します。 これらのコールバックは、同じスレッドでは実行されません。  
  
 プロファイラーは、コールバック中に元の場所のオブジェクトを検査するのが安全です `GarbageCollectionStarted` 。 ガベージコレクターは、から戻った後にオブジェクトの移動を開始し `GarbageCollectionStarted` ます。 プロファイラーは、このコールバックから戻った後、コールバックを受信するまで、すべてのオブジェクト Id が無効であると見なす必要があり `ICorProfilerCallback2::GarbageCollectionFinished` ます。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー** : CorProf.idl、CorProf.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorProfilerCallback インターフェイス](icorprofilercallback-interface.md)
- [ICorProfilerCallback2 インターフェイス](icorprofilercallback2-interface.md)
