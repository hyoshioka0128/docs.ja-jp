---
title: ICorProfilerInfo2::GetObjectGeneration メソッド
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo2.GetObjectGeneration
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo2::GetObjectGeneration
helpviewer_keywords:
- GetObjectGeneration method [.NET Framework profiling]
- ICorProfilerInfo2::GetObjectGeneration method [.NET Framework profiling]
ms.assetid: b0d25f76-0bd5-4aa6-96cf-bfec0e1de28b
topic_type:
- apiref
ms.openlocfilehash: 1263202c1fe524c924a88b9356e5ab9116cea553
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84502861"
---
# <a name="icorprofilerinfo2getobjectgeneration-method"></a>ICorProfilerInfo2::GetObjectGeneration メソッド
指定されたオブジェクトを格納しているヒープのセグメントを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetObjectGeneration(  
    [in] ObjectID objectId,  
    [out] COR_PRF_GC_GENERATION_RANGE *range);  
```  
  
## <a name="parameters"></a>パラメーター  
 `objectId`  
 からオブジェクトの ID です。  
  
 `range`  
 入出力ガベージコレクション中のジェネレーション内のメモリの範囲 (つまり、ブロック) を記述する[COR_PRF_GC_GENERATION_RANGE](cor-prf-gc-generation-range-structure.md)構造体へのポインター。 この範囲には、指定されたオブジェクトが含まれます。  
  
## <a name="remarks"></a>解説  
 `GetObjectGeneration`ガベージコレクションが実行されていない場合は、任意のプロファイラーコールバックからメソッドを呼び出すことができます。 つまり、 [ICorProfilerCallback2:: GarbageCollectionStarted](icorprofilercallback2-garbagecollectionstarted-method.md)と[ICorProfilerCallback2:: GarbageCollectionFinished](icorprofilercallback2-garbagecollectionfinished-method.md)の間で発生するものを除き、任意のコールバックから呼び出すことができます。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー** : CorProf.idl、CorProf.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorProfilerInfo インターフェイス](icorprofilerinfo-interface.md)
- [ICorProfilerInfo2 インターフェイス](icorprofilerinfo2-interface.md)
