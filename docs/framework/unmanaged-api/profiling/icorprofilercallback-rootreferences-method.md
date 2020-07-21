---
title: ICorProfilerCallback::RootReferences メソッド
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback.RootReferences
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback::RootReferences
helpviewer_keywords:
- RootReferences method [.NET Framework profiling]
- ICorProfilerCallback::RootReferences method [.NET Framework profiling]
ms.assetid: dbdf853b-d1a4-4828-8ef7-53d121d8e6ae
topic_type:
- apiref
ms.openlocfilehash: b587f30a01623c6e9806bcd9d01058a0880be239
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84499910"
---
# <a name="icorprofilercallbackrootreferences-method"></a>ICorProfilerCallback::RootReferences メソッド
ガベージコレクション後のルート参照に関する情報をプロファイラーに通知します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT RootReferences(  
    [in] ULONG    cRootRefs,  
    [in, size_is(cRootRefs)] ObjectID rootRefIds[] );  
```  
  
## <a name="parameters"></a>パラメーター  
 `cRootRefs`  
 から配列内の参照の数 `rootRefIds` 。  
  
 `rootRefIds`  
 から静的オブジェクトまたはスタック上のオブジェクトのいずれかを参照するオブジェクト Id の配列。  
  
## <a name="remarks"></a>解説  
 `RootReferences`と[ICorProfilerCallback2:: RootReferences2](icorprofilercallback2-rootreferences2-method.md)の両方が呼び出され、プロファイラーに通知されます。 通常、プロファイラーはどちらか一方を実装しますが、渡され `RootReferences2` た情報は渡されたのスーパーセットであるため、両方ではありません `RootReferences` 。  
  
 `rootRefIds`配列に null オブジェクトが含まれている可能性があります。 たとえば、スタックで宣言されたすべてのオブジェクト参照は、ガベージコレクターによってルートとして扱われ、常に報告されます。  
  
 によって返されるオブジェクト Id `RootReferences` は、コールバック自体では無効です。これは、ガベージコレクションが古いアドレスから新しいアドレスにオブジェクトを移動する途中にある可能性があるためです。 そのため、呼び出し中にプロファイラーがオブジェクトの検査を試行することはできません `RootReferences` 。 [ICorProfilerCallback2:: GarbageCollectionFinished](icorprofilercallback2-garbagecollectionfinished-method.md)が呼び出されると、すべてのオブジェクトが新しい場所に移動され、安全に検査できるようになります。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー** : CorProf.idl、CorProf.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorProfilerCallback インターフェイス](icorprofilercallback-interface.md)
