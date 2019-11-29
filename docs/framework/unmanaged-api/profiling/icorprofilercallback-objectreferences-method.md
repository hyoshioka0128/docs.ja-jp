---
title: ICorProfilerCallback::ObjectReferences メソッド
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback.ObjectReferences
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback::ObjectReferences
helpviewer_keywords:
- ObjectReferences method [.NET Framework profiling]
- ICorProfilerCallback::ObjectReferences method [.NET Framework profiling]
ms.assetid: dd5e9b64-b4a3-4ba6-9be6-ddb540f4ffcf
topic_type:
- apiref
ms.openlocfilehash: 4f8cfd912a3d6f66f5f2586a8942c7ce9bd52a63
ms.sourcegitcommit: 9a39f2a06f110c9c7ca54ba216900d038aa14ef3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/23/2019
ms.locfileid: "74445891"
---
# <a name="icorprofilercallbackobjectreferences-method"></a>ICorProfilerCallback::ObjectReferences メソッド
指定したオブジェクトによって参照されているメモリ内のオブジェクトに関する情報をプロファイラーに通知します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT ObjectReferences(  
    [in]  ObjectID objectId,  
    [in]  ClassID  classId,  
    [in]  ULONG    cObjectRefs,  
    [in, size_is(cObjectRefs)] ObjectID objectRefIds[] );  
```  
  
## <a name="parameters"></a>パラメーター  
 `objectId`  
 からオブジェクトを参照しているオブジェクトの ID。  
  
 `classId`  
 から指定したオブジェクトがインスタンスであるクラスの ID。  
  
 `cObjectRefs`  
 から指定したオブジェクトによって参照されるオブジェクトの数 (つまり、`objectRefIds` 配列内の要素の数)。  
  
 `objectRefIds`  
 から`objectId`によって参照されているオブジェクトの Id の配列。  
  
## <a name="remarks"></a>コメント  
 `ObjectReferences` メソッドは、ガベージコレクションが完了した後にヒープ内の残りのオブジェクトに対して呼び出されます。 プロファイラーがこのコールバックからエラーを返すと、プロファイリングサービスは、次のガベージコレクションまでこのコールバックの呼び出しを中止します。  
  
 `ObjectReferences` コールバックは、 [ICorProfilerCallback:: RootReferences](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-rootreferences-method.md)コールバックと組み合わせて使用して、ランタイムの完全なオブジェクト参照グラフを作成できます。 共通言語ランタイム (CLR) では、各オブジェクト参照が `ObjectReferences` メソッドによって1回だけ報告されるようにします。  
  
 `ObjectReferences` によって返されるオブジェクト Id は、コールバック自体では無効です。これは、ガベージコレクションがオブジェクトを移動する途中である可能性があるためです。 そのため、`ObjectReferences` の呼び出し中に、プロファイラーがオブジェクトの検査を試行することはできません。 [ICorProfilerCallback2:: GarbageCollectionFinished](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback2-garbagecollectionfinished-method.md)が呼び出されると、ガベージコレクションが完了し、検査を安全に行うことができます。  
  
 Null `ClassId` は、`objectId` にアンロード中の型があることを示します。  
  
## <a name="requirements"></a>要件  
 **:** 「[システム要件](../../../../docs/framework/get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー** : CorProf.idl、CorProf.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorProfilerCallback インターフェイス](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-interface.md)
